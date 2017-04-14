---
title: "&lt;webScriptEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 85cb5ecf-351b-45f3-aa29-aa2e4b64bcdd
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;webScriptEndpoint&gt;
Questo elemento di configurazione definisce un endpoint standard con un'associazione [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) fissa che determina l'aggiunta automatica del comportamento [\<enableWebScript\>](../../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md).  Usare questo endpoint per la scrittura di un servizio chiamato da un'applicazione AJAX ASP.NET.  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <webScriptEndpoint>   
          <standardEndpoint  
             webEndpointType=”String”/>        
       </webScriptEndpoint>   
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|webEndpointType|Stringa che specifica il tipo dell'endpoint.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Raccolta di endpoint standard rappresentati da endpoint predefiniti con una o più delle relative proprietà \(indirizzo, associazione, contratto\) fisse.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.WebScriptEndpoint>   
 <xref:System.ServiceModel.Configuration.WebScriptEndpointElement>