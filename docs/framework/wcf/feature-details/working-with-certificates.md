---
title: "Utilizzo dei certificati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "certificati [WCF]"
ms.assetid: 6ffb8682-8f07-4a45-afbb-8d2487e9dbc3
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Utilizzo dei certificati
Per programmare le funzionalità di sicurezza di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] in genere si utilizzano i certificati digitali X.509. In particolare, questi certificati vengono utilizzati per autenticare client e server nonché per crittografare e firmare digitalmente i messaggi.Questo argomento fornisce una breve descrizione delle funzionalità relative ai certificati digitali X.509 e illustra come utilizzarle in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Questo argomento contiene inoltre i collegamenti agli argomenti che trattano questi concetti in modo più dettagliato o che descrivono come eseguire attività comuni tramite l'utilizzo di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e dei certificati.  
  
 In breve, un certificato digitale è un componente dell'*infrastruttura a chiave pubblica* \(PKI, Public Key Infrastructure\). Questa infrastruttura è un sistema di certificati digitali, autorità di certificazione e altre autorità di registrazione che verificano e autenticano la validità di ogni parte coinvolta in una transazione elettronica basata sull'utilizzo di crittografia a chiave pubblica.Ogni certificato viene rilasciato da un'autorità di certificazione e presenta un set di campi che contengono determinati dati, ad esempio *soggetto* \(l'entità alla quale viene rilasciato il certificato\), date di validità \(la data di validità del certificato\), autorità emittente \(l'entità che ha emesso il certificato\) e chiave pubblica.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ognuna di queste proprietà viene elaborata come un'attestazione <xref:System.IdentityModel.Claims.Claim>. Esistono due tipi di attestazioni: di identità e di diritto.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] certificati X.509, vedere la pagina relativa ai [certificati di chiave pubblica X.509](http://go.microsoft.com/fwlink/?LinkId=209952)[!INCLUDE[crabout](../../../../includes/crabout-md.md)] attestazioni e sull'autorizzazione in WCF, vedere [Gestione di attestazioni e autorizzazioni con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] implementazione di un PKI, vedere la pagina relativa ai [servizi certificati di Windows Server 2008 R2](http://go.microsoft.com/fwlink/?LinkId=209949).  
  
 Una delle funzionalità principali di un certificato è consentire l'autenticazione dell'identità del proprietario del certificato presso altre entità.Un certificato contiene la *chiave pubblica* del proprietario mentre il proprietario conserva la chiave privata.La chiave pubblica può essere utilizzata per crittografare i messaggi inviati al proprietario del certificato.In quanto unico detentore della chiave privata, solo il proprietario è in grado di decrittografare questi messaggi.  
  
 I certificati devono essere rilasciati da un autorità di certificazione, che spesso è un'emittente di certificati di terze parti.Nei domini Windows è disponibile un'autorità di certificazione utilizzabile per rilasciare certificati ai computer appartenenti al dominio.  
  
## Visualizzazione dei certificati  
 Quando si utilizzano i certificati, spesso è necessario visualizzarli e analizzarne le proprietà.A tale scopo è possibile ricorrere allo snap\-in Microsoft Management Console \(MMC\), uno strumento di facile utilizzo.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: visualizzare certificati con lo snap\-in MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).  
  
## Archivi certificati  
 I certificati vengono memorizzati in appositi archivi.Sono disponibili due posizioni principali di archiviazione, ognuna delle quali è composta da più sottoarchivi.Gli amministratori di un computer possono visualizzare entrambi gli archivi principali mediante lo snap\-in MMC.Gli altri utenti, invece, sono in grado di visualizzare soltanto l'archivio utente corrente.  
  
-   **Archivio locale del computer**:contiene i certificati utilizzati dai processi del computer, ad esempio [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].Utilizzare questa posizione per archiviare i certificati utilizzati per l'autenticazione del server presso i client.  
  
-   **Archivio dell'utente corrente**:questa posizione in genere viene utilizzata dalle applicazioni interattive per memorizzare i certificati relativi all'utente corrente del computer.Se si crea un'applicazione client, utilizzare questa posizione per archiviare i certificati utilizzati per l'autenticazione degli utenti presso un servizio.  
  
 Ognuno di questi due archivi è composto da più sottoarchivi.Segue l'elenco di alcuni dei sottoarchivi più importanti quando si programma in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   **Autorità di certificazione radice attendibili**:i certificati contenuti in questo archivio possono essere utilizzati per creare una catena di certificati che consente di risalire a un certificato di autorità di certificazione di questo archivio.  
  
    > [!IMPORTANT]
    >  Il computer locale considera implicitamente attendibile qualsiasi certificato memorizzato in questo archivio, anche se il certificato non è stato rilasciato da un autorità di certificazione di terze parti attendibile.È pertanto necessario garantire che questo archivio contenga soltanto certificati rilasciati da emittenti completamente attendibili, nonché comprendere quali problemi possono verificarsi qualora questa indicazione non venga rispettata.  
  
-   **Personale**:questo archivio viene utilizzato per i certificati associati a un utente di un computer.In genere questo archivio viene utilizzato per memorizzare i certificati rilasciati mediante uno dei certificati di autorità di certificazione contenuti nell'archivio Autorità di certificazione radice attendibili.In alternativa, questo archivio può contenere certificati autocertificati ritenuti attendibili da un'applicazione.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]gli archivi certificati, vedere il [documento relativo agli archivi certificati](http://go.microsoft.com/fwlink/?LinkId=88912).  
  
### Scelta di un archivio  
 La scelta della posizione in cui archiviare un certificato dipende dalla modalità di esecuzione del servizio o del client.In particolare, la scelta si basa sulle regole di carattere generale seguenti:  
  
-   Se il servizio WCF è ospitato in un servizio Windows utilizzare l'archivio del **computer locale**.Si noti che per memorizzare certificati in questo archivio è necessario disporre dei privilegi di amministratore.  
  
-   Se il servizio o il client si trova in un'applicazione in esecuzione in un account utente, utilizzare l'archivio **utente corrente**.  
  
### Accesso agli archivi  
 Analogamente alle cartelle di un computer, anche gli archivi vengono protetti tramite gli elenchi di controllo di accesso \(ACL, Access Control List\).Quando si crea un servizio ospitato in Internet Information Services \(IIS\), il processo [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] è in esecuzione nell'account [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].Tale account deve essere autorizzato ad accedere all'archivio contenente i certificati utilizzati da un servizio.Ogni archivio principale viene protetto mediante un ACL predefinito, che tuttavia può essere modificato.Se si crea un ruolo a parte per accedere a un archivio, a tale ruolo è necessario concedere l'autorizzazione di accesso.Per informazioni su come modificare l'ACL mediante lo strumento WinHttpCertConfig.exe, vedere [Procedura: creare certificati temporanei da usare durante lo sviluppo](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] utilizzo di certificati client in IIS, vedere la pagina relativa alla [procedura per chiamare un servizio Web utilizzando un certificato client per l'autenticazione in un'applicazione Web ASP.NET](http://go.microsoft.com/fwlink/?LinkId=88914).  
  
## Catena di trust e autorità di certificazione  
 I certificati vengono creati in una gerarchia dove ogni singolo certificato è collegato alla CA che ha emesso il certificato.Questo collegamento è per il certificato della CA.Il certificato della CA collega quindi la CA che ha emesso il certificato della CA originale.Questo processo si ripete fino a raggiungere il certificato della CA radice.Il certificato della CA radice è considerato naturalmente attendibile.  
  
 I certificati digitali vengono utilizzati per autenticare un'entità basandosi su una *catena di trust*.Lo snap\-in MMC consente di visualizzare la catena di qualsiasi certificato. A tale scopo, fare doppio clic sul certificato desiderato e quindi sulla scheda **Percorso certificato**.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] importazione di catene di certificati per un'autorità di certificazione, vedere [Procedura: specificare la catena di certificati di autorità di certificazione utilizzata per verificare le firme](../../../../docs/framework/wcf/feature-details/specify-the-certificate-authority-chain-verify-signatures-wcf.md).  
  
> [!NOTE]
>  Qualsiasi emittente può essere definito come un'autorità radice attendibile. A tale scopo, aggiungere il certificato di tale emittente nell'archivio Autorità di certificazione radice attendibili.  
  
### Disabilitazione della catena di trust  
 Quando si crea un nuovo servizio è possibile che si utilizzi un certificato che non è stato rilasciato tramite un certificato radice attendibile oppure che il certificato emittente non sia contenuto nell'archivio Autorità di certificazione radice attendibili.In questo caso, e solo per scopi di sviluppo, è possibile disabilitare temporaneamente il meccanismo che verifica la catena di trust di un certificato.A tale scopo, impostare la proprietà `CertificateValidationMode` su `PeerTrust` oppure su `PeerOrChainTrust`.Queste modalità specificano rispettivamente che il certificato può essere autocertificato \(trust peer\) o appartenere a una catena di trust.Questa proprietà può essere impostata in una qualsiasi delle classi seguenti:  
  
|Classe|Proprietà|  
|------------|---------------|  
|<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>|<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>|<xref:System.ServiceModel.Security.X509PeerCertificateAuthentication.CertificateValidationMode%2A?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>|<xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.IssuedTokenServiceCredential>|<xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A?displayProperty=fullName>|  
  
 La proprietà può anche essere impostata in configurazione.Gli elementi seguenti vengono utilizzati per specificare la modalità di convalida:  
  
-   [\<autenticazione\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)  
  
-   [\<autenticazionePeer\>](../../../../docs/framework/configure-apps/file-schema/wcf/peerauthentication-element.md)  
  
-   [\<autenticazioneMittenteMessaggio\>](../../../../docs/framework/configure-apps/file-schema/wcf/messagesenderauthentication-element.md)  
  
## Autenticazione personalizzata  
 La proprietà `CertificateValidationMode` consente inoltre di personalizzare la modalità di autenticazione dei certificati.Per impostazione predefinita, il livello è impostato su `ChainTrust`.Per utilizzare il valore <xref:System.ServiceModel.Security.X509CertificateValidationMode> è necessario impostare anche l'attributo `CustomCertificateValidatorType` sull'assembly e sul tipo utilizzati per convalidare il certificato.Per creare un validator personalizzato è necessario ereditare una classe dalla classe astratta <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  
  
 Quando si crea un autenticatore personalizzato è fondamentale eseguire l'override del metodo <xref:System.IdentityModel.Selectors.X509CertificateValidator.Validate%2A>.Per un esempio di autenticazione personalizzata, vedere l'esempio [Validator del certificato X.509](../../../../docs/framework/wcf/samples/x-509-certificate-validator.md).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Credenziale personalizzata e convalida della credenziale](../../../../docs/framework/wcf/extending/custom-credential-and-credential-validation.md).  
  
## Utilizzo dello strumento Makecert.exe per compilare una catena di certificati  
 Lo strumento di creazione dei certificati Makecert.exe crea certificati X.509 e coppie di chiavi privata\/pubblica.La chiave privata può essere salvata su disco e quindi utilizzata per rilasciare e firmare nuovi certificati, simulando in questo modo una gerarchia di certificati concatenati.Questo strumento deve essere utilizzato esclusivamente come risorsa ausiliare durante la fase di sviluppo dei servizi. È pertanto necessario evitare di utilizzarlo per creare i certificati da utilizzare nella distribuzione definitiva.Quando si sviluppa un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], attenersi ai passaggi seguenti per compilare una catena di trust tramite lo strumento Makecert.exe.  
  
#### Per compilare una catena di trust tramite lo strumento Makecert.exe  
  
1.  Utilizzare lo strumento MakeCert.exe per creare un certificato temporaneo dell'autorità radice \(autofirmato\).Salvare la chiave privata su disco.  
  
2.  Utilizzare il nuovo certificato per rilasciare un altro certificato contenente la chiave pubblica.  
  
3.  Importare il certificato dell'autorità radice nell'archivio Autorità di certificazione radice attendibili.  
  
4.  Per istruzioni dettagliate, vedere [Procedura: creare certificati temporanei da usare durante lo sviluppo](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md).  
  
## Scelta del certificato da utilizzare  
 Quando si utilizzano i certificati spesso sorgono dubbi su quale certificato scegliere e sul motivo per cui sceglierlo.La soluzione a questi dubbi varia a seconda che la programmazione riguardi un client o un servizio.Le informazioni seguenti rappresentano una linea guida generale e non forniscono una risposta esauriente a questi dubbi.  
  
### Certificati di servizio  
 Lo scopo principale dei certificati di servizio è autenticare il server presso i client.Uno dei primi controlli svolti durante l'autenticazione di un server presso un client consiste nel confrontare il valore del campo **Soggetto** con l'Uniform Resource Identifier \(URI\) utilizzato per contattare il servizio. In particolare, è necessario che i DNS di entrambi corrispondano fra loro.Ad esempio, se l'URI del servizio è "http:\/\/www.contoso.com\/endpoint\/", anche il campo **Soggetto** deve contenere il valore "www.contoso.com."  
  
 Si noti che il campo può contenere più valori, ognuno avente un prefisso iniziale che ne indica il valore.Nella maggior parte dei casi viene utilizzato il prefisso iniziale "CN" per indicare un nome comune. Ad esempio, "CN \= www.contoso.com".È inoltre possibile che il campo **Soggetto** sia vuoto. In tal caso, il campo **Nome alternativo soggetto** può contenere il valore **Nome DNS**.  
  
 Si noti inoltre che il valore del campo **Scopi designati** del certificato deve includere un valore appropriato, ad esempio "Autenticazione server" o "Autenticazione client".  
  
### Certificati client  
 Anziché essere rilasciati da un'autorità di certificazione di terze parti,in genere i certificati client vengono memorizzati da un'autorità radice nell'archivio Personale dell'utente corrente. Il campo Scopi designati in questo caso viene impostato su "Autenticazione client".Un client può utilizzare un certificato client quando è necessario eseguire l'autenticazione reciproca.  
  
## Revoca online e revoca offline  
  
### Validità del certificato  
 Ogni certificato è valido solo per un determinato periodo di tempo, detto *periodo di validità*.Il periodo di validità è definito in base ai campi **Valido dal** e **Valido fino al** di un certificato X.509.Durante l'autenticazione questi due campi vengono verificati per stabilire se il certificato è nel periodo di validità.  
  
### Elenco di revoche di certificati \(CRL, Certificate Revocation List\)  
 Durante il periodo di validità, l'autorità di certificazione può revocare un certificato in qualsiasi momento.Ciò può verificarsi per vari motivi, ad esempio se la chiave privata del certificato viene compromessa.  
  
 In questo caso, tutti i certificati appartenenti alle catene di trust aventi origine dal certificato revocato sono anch'essi considerati non validi e durante le procedure di autenticazione vengono considerati non attendibili.Per determinare quali certificati sono stati revocati, ogni emittente pubblica un *elenco di revoche di certificati* \(CRL, Certificate Revocation List\) dotato di timestamp e datestamp.Questo elenco può essere controllato tramite la revoca online oppure la revoca offline impostando la proprietà `RevocationMode` o la proprietà `DefaultRevocationMode` delle classi seguenti su uno dei valori dell'enumerazione <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>: <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>, <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>, <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> e <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>.Il valore predefinito di tutte le proprietà è `Online`.  
  
 La modalità può inoltre essere impostata nella configurazione tramite l'attributo `revocationMode` sia dell'[\<authentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md) \(della [\<comportamentiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)\) sia dell'[\<authentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md) \(della [\<comportamentiEndpoint\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md)\).  
  
## Metodo SetCertificate  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] spesso occorre specificare un certificato o un set di certificati che un servizio o un client deve utilizzare per autenticare, crittografare o firmare digitalmente un messaggio.Questa operazione può essere eseguita a livello di programmazione mediante il metodo `SetCertificate` di varie classi che rappresentano i certificati X.509.Le classi seguenti utilizzano il metodo `SetCertificate` per specificare un certificato.  
  
|Classe|Metodo|  
|------------|------------|  
|<xref:System.ServiceModel.Security.PeerCredential>|<xref:System.ServiceModel.Security.PeerCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>|<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>|<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.SetCertificate%2A>|  
  
 Il metodo `SetCertificate` si basa sulla definizione di una posizione di archivio, di un archivio, di un tipo "di ricerca" \(ovvero il parametro `x509FindType`\) che specifica un campo del certificato e un valore da ricercare nel campo.Ad esempio, nel codice seguente viene creata un'istanza della classe <xref:System.ServiceModel.ServiceHost> e viene utilizzato il metodo `SetCertificate` per impostare il certificato del servizio utilizzato per autenticare il servizio presso i client.  
  
 [!code-csharp[c_WorkingWithCertificates#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_workingwithcertificates/cs/source.cs#1)]
 [!code-vb[c_WorkingWithCertificates#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_workingwithcertificates/vb/source.vb#1)]  
  
### Certificati aventi lo stesso valore  
 Un archivio può contenere più certificati aventi lo stesso nome del soggetto.Ciò significa che se si imposta il tipo `x509FindType` su <xref:System.Security.Cryptography.X509Certificates.X509FindType> o <xref:System.Security.Cryptography.X509Certificates.X509FindType> e più certificati dispongono dello stesso valore, viene generata un'eccezione. Infatti, nonesistealcun modoper distinguere quale certificato è richiesto.Per risolvere questo problema, impostare la proprietà `x509FindType` su <xref:System.Security.Cryptography.X509Certificates.X509FindType>.Il campo dell'identificazione personale \("Thumbprint"\) contiene infatti un valore univoco che può essere utilizzato per individuare un certificato specifico all'interno di un archivio.Tuttavia, ciò comporta uno svantaggio: se il certificato viene revocato o rinnovato, il metodo `SetCertificate` ha esito negativo poiché in questi casi l'identificazione personale viene rispettivamente eliminata o alterata.Oppure, se il certificato non è più valido, l'autenticazione ha esito negativo.Per risolvere questo problema è possibile impostare il parametro `x590FindType` su <xref:System.Security.Cryptography.X509Certificates.X509FindType> e specificare quindi nome dell'emittente.Se non è richiesto alcun emittente specifico, è anche possibile impostare uno degli altri valori dell'enumerazione <xref:System.Security.Cryptography.X509Certificates.X509FindType>, ad esempio <xref:System.Security.Cryptography.X509Certificates.X509FindType>.  
  
## Impostazione dei certificati in configurazione  
 I certificati possono anche essere impostati in configurazione.Se si crea un servizio, le credenziali, compresi i certificati, vengono specificate nella [\<comportamentiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md).Quando si programma un client, i certificati vengono specificati nella [\<comportamentiEndpoint\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md).  
  
## Mapping di un certificato a un account utente  
 Una funzionalità di IIS e di Active Directory è la possibilità di eseguire il mapping di un certificato a un account utente di Windows.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] funzionalità, vedere la pagina relativa al [mapping dei certificati agli account utente](http://go.microsoft.com/fwlink/?LinkId=88917).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] utilizzo della funzionalità di mapping di Active Directory, vedere [Mapping di certificati client con il mapping del servizio directory](http://go.microsoft.com/fwlink/?LinkId=88918).  
  
 Se questa funzionalità è abilitata è possibile impostare la proprietà <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.MapClientCertificateToWindowsAccount%2A> della classe <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> su `true`.In configurazione è possibile impostare l'attributo `mapClientCertificateToWindowsAccount` dell'elemento [\<autenticazione\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) su `true`, come mostrato nel codice seguente.  
  
```  
<serviceBehaviors>  
 <behavior name="MappingBehavior">  
  <serviceCredentials>  
   <clientCertificate>  
    <authentication certificateValidationMode="None" mapClientCertificateToWindowsAccount="true" />  
   </clientCertificate>  
  </serviceCredentials>  
 </behavior>  
</serviceBehaviors>  
```  
  
 L'esecuzione del mapping di un certificato X.509 al token che rappresenta un account utente di Windows è considerata un'elevazione dei privilegi perché, una volta eseguito tale mapping, il token di Windows può essere utilizzato per accedere alle risorse protette.Pertanto, il criterio del dominio richiede che il certificato X.509 sia conforme al proprio criterio prima di eseguire il mapping.Il pacchetto di sicurezza *SChannel* applica questo requisito.  
  
 Quando si utilizza [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] o versioni successive, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] garantisce che il certificato sia conforme al criterio di dominio prima che venga mappato a un account di Windows.  
  
 Nella prima versione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] il mapping viene eseguito senza prendere in considerazione il criterio del dominio.È pertanto possibile che le applicazioni che funzionano correttamente con la prima versione presentano problemi se il mapping viene abilitato e il certificato X.509 non soddisfa il criterio del dominio.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels>   
 <xref:System.ServiceModel.Security>   
 <xref:System.ServiceModel>   
 <xref:System.Security.Cryptography.X509Certificates.X509FindType>   
 [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)