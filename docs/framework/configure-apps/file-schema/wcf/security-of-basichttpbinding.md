---
title: "&lt;security&gt; di &lt;basicHttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6432708d-5465-4bd9-bfc2-466742db99cb
caps.latest.revision: 16
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 16
---
# &lt;security&gt; di &lt;basicHttpBinding&gt;
Definisce le funzionalità di sicurezza di [\<basicHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md).  
  
## Sintassi  
  
```  
  
<security mode="Message/None/Transport/TransportWithCredential">  
   <transport  
      clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"  
      proxyCredentialType="Basic/Digest/None/Ntlm/Windows"  
      realm="string" />  
   <message  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
            clientCredentialType="Certificate/IssuedToken/None/UserName/Windows" />  
</security>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|modalità|Parametro facoltativo.  Specifica il tipo di sicurezza usata.  Il valore predefinito è `None`.  L'attributo è di tipo <xref:System.ServiceModel.BasicHttpSecurityMode>.|  
  
## Attributo mode  
  
|Valore|Descrizione|  
|------------|-----------------|  
|None|-   I messaggi non vengono protetti durante il trasferimento.|  
|Trasporto|La sicurezza è fornita mediante il trasporto HTTPS.  I messaggi SOAP sono protetti mediante HTTPS.  Il servizio viene autenticato sul client mediante il certificato X.509 del servizio.  Il client viene autenticato mediante il ClientCredentialType  fornito.  Vedere l'[\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-basichttpbinding.md).|  
|Messaggio|La sicurezza è fornita mediante la sicurezza dei messaggi SOAP.  Per impostazione predefinita, il corpo viene crittografato e firmato.  Per questa associazione, il sistema richiede che il certificato server sia fornito al client fuori banda.  L'unico valore `ClientCredentialType` valido per questa associazione è `Certificate`.|  
|TransportWithMessageCredential|Integrità, riservatezza e autenticazione server sono fornite dalla sicurezza del trasporto.  L'autenticazione del client è fornita per mezzo della sicurezza del messaggio SOAP.  Questa modalità è appropriata quando l'utente esegue l'autenticazione usando nome utente\/password in presenza di una distribuzione HTTP esistente per la sicurezza del trasferimento dei messaggi.|  
|TransportCredentialOnly|Questa modalità non fornisce l'integrità e la riservatezza dei messaggi,  Fornisce autenticazione client basata su HTTP.  Tale modalità deve essere usata con cautela.  In particolare, va usata in ambienti dove la sicurezza del trasporto viene fornita tramite altri mezzi \(ad esempio IPSec\) e l'infrastruttura [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] fornisce solo l'autenticazione client.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-basichttpbinding.md)|Definisce le impostazioni di sicurezza del trasporto per un servizio HTTP di base.  L'elemento corrisponde a <xref:System.ServiceModel.HttpTransportSecurity>.|  
|[\<messaggio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-basichttpbinding.md)|Definisce le impostazioni di sicurezza del messaggio per un servizio HTTP di base.  L'elemento corrisponde a <xref:System.ServiceModel.BasicHttpMessageSecurity>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|associazione|L'elemento di associazione di [\<basicHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)|  
  
## Note  
 Per impostazione predefinita, il messaggio SOAP non è protetto e il client non viene autenticato.  Questo elemento consente di configurare impostazioni di sicurezza aggiuntive per l'elemento `basicHttpBinding`.  
  
## Vedere anche  
 <xref:System.ServiceModel.BasicHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.BasicHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement>   
 <xref:System.ServiceModel.BasicHttpSecurity>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Selezione di un tipo di credenziale](../../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)