---
title: "Protezione dei servizi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "configurazione [WCF], protezione dei servizi"
  - "Sicurezza WCF"
  - "WCF, sicurezza"
ms.assetid: f0ecc6f7-f4b5-42a4-9cb1-b02e28e26620
caps.latest.revision: 28
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 28
---
# Protezione dei servizi
La protezione di un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] è costituita da due requisiti principali: protezione del trasferimento e autorizzazione. Un terzo requisito, ovvero il controllo degli eventi di sicurezza, viene descritto in [Controllo](../../../docs/framework/wcf/feature-details/auditing-security-events.md). In sintesi, la protezione del trasferimento include l'autenticazione \(verifica dell'identità del servizio e del client\), la riservatezza \(crittografia del messaggio\) e l'integrità \(apposizione della firma digitale per il rilevamento di eventuali manomissioni\). L'autorizzazione rappresenta il controllo dell'accesso alle risorse che consente la lettura di un file, ad esempio, solo a utenti autorizzati. Se si usano le funzionalità di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], i due requisiti principali vengono implementati facilmente.  
  
 Ad eccezione della classe <xref:System.ServiceModel.BasicHttpBinding> \(o dell'elemento [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) nella configurazione\), la sicurezza del trasferimento è abilitata per impostazione predefinita per tutte le associazioni predefinite. Gli argomenti trattati in questa sezione interessano due scenari di base: implementazione della protezione del trasferimento e dell'autorizzazione in un servizio Intranet ospitato in IIS \(Internet Information Services\) e implementazione della protezione del trasferimento e dell'autorizzazione in un servizio ospitato in IIS.  
  
> [!NOTE]
>  Windows XP Home Edition non supporta l'autenticazione di Windows. Non eseguire quindi un servizio su questo sistema.  
  
## Nozioni di base sulla protezione  
 La protezione si basa su *credenziali*. Una credenziale prova che un'entità corrisponde a ciò che essa dichiara di essere. Un'*entità* può essere una persona, un processo software, una società o qualsiasi altra cosa che può essere autorizzata. Ad esempio, un client di un servizio fa un'*attestazione* di *identità* e la credenziale prova in qualche modo tale attestazione. In uno scenario tipico si verifica uno scambio di credenziali. Per prima cosa un servizio fa un'attestazione della propria identità e la prova al client con una credenziale. Viceversa, il client fa un'attestazione di identità e presenta una credenziale al servizio. Se entrambe le parti considerano attendibili le rispettive credenziali, potrà essere stabilito un *contesto protetto* nel quale tutti i messaggi vengono scambiati in riservatezza e vengono firmati per proteggerne l'integrità. Dopo che il servizio stabilisce l'identità del client, può associare le attestazioni nella credenziale a un *ruolo* o *appartenenza* in un gruppo. In ogni caso, usando il ruolo o il gruppo al quale appartiene il client, il servizio *autorizza* il client a eseguire un set limitato di operazioni basato sui privilegi del ruolo o del gruppo.  
  
## Meccanismi di sicurezza di Windows  
 Se il client e il computer del servizio sono entrambi in un dominio Windows che richiede a entrambi di accedere alla rete, le credenziali vengono fornite dall'infrastruttura di Windows. In tal caso, le credenziali vengono stabilite quando un utente del computer accede alla rete. Tutti gli utenti e tutti i computer sulla rete devono essere convalidati come appartenenti al set attendibile di utenti e computer. In un sistema Windows ogni utente e computer di questo insieme è anche noto come un'*entità di sicurezza*.  
  
 In un dominio Windows supportato da un controller *Kerberos*, il controller Kerberos usa uno schema basato sulla concessione di ticket a ogni entità di sicurezza. I ticket concessi dal controller sono ritenuti attendibili da altri servizi di concessione ticket presenti nel sistema. Ogni volta che un'entità tenta di eseguire un'operazione o accedere a una *risorsa* \(ad esempio un file o una directory in un computer\), il ticket viene esaminato per verificarne la validità. Se il ticket viene ritenuto valido, all'entità di sicurezza viene concesso un altro ticket per l'operazione. Questo metodo di concessione dei ticket risulta più efficiente rispetto al metodo alternativo che consiste nel tentare di convalidare l'entità di sicurezza per ogni operazione.  
  
 Un meccanismo superato e meno sicuro usato nei domini Windows è rappresentato da NT LAN Manager \(NTLM\). NTLM può rappresentare un'alternativa nei casi in cui non è possibile usare Kerberos \(in genere all'esterno di un dominio Windows, ad esempio un gruppo di lavoro\). NTLM è inoltre disponibile come un'opzione di sicurezza per IIS.  
  
 In un sistema Windows l'autorizzazione funziona assegnando ogni computer e ogni utente a un set di ruoli e gruppi. Ogni computer Windows, ad esempio, deve essere configurato e controllato da una persona \(o gruppo di persone\) a cui è assegnato il ruolo di *amministratore*. Un altro ruolo è quello di *utente*, che ha un set di autorizzazioni molto più limitato. Oltre che a ruoli, gli utenti vengono assegnati a gruppi. Un gruppo consente a più utenti di svolgere lo stesso ruolo. In pratica, quindi, un computer Windows viene amministrato assegnando utenti a gruppi. Ad esempio, più utenti possono essere assegnati al gruppo di utenti di un computer e un set molto più limitato di utenti può essere assegnato al gruppo di amministratori. In un computer locale un amministratore può anche creare nuovi gruppi e assegnarvi altri utenti \(o altri gruppi\).  
  
 In un computer che esegue Windows ogni cartella inclusa in una directory può essere protetta. In altri termini, è possibile selezionare una cartella e controllare quali utenti possono accedere ai file e se possono copiare un file o \(nel caso dispongano di maggiori autorizzazioni\) modificarli, eliminarli o aggiungerli alla cartella. Questo processo è noto come controllo di accesso e il meccanismo correlato è noto come elenco di controllo di accesso \(ACL\). Quando si crea l'ACL, è possibile assegnare privilegi di accesso a qualsiasi gruppo, nonché a singoli membri di un dominio.  
  
 L'infrastruttura [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è progettata per usare questi meccanismi di sicurezza di Windows. Pertanto, se si sta creando un servizio che viene distribuito su una Intranet e i cui client sono limitati a membri del dominio Windows, la protezione viene implementata facilmente. Al dominio possono accedere soltanto utenti validi. Dopo che gli utenti hanno eseguito l'accesso, il controller Kerberos consente a ogni utente di stabilire contesti protetti con qualsiasi altro computer o applicazione. In un computer locale i gruppi possono essere creati facilmente e, quando la protezione viene applicata a cartelle specifiche, tali gruppi possono essere usati per assegnare privilegi di accesso nel computer.  
  
## Implementazione della protezione di Windows in servizi Intranet  
 Per proteggere un'applicazione che viene eseguita esclusivamente in un dominio Windows, è possibile usare le impostazioni di sicurezza predefinite dell'associazione <xref:System.ServiceModel.WSHttpBinding> o <xref:System.ServiceModel.NetTcpBinding>. Per impostazione predefinita, qualsiasi utente che si trova nello stesso dominio Windows può accedere ai servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Poiché hanno eseguito l'accesso alla rete, questi utenti sono ritenuti attendibili. I messaggi tra un servizio e un client vengono crittografati ai fini della riservatezza e firmati ai fini dell'integrità.[!INCLUDE[crabout](../../../includes/crabout-md.md)] come creare un servizio che usa la sicurezza di Windows, vedere [Procedura: proteggere un servizio con credenziali di Windows](../../../docs/framework/wcf/how-to-secure-a-service-with-windows-credentials.md).  
  
### Autorizzazione mediante la classe PrincipalPermissionAttribute  
 Se è necessario limitare l'accesso delle risorse in un computer, il modo più semplice è usare la classe <xref:System.Security.Permissions.PrincipalPermissionAttribute>. Questo attributo consente di limitare la chiamata a operazioni del servizio richiedendo che l'utente appartenga a un gruppo o ruolo di Windows specificato o che sia un utente specifico.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Procedura: limitare l'accesso tramite la classe PrincipalPermissionAttribute](../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md).  
  
### Rappresentazione  
 La rappresentazione è un altro meccanismo che è possibile usare per controllare l'accesso alle risorse. Per impostazione predefinita, un servizio ospitato da IIS viene eseguito con l'identità dell'account ASPNET. L'account ASPNET può accedere soltanto alle risorse per le quali dispone di autorizzazione. È tuttavia possibile impostare l'ACL in modo che una cartella escluda l'account del servizio ASPNET e consenta invece ad altre identità specifiche di accedere alla cartella. Il problema diventa quindi come consentire a questi utenti di accedere alla cartella se all'account ASPNET non è consentito. La soluzione è usare la rappresentazione, mediante la quale al servizio viene consentito di usare le credenziali del client per accedere a una determinata risorsa. Un altro esempio è l'accesso a un database SQL Server per il quale solo determinati utenti dispongono dell'autorizzazione.[!INCLUDE[crabout](../../../includes/crabout-md.md)]ll'uso della rappresentazione, vedere [Procedura: rappresentare un client in un servizio](../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md) e [Delega e rappresentazione](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md).  
  
## Protezione su Internet  
 La protezione su Internet ha gli stessi requisiti della protezione su una Intranet. Un servizio deve presentare le proprie credenziali per provare l'autenticità e i client devono provare la propria identità al servizio. Dopo che l'identità di un client è stata verificata, il servizio può controllare i privilegi di accesso del client alle risorse. A causa della natura eterogenea di Internet, tuttavia, le credenziali presentate differiscono da quelle usate in un dominio Windows. Mentre un controller Kerberos gestisce l'autenticazione di utenti in un dominio con ticket per credenziali, su Internet servizi e client si basano su uno di tanti modi diversi per presentare credenziali. L'obiettivo di questo argomento è comunque di presentare un approccio comune che consenta di creare un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] accessibile su Internet.  
  
### Uso di IIS e ASP.NET  
 I requisiti della protezione Internet e i meccanismi per risolvere questi problemi non sono nuovi. IIS è il server Web di Microsoft per Internet e ha molte funzionalità di sicurezza che risolvono questi problemi. [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] include inoltre funzionalità di sicurezza che possono essere usate dai servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Per sfruttare queste funzionalità di sicurezza, ospitare un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in IIS.  
  
#### Uso del provider di appartenenze e ruoli di ASP.NET  
 ASP.NET include un provider di appartenenze e ruoli. Il provider è un database di coppie nome utente\/password per l'autenticazione dei chiamanti che consente inoltre di specificare i privilegi di accesso di ogni chiamante. Con [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è possibile usare un provider di appartenenze e ruoli preesistente mediante la configurazione. Per un'applicazione di esempio che mostra l'uso di questo provider, vedere l'esempio [Provider di appartenenza e di ruoli](../../../docs/framework/wcf/samples/membership-and-role-provider.md).  
  
### Credenziali usate da IIS  
 Diversamente da un dominio Windows supportato da un controller Kerberos, Internet è un ambiente che non è dotato di un unico controller che gestisce i milioni di utenti che accedono alla rete in qualsiasi momento. Le credenziali usate su Internet, invece, sono in genere nella forma di certificati X.509 \(noti anche come certificati Secure Sockets Layer o SSL\). Questi certificati vengono emessi in genere da un'*autorità di certificazione* che può essere una società di terze parti che attesta l'autenticità del certificato e della persona alla quale è stato inviato. Per esporre il servizio su Internet è inoltre necessario fornire un certificato attendibile per autenticare il servizio.  
  
 La questione è dunque come ottenere un certificato di questo tipo. Un metodo consiste nel recarsi presso un'autorità di certificazione di terze parti, ad esempio Authenticode o VeriSign, quando si è pronti per distribuire il servizio e acquistare un certificato per il servizio. Se tuttavia si è nella fase di sviluppo con [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e non si è ancora pronti ad acquistare un certificato, sono disponibili strumenti e tecniche per la creazione di certificati X.509 che è possibile usare per simulare una distribuzione della produzione.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Utilizzo dei certificati](../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
## Modalità di sicurezza  
 La programmazione della protezione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] comporta alcune decisioni critiche. Una delle decisioni fondamentali è la scelta della *modalità di sicurezza*. Le due modalità di sicurezza principali sono la *modalità di sicurezza trasporto* e la *modalità di sicurezza messaggio*.  
  
 Una terza modalità, che combina la semantica di entrambe le modalità principali, è la *modalità di sicurezza trasporto con credenziali messaggio \(TransportwithMessageCredentials\)*.  
  
 La modalità di sicurezza determina il modo in cui vengono protetti i messaggi e ogni scelta presenta vantaggi e svantaggi, come spiegato di seguito.[!INCLUDE[crabout](../../../includes/crabout-md.md)]ll'impostazione della modalità di sicurezza, vedere [Procedura: impostare la modalità di sicurezza](../../../docs/framework/wcf/how-to-set-the-security-mode.md).  
  
#### Modalità di sicurezza trasporto  
 Tra la rete e l'applicazione esistono più livelli. Uno di questi è il *livello* di trasporto, che gestisce il trasferimento di messaggi tra endpoint. Ai fini del presente documento, è sufficiente comprendere che [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] usa più protocolli di trasporto, ognuno dei quali in grado di proteggere il trasferimento di messaggi.[!INCLUDE[crabout](../../../includes/crabout-md.md)]i trasporti, vedere [Trasporti](../../../docs/framework/wcf/feature-details/transports.md).  
  
 Due protocolli comunemente usati sono HTTP e TCP. Ognuno di questi protocolli può proteggere il trasferimento di messaggi mediante un meccanismo \(o meccanismi\) specifico del protocollo. Ad esempio, il protocollo HTTP viene protetto usando SSL su HTTP, comunemente abbreviato "HTTPS". Pertanto, quando si seleziona la modalità di sicurezza trasporto si sceglie di usare il meccanismo dettato dal protocollo. Ad esempio, se si seleziona la classe <xref:System.ServiceModel.WSHttpBinding> e si imposta la relativa modalità di sicurezza su Trasporto, come meccanismo di sicurezza si sta selezionando SSL su HTTP \(HTTPS\). Il vantaggio della modalità trasporto è la maggiore efficienza rispetto alla modalità messaggio. Ciò dipende dal fatto che la protezione viene integrata a un livello relativamente basso. Quando si usa la modalità trasporto, il meccanismo di sicurezza deve essere implementato in base alla specifica per il trasporto. I messaggi possono quindi fluire in modo protetto solo da punto a punto sul trasporto.  
  
#### Modalità di sicurezza messaggio  
 Contrariamente alla modalità trasporto, la modalità messaggio fornisce la protezione includendo i dati sulla protezione in ogni messaggio. Usando intestazioni di sicurezza XML e SOAP, le credenziali e altri dati necessari a garantire l'integrità e la riservatezza del messaggio vengono inclusi in ogni messaggio. Ogni messaggio include dati di sicurezza e ciò determina una riduzione delle prestazioni in quanto ogni messaggio deve essere elaborato individualmente. Nella modalità trasporto, quando il livello di trasporto è protetto, tutti i messaggi fluiscono liberamente. La modalità di sicurezza messaggio ha tuttavia il vantaggio di essere più flessibile rispetto alla modalità di sicurezza trasporto. Ciò significa che i requisiti di sicurezza non sono determinati dal trasporto. Per proteggere il messaggio è possibile usare qualsiasi tipo di credenziale client. Nella modalità trasporto il protocollo di trasporto determina il tipo di credenziale client che è possibile usare.  
  
#### Trasporto con credenziali messaggio  
 La terza modalità combina le caratteristiche migliori delle modalità trasporto e messaggio. In questa modalità la protezione del trasporto viene usata per garantire in modo efficiente la riservatezza e l'integrità di ogni messaggio. Allo stesso tempo ogni messaggio include i dati delle credenziali che consentono l'autenticazione del messaggio. Con l'autenticazione è possibile implementare anche l'autorizzazione. Mediante l'autenticazione di un mittente, l'accesso alle risorse può essere concesso \(o negato\) in base all'identità del mittente.  
  
## Specifica del tipo di credenziale client e del valore della credenziale  
 Dopo avere selezionato una modalità di sicurezza, è necessario specificare anche un tipo di credenziale client. Il tipo di credenziale client specifica il tipo che un client deve usare per l'autenticazione al server.  
  
 Non tutti gli scenari richiedono un tipo di credenziale client. Se si usa SSL su HTTP \(HTTPS\), un servizio esegue l'autenticazione al client. Come parte di questa autenticazione, il certificato del servizio viene inviato al client in un processo denominato *negoziazione*. Il trasporto protetto da SSL garantisce che tutti i messaggi siano riservati.  
  
 Se si sta creando un servizio che richiede che il client venga autenticato, la scelta di un tipo di credenziale client dipende dal trasporto e dalla modalità selezionati. Ad esempio, se si usa il trasporto HTTP e si sceglie la modalità Trasporto, è possibile scegliere tra più tipi di credenziale, ad esempio Di base, Digest e altri.[!INCLUDE[crabout](../../../includes/crabout-md.md)] questi tipi di credenziale, vedere [Informazioni sull'autenticazione HTTP](../../../docs/framework/wcf/feature-details/understanding-http-authentication.md).  
  
 Se si sta creando un servizio in un dominio Windows che sarà disponibile soltanto per altri utenti della rete, il tipo di credenziale client più facile da usare è quello di Windows. Può tuttavia essere necessario fornire un servizio con un certificato. A questo proposito, vedere [Procedura: specificare valori di credenziali client](../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
#### Valori della credenziale  
 Un *valore della credenziale* è la credenziale effettiva usata dal servizio. Una volta specificato un tipo di credenziale, può essere necessario configurare il servizio con le credenziali effettive. Se è stato selezionato Windows \(e il servizio verrà eseguito in un dominio Windows\), non è necessario specificare il valore effettivo di una credenziale.  
  
## Identità  
 In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] il termine *identità* ha significati diversi a seconda che si riferisca al server o al client. In breve, quando si esegue un servizio, dopo l'autenticazione viene assegnata un'identità al contesto di sicurezza. Per visualizzare l'identità effettiva, controllare le proprietà <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> e <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> della classe <xref:System.ServiceModel.ServiceSecurityContext>.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Procedura: esaminare il contesto di sicurezza](../../../docs/framework/wcf/how-to-examine-the-security-context.md).  
  
 Al contrario, sul client l'identità viene usata per convalidare il servizio. In fase di progettazione uno sviluppatore di client può impostare l'elemento [\<identità\>](../../../docs/framework/configure-apps/file-schema/wcf/identity.md) su un valore ottenuto dal servizio. In fase di esecuzione il client verifica il valore dell'elemento rispetto all'identità effettiva del servizio. Se il controllo ha un esito negativo, il client termina la comunicazione. Il valore può essere un nome di entità utente \(UPN\), se il servizio viene eseguito con l'identità di un utente specifico, o un nome di entità servizio \(SPN\), se il servizio viene eseguito con un account computer.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Identità del servizio e autenticazione](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md). La credenziale può anche essere un certificato o un campo presente in un certificato che identifica il certificato.  
  
## Livelli di sicurezza  
 La proprietà `ProtectionLevel` ricorre in più classi di attributi \(ad esempio, le classi <xref:System.ServiceModel.ServiceContractAttribute> e <xref:System.ServiceModel.OperationContractAttribute>\). Il livello di sicurezza è un valore che specifica se i messaggi \(o parti del messaggio\) che supportano un servizio sono firmati, firmati e crittografati o inviati senza firma né crittografia.[!INCLUDE[crabout](../../../includes/crabout-md.md)]lla proprietà, vedere [Informazioni sul livello di protezione](../../../docs/framework/wcf/understanding-protection-level.md). Per alcuni esempi di programmazione, vedere [Procedura: impostare la proprietà ProtectionLevel](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md).[!INCLUDE[crabout](../../../includes/crabout-md.md)]lla progettazione di un contratto di servizio con `ProtectionLevel` nel contesto, vedere [Progettazione dei contratti di servizio](../../../docs/framework/wcf/designing-service-contracts.md).  
  
## Vedere anche  
 <xref:System.ServiceModel>   
 <xref:System.ServiceModel.Description.ServiceCredentials>   
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 [Identità del servizio e autenticazione](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [Informazioni sul livello di protezione](../../../docs/framework/wcf/understanding-protection-level.md)   
 [Delega e rappresentazione](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)   
 [Progettazione dei contratti di servizio](../../../docs/framework/wcf/designing-service-contracts.md)   
 [Sicurezza](../../../docs/framework/wcf/feature-details/security.md)   
 [Cenni preliminari sulla sicurezza](../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Procedura: impostare la proprietà ProtectionLevel](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)   
 [Procedura: proteggere un servizio con credenziali di Windows](../../../docs/framework/wcf/how-to-secure-a-service-with-windows-credentials.md)   
 [Procedura: impostare la modalità di sicurezza](../../../docs/framework/wcf/how-to-set-the-security-mode.md)   
 [Procedura: specificare il tipo di credenziali client](../../../docs/framework/wcf/how-to-specify-the-client-credential-type.md)   
 [Procedura: limitare l'accesso tramite la classe PrincipalPermissionAttribute](../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)   
 [Procedura: rappresentare un client in un servizio](../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)   
 [Procedura: esaminare il contesto di sicurezza](../../../docs/framework/wcf/how-to-examine-the-security-context.md)