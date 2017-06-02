---
title: "Delega e rappresentazione con WCF | Microsoft Docs"
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
  - "rappresentazione [WCF]"
  - "delega [WCF]"
ms.assetid: 110e60f7-5b03-4b69-b667-31721b8e3152
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# Delega e rappresentazione con WCF
La *rappresentazione* è una tecnica comune utilizzata dai servizi per limitare l'accesso dei client alle risorse del dominio del servizio. Tali risorse possono essere risorse del computer, ad esempio file locali \(rappresentazione\), o risorse in un'altro computer, ad esempio una condivisione file \(delega\). Per un'applicazione di esempio, vedere [Rappresentazione di client](../../../../docs/framework/wcf/samples/impersonating-the-client.md). Per un esempio di come usare la rappresentazione, vedere [Procedura: rappresentare un client in un servizio](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md).  
  
> [!IMPORTANT]
>  Tenere presente che, in caso di rappresentazione di un client in un servizio, il servizio viene eseguito con le credenziali client, che potrebbero prevedere privilegi più elevati rispetto al processo server.  
  
## Panoramica  
 In genere, i client chiamano un servizio per l’esecuzione di determinate operazioni da parte del servizio stesso per loro conto. La rappresentazione consente al servizio di eseguire azioni per conto del client. La delega consente a un servizio front end di inoltrare le richieste del client ad un servizio back end in modo tale che quest'ultimo possa anche rappresentare il client. La rappresentazione, in genere, viene utilizzata per controllare se un client è autorizzato ad eseguire una particolare azione, mentre la delega è un modo per propagare ad un servizio back end le funzionalità della rappresentazione insieme all'identità del client. La delega è una funzionalità di dominio Windows che può essere utilizzata quando viene eseguita l'autenticazione basata su Kerberos. La delega si differenzia dal flusso dell'identità ed è un'operazione con privilegi maggiori in quanto trasferisce la possibilità di rappresentare il client senza il possesso della relativa password.  
  
 Sia la rappresentazione che la delega richiedono che il client abbia una identità di Windows. Se un client non possiede un'identità di Windows, l'unica opzione disponibile è propagare l'identità del client al secondo servizio.  
  
## Nozioni fondamentali sulla rappresentazione  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] supporta la rappresentazione per varie credenziali client. In questo argomento viene descritto il supporto del modello di servizio per la rappresentazione del chiamante durante l'implementazione di un metodo del servizio. Vengono inoltre descritti gli scenari di distribuzione più frequenti che riguardando la rappresentazione e la sicurezza SOAP, nonché le opzioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in tali scenari.  
  
 Questo argomento si incentra sulla rappresentazione e la delega in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in caso di utilizzo della sicurezza SOAP. È possibile usare la rappresentazione e la delega con [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] anche quando si usa la sicurezza del trasporto, come descritto in [Utilizzo della rappresentazione con la protezione del trasporto](../../../../docs/framework/wcf/feature-details/using-impersonation-with-transport-security.md).  
  
## Due metodi  
 La sicurezza SOAP in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] prevede due metodi distinti per eseguire la rappresentazione. Il metodo utilizzato dipende dall'associazione. Il primo consiste nella rappresentazione da un token di Windows ottenuto dall'autenticazione Security Support Provider Interface \(SSPI\) o Kerberos, che viene quindi memorizzato nella cache del servizio. Il secondo consiste nella rappresentazione da un token di Windows ottenuto dalle estensioni Kerberos, collettivamente denominate *Service\-for\-User* \(S4U\).  
  
### Rappresentazione con un token memorizzato nella cache  
 È possibile eseguire la rappresentazione con un token memorizzato nella cache con gli elementi seguenti:  
  
-   <xref:System.ServiceModel.WSHttpBinding>, <xref:System.ServiceModel.WSDualHttpBinding> e <xref:System.ServiceModel.NetTcpBinding> con una credenziale client di Windows.  
  
-   <xref:System.ServiceModel.BasicHttpBinding> con l'enumerazione <xref:System.ServiceModel.BasicHttpSecurityMode> impostata sulla credenziale <xref:System.ServiceModel.BasicHttpSecurityMode> o qualsiasi altra associazione standard in cui il client presenta una credenziale basata sul nome utente di cui il servizio può eseguire il mapping a un account di Windows valido.  
  
-   Qualsiasi <xref:System.ServiceModel.Channels.CustomBinding> che utilizza una credenziale client di Windows con la proprietà `requireCancellation` impostata su `true` \(tale proprietà è disponibile per le classi seguenti: <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters>, <xref:System.ServiceModel.Security.Tokens.SslSecurityTokenParameters> e <xref:System.ServiceModel.Security.Tokens.SspiSecurityTokenParameters>\). Se si utilizza una conversazione protetta sull'associazione, è necessario che abbia la proprietà `requireCancellation` impostata su `true`.  
  
-   Qualsiasi <xref:System.ServiceModel.Channels.CustomBinding> in cui il client presenta una credenziale basata sul nome utente. Se si utilizza una conversazione protetta sull'associazione, è necessario che abbia la proprietà `requireCancellation` impostata su `true`.  
  
### Rappresentazione basata su S4U.  
 È possibile eseguire la rappresentazione basata su S4U con gli elementi seguenti:  
  
-   <xref:System.ServiceModel.WSHttpBinding>, <xref:System.ServiceModel.WSDualHttpBinding> e <xref:System.ServiceModel.NetTcpBinding> con una credenziale client basata su certificato di cui il servizio può eseguire il mapping a un account di Windows valido.  
  
-   Qualsiasi <xref:System.ServiceModel.Channels.CustomBinding> che utilizza una credenziale client di Windows con la proprietà `requireCancellation` impostata su `false`  
  
-   Qualsiasi <xref:System.ServiceModel.Channels.CustomBinding> che utilizza una credenziale client di Windows o basata sul nome utente e una conversazione protetta con la proprietà `requireCancellation` impostata su `false`.  
  
 La misura in cui il servizio può eseguire la rappresentazione del client dipende dai privilegi di cui dispone l'account del servizio quando tenta la rappresentazione, dal tipo di rappresentazione utilizzato ed eventualmente dall'ambito di rappresentazione consentito dal client.  
  
> [!NOTE]
>  Quando il client e il servizio sono in esecuzione nello stesso computer e il client è in esecuzione con un account del sistema \(ad esempio `Local System` o `Network Service`\), il client non può essere rappresentato quando viene stabilita una sessione protetta con token del contesto di sicurezza con stato. Un'applicazione Windows Form o console viene in genere eseguita con l'account attualmente connesso e quindi l'account può essere rappresentato per impostazione predefinita. Tuttavia, quando il client è una pagina [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] ospitata in [!INCLUDE[iis601](../../../../includes/iis601-md.md)] o [!INCLUDE[iisver](../../../../includes/iisver-md.md)], il client viene eseguito con l'account `Network Service` per impostazione predefinita. Tutte le associazioni fornite dal sistema che supportano le sessioni protette utilizzano un token del contesto di sicurezza \(SCT\) senza stato per impostazione predefinita. Tuttavia, se il client è una pagina [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e si utilizzano sessioni protette con token SCT con stato, non è possibile eseguire la rappresentazione del client.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'uso di token SCT con stato in una sessione di sicurezza, vedere [Procedura: creare un token di contesto di sicurezza per una sessione sicura](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
## Rappresentazione in un metodo del servizio: modello dichiarativo  
 La maggior parte degli scenari di rappresentazione implicano l'esecuzione del metodo del servizio nel contesto del chiamante.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce una funzionalità di rappresentazione che semplifica questa operazione consentendo all'utente di specificare il requisito di rappresentazione nell'attributo <xref:System.ServiceModel.OperationBehaviorAttribute>. Ad esempio, nel codice seguente, l'infrastruttura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] rappresenta il chiamante prima di eseguire il metodo `Hello`. Qualsiasi tentativo di accedere a risorse native nel metodo `Hello` ha esito positivo solo se l'elenco di controllo di accesso \(ACL\) della risorsa consente al chiamante i privilegi di accesso. Per attivare la rappresentazione, impostare la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> su uno dei valori dell'enumerazione <xref:System.ServiceModel.ImpersonationOption>, ovvero <xref:System.ServiceModel.ImpersonationOption?displayProperty=fullName> o <xref:System.ServiceModel.ImpersonationOption?displayProperty=fullName>, come illustrato nell'esempio seguente.  
  
> [!NOTE]
>  Quando un servizio dispone di credenziali più elevate del client remoto, vengono utilizzate le credenziali del servizio se la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> è impostata su <xref:System.ServiceModel.ImpersonationOption>. In altri termini, se un utente con privilegi di basso livello fornisce le sue credenziali, un servizio con privilegi di livello più elevato esegue il metodo con le credenziali del servizio e può utilizzare risorse che l'utente con privilegi di basso livello non sarebbe altrimenti in grado di utilizzare.  
  
 [!code-csharp[c_ImpersonationAndDelegation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#1)]
 [!code-vb[c_ImpersonationAndDelegation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#1)]  
  
 L'infrastruttura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può rappresentare il chiamante solo se il chiamante viene autenticato con credenziali di cui è possibile eseguire il mapping a un account utente di Windows. Se il servizio è configurato per l'autenticazione con una credenziale di cui non è possibile eseguire il mapping a un account di Windows, il metodo del servizio non viene eseguito.  
  
> [!NOTE]
>  In [!INCLUDE[wxp](../../../../includes/wxp-md.md)], se viene creato un token SCT con stato, la rappresentazione ha esito negativo, generando <xref:System.InvalidOperationException>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md).  
  
## Rappresentazione in un metodo del servizio: modello imperativo  
 Talvolta, per funzionare, non è necessario che un chiamante rappresenti l'intero metodo del servizio, ma solo una parte. In questo caso, è possibile ottenere l'identità Windows del chiamante nel metodo del servizio ed eseguire la rappresentazione in modo imperativo. A tale scopo, utilizzare la proprietà <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> della classe <xref:System.ServiceModel.ServiceSecurityContext> per restituire un'istanza della classe <xref:System.Security.Principal.WindowsIdentity> e chiamare il metodo <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A> prima di utilizzare l'istanza.  
  
> [!NOTE]
>  Assicurarsi di usare l'istruzione [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]`Using` o l'istruzione C\# `using` per ripristinare automaticamente l'azione di rappresentazione. Se non si utilizza l'istruzione o se si utilizza un linguaggio di programmazione diverso da [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o C\#, accertarsi di ripristinare il livello di rappresentazione. In caso contrario, si stabilisce la base per attacchi Denial of service e di elevazione del privilegio.  
  
 [!code-csharp[c_ImpersonationAndDelegation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#2)]
 [!code-vb[c_ImpersonationAndDelegation#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#2)]  
  
## Rappresentazione per tutti i metodi del servizio  
 In alcuni casi, è necessario eseguire tutti i metodi di un servizio nel contesto del chiamante. Anziché attivare in modo esplicito questa funzionalità sulla base di ciascun metodo, utilizzare la classe <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>. Impostare la proprietà <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ImpersonateCallerForAllOperations%2A> su `true`, come illustrato nel codice seguente. La classe <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> viene recuperata dalle raccolte di comportamenti della classe <xref:System.ServiceModel.ServiceHost>. Si noti inoltre che anche la proprietà `Impersonation` della classe <xref:System.ServiceModel.OperationBehaviorAttribute> applicata a ogni metodo deve essere impostata su <xref:System.ServiceModel.ImpersonationOption> o <xref:System.ServiceModel.ImpersonationOption>.  
  
 [!code-csharp[c_ImpersonationAndDelegation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#3)]
 [!code-vb[c_ImpersonationAndDelegation#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#3)]  
  
 Nella tabella seguente viene descritto il comportamento di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per tutte le possibili combinazioni di `ImpersonationOption` e `ImpersonateCallerForAllServiceOperations`.  
  
|`ImpersonationOption`|`ImpersonateCallerForAllServiceOperations`|Comportamento|  
|---------------------------|------------------------------------------------|-------------------|  
|Obbligatorio|n\/d|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] rappresenta il chiamante|  
|Allowed|false|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non rappresenta il chiamante|  
|Allowed|true|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] rappresenta il chiamante|  
|NotAllowed|false|[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non rappresenta il chiamante|  
|NotAllowed|true|Non consentita \(verrà generata un'eccezione <xref:System.InvalidOperationException>\).|  
  
## Livello di rappresentazione ottenuto dalla rappresentazione con credenziali di Windows e con un token memorizzato nella cache  
 In alcuni scenari il client dispone di un controllo parziale sul livello di rappresentazione eseguito dal servizio quando si utilizza una credenziale client di Windows. Uno scenario si ha quando il client specifica un livello di rappresentazione anonimo, l'altro quando si esegue la rappresentazione con un token memorizzato nella cache. A tale scopo, impostare la proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> della classe <xref:System.ServiceModel.Security.WindowsClientCredential>, a cui si accede come proprietà della classe generica <xref:System.ServiceModel.ChannelFactory%601>.  
  
> [!NOTE]
>  Quando si specifica un livello di rappresentazione anonimo, il client accede al servizio in modo anonimo. Il servizio deve pertanto consentire gli accessi anonimi, indipendentemente dal fatto che venga eseguita o meno la rappresentazione.  
  
 Il client può specificare il livello di rappresentazione come <xref:System.Security.Principal.TokenImpersonationLevel>, <xref:System.Security.Principal.TokenImpersonationLevel>, <xref:System.Security.Principal.TokenImpersonationLevel> o <xref:System.Security.Principal.TokenImpersonationLevel>. Al livello specificato viene prodotto solo un token, come illustrato nel codice seguente.  
  
 [!code-csharp[c_ImpersonationAndDelegation#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_impersonationanddelegation/cs/source.cs#4)]
 [!code-vb[c_ImpersonationAndDelegation#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_impersonationanddelegation/vb/source.vb#4)]  
  
 Nella tabella seguente viene indicato il livello di rappresentazione ottenuto dal servizio in caso di rappresentazione da un token memorizzato nella cache.  
  
|Valore di `AllowedImpersonationLevel`|Il servizio dispone di `SeImpersonatePrivilege`|Servizio e client con funzionalità di delega|`ImpersonationLevel` con token memorizzato nella cache|  
|-------------------------------------------|-----------------------------------------------------|--------------------------------------------------|------------------------------------------------------------|  
|Anonymous|Sì|n\/d|Rappresentazione|  
|Anonymous|No|n\/d|Identification|  
|Identification|n\/d|n\/d|Identification|  
|Rappresentazione|Sì|n\/d|Rappresentazione|  
|Rappresentazione|No|n\/d|Identification|  
|Delegation|Sì|Sì|Delegation|  
|Delegation|Sì|No|Rappresentazione|  
|Delegation|No|n\/d|Identification|  
  
## Livello di rappresentazione ottenuto dalla rappresentazione con credenziali basate sul nome utente e con un token memorizzato nella cache  
 Passando al servizio il nome utente e la password, un client consente a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di accedere come tale utente, il che equivale a impostare la proprietà `AllowedImpersonationLevel` su <xref:System.Security.Principal.TokenImpersonationLevel> \(la proprietà `AllowedImpersonationLevel` è disponibile sulle classi <xref:System.ServiceModel.Security.WindowsClientCredential> e <xref:System.ServiceModel.Security.HttpDigestClientCredential>\). Nella tabella seguente viene indicato il livello di rappresentazione ottenuto quando il servizio riceve credenziali basate sul nome utente.  
  
|`AllowedImpersonationLevel`|Il servizio dispone di `SeImpersonatePrivilege`|Servizio e client con funzionalità di delega|`ImpersonationLevel` con token memorizzato nella cache|  
|---------------------------------|-----------------------------------------------------|--------------------------------------------------|------------------------------------------------------------|  
|n\/d|Sì|Sì|Delegation|  
|n\/d|Sì|No|Rappresentazione|  
|n\/d|No|n\/d|Identification|  
  
## Livello di rappresentazione ottenuto dalla rappresentazione basata su S4U  
  
|Il servizio dispone di `SeTcbPrivilege`|Il servizio dispone di `SeImpersonatePrivilege`|Servizio e client con funzionalità di delega|`ImpersonationLevel` con token memorizzato nella cache|  
|---------------------------------------------|-----------------------------------------------------|--------------------------------------------------|------------------------------------------------------------|  
|Sì|Sì|n\/d|Rappresentazione|  
|Sì|No|n\/d|Identification|  
|No|n\/d|n\/d|Identification|  
  
## Mapping di un certificato client a un account di Windows  
 È possibile effettuare l'autenticazione di un client a un servizio tramite un certificato e fare in modo che il servizio esegua il mapping del client a un account esistente tramite Active Directory. Nel codice XML seguente viene illustrato come configurare il servizio affinché esegua il mapping del certificato.  
  
```xml  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="MapToWindowsAccount">  
      <serviceCredentials>  
        <clientCertificate>  
          <authentication mapClientCertificateToWindowsAccount="true" />  
        </clientCertificate>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
 Nel codice seguente viene illustrato come configurare il servizio.  
  
```  
  
// Create a binding that sets a certificate as the client credential type.  
WSHttpBinding b = new WSHttpBinding();  
b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
// Create a service host that maps the certificate to a Windows account.  
Uri httpUri = new Uri("http://localhost/Calculator");  
ServiceHost sh = new ServiceHost(typeof(HelloService), httpUri);  
sh.Credentials.ClientCertificate.Authentication.MapClientCertificateToWindowsAccount = true;  
  
```  
  
## Delegation  
 Per delegare ad un servizio back end, è necessario che un servizio esegua l'autenticazione multifase Kerberos \(SSPI senza fallback NTLM\) o l'autenticazione Kerberos diretta ad un servizio back end utilizzando l'identità Windows del client. Per delegare ad un servizio back\-end, creare una classe <xref:System.ServiceModel.ChannelFactory%601> e un canale, quindi comunicare tramite il canale durante la rappresentazione del client. Con questo tipo di delega, la distanza con la quale deve essere posizionato il servizio back end dal servizio front end dipende dal livello di rappresentazione raggiunto dal servizio front end. Se il livello di rappresentazione è <xref:System.Security.Principal.TokenImpersonationLevel>, è necessario che i servizi front end e back end vengano eseguiti nello stesso computer. Se il livello di rappresentazione è <xref:System.Security.Principal.TokenImpersonationLevel>, i servizi front end e back end possono essere eseguiti in computer diversi o nello stesso computer. L'attivazione della rappresentazione a livello di delega richiede che, per consentire la delega, i criteri di dominio di Windows siano configurati. Per altre informazioni sulla configurazione di Active Directory per il supporto della delega, vedere la pagina sull'[abilitazione dell'autenticazione delegata](http://go.microsoft.com/fwlink/?LinkId=99690).  
  
> [!NOTE]
>  Se il client esegue l'autenticazione al servizio front end utilizzando un nome utente e una password corrispondenti a un account di Windows nel servizio back end, il servizio front end può autenticarsi al servizio back end riutilizzando il nome utente e la password del client. Questa è una forma di flusso di identità particolarmente utile in quanto il trasferimento del nome utente e della password al servizio back\-end consente a quest'ultimo di eseguire la rappresentazione, ma non costituisce una delega perché Kerberos non viene utilizzato. I controlli di Active Directory sulla delega non vengono applicati all'autenticazione del nome utente e della password.  
  
### Capacità di delega come funzione del livello di rappresentazione.  
  
|Livello di rappresentazione|Il servizio può eseguire la delega tra processi.|Il servizio può eseguire la delega tra computer.|  
|---------------------------------|------------------------------------------------------|------------------------------------------------------|  
|<xref:System.Security.Principal.TokenImpersonationLevel>|No|No|  
|<xref:System.Security.Principal.TokenImpersonationLevel>|Sì|No|  
|<xref:System.Security.Principal.TokenImpersonationLevel>|Sì|Sì|  
  
 Nell'esempio di codice riportato di seguito viene illustrato come utilizzare la delega.  
  
 [!code-csharp[c_delegation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_delegation/cs/source.cs#1)]
 [!code-vb[c_delegation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_delegation/vb/source.vb#1)]  
  
### Procedura: configurare un'applicazione per utilizzare una delega vincolata.  
 Prima di utilizzare una delega vincolata, è necessario che il mittente, il destinatario e il controller di dominio siano configurati per raggiungere tale obiettivo. La procedura riportata di seguito elenca i passaggi che consentono la delega vincolata. Per altre informazioni sulle differenze tra la delega e la delega vincolata, vedere la parte che descrive gli argomenti vincolati nella pagina sulle [estensioni Kerberos di Windows Server 2003](http://go.microsoft.com/fwlink/?LinkId=100194).  
  
1.  Nel controller di dominio, cancellare la casella di controllo **L'account è sensibile e non può essere delegato** selezionata per l'account nel quale viene eseguita l'applicazione del client.  
  
2.  Nel controller di dominio, selezionare la casella di controllo **L'account è attendibile per la delega** selezionata per l'account nel quale viene eseguita l'applicazione del client.  
  
3.  Nel controller di dominio, configurare il computer di livello intermedio in modo che sia attendibile per la delega facendo clic sull'opzione **Computer attendibili per la delega**.  
  
4.  Nel controller di dominio, configurare il computer di livello intermedio per l'utilizzo della delega vincolata facendo clic sull'opzione **Computer attendibili per la delega solo ai servizi specificati**.  
  
 Per ulteriori dettagli sulla configurazione della delega vincolata, vedere gli argomenti seguenti su MSDN:  
  
-   [Risoluzione dei problemi relativi alla delega Kerberos](http://go.microsoft.com/fwlink/?LinkId=36724)  
  
-   [Transizione del protocollo Kerberos e delega vincolata](http://go.microsoft.com/fwlink/?LinkId=36725)  
  
## Vedere anche  
 <xref:System.ServiceModel.OperationBehaviorAttribute>   
 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A>   
 <xref:System.ServiceModel.ImpersonationOption>   
 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A>   
 <xref:System.ServiceModel.ServiceSecurityContext>   
 <xref:System.Security.Principal.WindowsIdentity>   
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>   
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ImpersonateCallerForAllOperations%2A>   
 <xref:System.ServiceModel.ServiceHost>   
 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A>   
 <xref:System.ServiceModel.Security.WindowsClientCredential>   
 <xref:System.ServiceModel.ChannelFactory%601>   
 <xref:System.Security.Principal.TokenImpersonationLevel>   
 [Utilizzo della rappresentazione con la protezione del trasporto](../../../../docs/framework/wcf/feature-details/using-impersonation-with-transport-security.md)   
 [Rappresentazione di client](../../../../docs/framework/wcf/samples/impersonating-the-client.md)   
 [Procedura: rappresentare un client in un servizio](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)   
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)