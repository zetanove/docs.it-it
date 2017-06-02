---
title: "&lt;secureConversationAuthentication&gt; di &lt;serviceCredential&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0bd3fac7-befd-4a45-ba51-c200b33be0fd
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# &lt;secureConversationAuthentication&gt; di &lt;serviceCredential&gt;
Specifica le impostazioni per un servizio di conversazione protetta.  
  
## Sintassi  
  
```  
  
<secureConversationAuthentication securityStateEncoderType="String" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`securityStateEncoderType`|Stringa che specifica il tipo di <xref:System.ServiceModel.Security.SecurityStateEncoder> da usare.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|Specifica la credenziale da usare nell'autenticazione del servizio e le impostazioni relative alla convalida delle credenziali client.|  
  
## Note  
 Usare questo elemento di configurazione per specificare un elenco di tipi di attestazione noti per la serializzazione dei cookie del token del contesto di sicurezza \(SCT, Security Context Token\), oltre a un codificatore per la codifica e la sicurezza delle informazioni sui cookie.  Per altre informazioni su SCT, vedere <xref:System.ServiceModel.Security.SecureConversationServiceCredential>.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.SecureConversationServiceElement>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.SecureConversationAuthentication%2A>   
 <xref:System.ServiceModel.Description.ServiceCredentials.SecureConversationAuthentication%2A>   
 <xref:System.ServiceModel.Security.SecureConversationServiceCredential>