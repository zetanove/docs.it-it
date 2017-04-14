---
title: "&lt;security&gt; di &lt;netMsmqBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 001d11a9-7439-498c-b09d-fca20eaf8cd3
caps.latest.revision: 15
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 15
---
# &lt;security&gt; di &lt;netMsmqBinding&gt;
Definisce le impostazioni di sicurezza per un'associazione MSMQ.  e specifica se è stata abilitata la sicurezza basata sul trasporto o la sicurezza SOAP. In tal caso, indica la modalità di autenticazione e i livelli di protezione in uso.  
  
## Sintassi  
  
```  
  
<security mode="None/Transport/Message/Both">  
   <transport msmqAuthenticationMode="None/WindowsDomain/Certificate"  
      msmqEncryptionAlgorithm="RC4Stream/AES"  
      msmqProtectionLevel="None/Sign/EncryptAndSign"  
      msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
      <message  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
      clientCredentialType="None/Windows/UserName/Certificate/CardSpace"/>  
</security>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|modalità|Specifica il tipo di sicurezza che controlla integrità, riservatezza e autenticazione.  Di seguito vengono elencati i valori validi:<br /><br /> -   None: disabilita la sicurezza.<br />-   Transport: sicurezza e autenticazione sono offerte dal trasporto.  Si applica alla sicurezza del messaggio tra i due gestori delle code.  Tra l'applicazione e il gestore della coda non viene offerta alcuna sicurezza.  Le applicazioni Msmq esistenti sono funzionalmente equivalenti con questo tipo di modalità di sicurezza.<br />-   Message: specifica la sicurezza completa dell'applicazione.  A livello del trasporto non viene offerta alcuna sicurezza.  È simile alla sicurezza offerta da altre associazioni standard.<br />-   Both: offre sicurezza sia a livello di trasporto che di messaggistica SOAP.  A entrambi i livelli è richiesta la stessa credenziale.<br /><br /> L'impostazione predefinita è Transport.  L'attributo è di tipo <xref:System.ServiceModel.NetMsmqSecurityMode>.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<messaggio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-netmsmqbinding.md)|Definisce le impostazioni di sicurezza per il messaggio SOAP.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.MessageSecurityOverMsmqElement>.|  
|[\<transport\>](../../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-netmsmqbinding.md)|Definisce le impostazioni di sicurezza per il trasporto MSMQ.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|associazione|L'elemento di associazione di [\<netMsmqBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md)|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.NetMsmqSecurityElement>   
 <xref:System.ServiceModel.NetMsmqBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.NetMsmqBindingElement.Security%2A>   
 <xref:System.ServiceModel.NetMsmqSecurity>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)   
 [Code in WCF](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)