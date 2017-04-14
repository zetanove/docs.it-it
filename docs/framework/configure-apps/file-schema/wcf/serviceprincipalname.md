---
title: "&lt;servicePrincipalName&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f3b85d3-20f2-4cd8-8a6a-ee18befbd165
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;servicePrincipalName&gt;
Specifica l'identità di un servizio in base al relativo nome dell'entità servizio \(SPN, Service Principal Name\).  
  
 Per altre informazioni sull'impostazione del nome SPN, vedere [Identità del servizio e autenticazione](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md).  
  
## Sintassi  
  
```  
  
<servicePrincipalName value = "String" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|predefinito|Nome in base al quale un client identifica in modo univoco un'istanza di un servizio.  Se si installano più istanze di un servizio in computer distribuiti in una foresta, a ogni istanza deve essere associato un nome SPN distinto.  Se i client possono usare più nomi per l'autenticazione, una determinata istanza di servizio può presentare più SPN.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identità\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Specifica l'identità del servizio da autenticare presso il client.|  
  
## Note  
 Un client [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] protetto che si connette a un endpoint con questa identità usa l'SPN quando esegue l'autenticazione SSPI con l'endpoint.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.IdentityElement>   
 <xref:System.ServiceModel.EndpointAddress>   
 <xref:System.ServiceModel.EndpointAddress.Identity%2A>   
 <xref:System.ServiceModel.SpnEndpointIdentity>   
 [Identità del servizio e autenticazione](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [\<identità\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)