---
title: "&lt;defaultPorts&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 725d4ee5-bd46-4f0e-9c20-30ba75d6eb2c
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;defaultPorts&gt;
Raccolta di porte predefinite in cui sono elencati gli endpoint di comunicazione predefiniti sui quali l'applicazione client è in ascolto.  
  
## Sintassi  
  
```  
  
<useRequestHeadersForMetadataAddress>  
   <defaultPorts>  
      <add scheme="http" port="integer" />  
   </defaultPorts>  
</useRequestHeadersForMetadataAddress>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<add\> di \<defaultPorts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-defaultports.md)|Endpoint di comunicazione predefinito sul quale l'applicazione client è in ascolto.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<useRequestHeadersForMetadataAddress\>](../../../../../docs/framework/configure-apps/file-schema/wcf/userequestheadersformetadataaddress.md)|Elenco di porte predefinite.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.DefaultPortElementCollection>