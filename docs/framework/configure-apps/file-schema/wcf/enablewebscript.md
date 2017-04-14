---
title: "&lt;enableWebScript&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9c7e96e1-af70-4e6e-ac5c-d67929dddbaa
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;enableWebScript&gt;
Questo elemento attiva il comportamento dell'endpoint che rende possibile l'uso del servizio da pagine Web ASP.NET AJAX.  
  
## Sintassi  
  
```  
  
<enableWebScript />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica l'insieme di comportamenti dell'endpoint.|  
  
## Note  
 Questo comportamento deve essere usato solo in combinazione con l'associazione standard [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) o con l'elemento di associazione [\<webMessageEncoding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webmessageencoding.md).  Per altre informazioni su questo comportamento, vedere <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.WebScriptEnablingElement>   
 <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>   
 [Integrazione AJAX e supporto JSON](../../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)   
 [\<webHttp\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md)