---
title: "&lt;webHttpEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ecaaeb6f-ebd0-411d-8b53-92477cd45347
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;webHttpEndpoint&gt;
Questo elemento di configurazione definisce un endpoint standard con un'associazione [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) fissa che determina l'aggiunta automatica del comportamento [\<webHttp\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md).  Usare questo endpoint per la scrittura di un servizio REST.  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <webHttpEndpoint>   
          <standardEndpoint  
             automaticFormatSelectionEnabled="String"   
             defaultOutgoingResponseFormat=”Xml/Json”  
             helpEnabled=”Boolean”  
             webEndpointType=”String”/>        
       </webHttpEndpoint>   
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|automaticFormatSelectionEnabled|Valore booleano che indica se la selezione automatica del formato è abilitata.<br /><br /> Quando la selezione automatica del formato è abilitata, l'infrastruttura analizza l'intestazione `Accept` del messaggio di richiesta e determina il formato appropriato per la risposta.  Se l'intestazione `Accept` non specifica un formato adatto per la risposta, l'infrastruttura usa il `Content-Type` del messaggio di richiesta o il formato della risposta predefinito dell'operazione.|  
|defaultOutgoingResponseFormat|Attributo che specifica il formato predefinito per la risposta in uscita.  L'attributo è di tipo <xref:System.Servicemodel.Web.Webmessageformat>.|  
|helpEnabled|Valore booleano che indica se la Guida HTTP è abilitata per l'endpoint.|  
|webEndpointType|Stringa che specifica il tipo dell'endpoint.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Raccolta di endpoint standard rappresentati da endpoint predefiniti con una o più delle relative proprietà \(indirizzo, associazione, contratto\) fisse.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.WebHttpEndpoint>   
 <xref:System.ServiceModel.Configuration.WebHttpEndpointElement>