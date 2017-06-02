---
title: "&lt;security&gt; di &lt;wsDualHttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 869c05e7-4ebe-467d-95ab-c8f8de4e6b9e
caps.latest.revision: 15
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 15
---
# &lt;security&gt; di &lt;wsDualHttpBinding&gt;
Definisce le funzionalità di sicurezza di [\<wsDualHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md).  
  
## Sintassi  
  
```  
  
<security mode="Message/None">  
   <message  
      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
      clientCredentialType="Certificate/IssuedToken/None/UserName/Windows"  
      negotiateServiceCredential="Boolean"/>  
</security>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|modalità|-   Parametro facoltativo.  Specifica il tipo di sicurezza applicata.  Il valore predefinito è `Message`.  L'attributo è di tipo <xref:System.ServiceModel.WSDualHttpSecurityMode>.|  
  
## Attributo mode  
  
|Valore|Descrizione|  
|------------|-----------------|  
|None|La sicurezza è disabilitata.|  
|Messaggio|La sicurezza è fornita mediante la sicurezza dei messaggi SOAP.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<messaggio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wsdualhttpbinding.md)|Definisce le impostazioni di sicurezza per il messaggio.  L'elemento è di tipo <xref:System.ServiceModel.MessageSecurityOverHttp>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione di [\<wsDualHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md).|  
  
## Note  
 Un'associazione duale espone l'indirizzo IP del client al servizio.  Nel client è necessario implementare un meccanismo di sicurezza in grado di garantire che il client si connetta solo a servizi ritenuti attendibili.  
  
## Vedere anche  
 <xref:System.ServiceModel.WSDualHttpSecurity>   
 <xref:System.ServiceModel.WsDualHttpBinding.Security%2A>   
 <xref:System.ServiceModel.Configuration.WsDualHttpBindingElement.Security%2A>   
 <xref:System.ServiceModel.Configuration.WsDualHttpSecurityElement>   
 <xref:System.ServiceModel.BasicHttpSecurity>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)