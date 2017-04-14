---
title: "&lt;add&gt; di &lt;defaultPorts&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f162ce42-963b-4779-96a7-d6d8b4ea0d2f
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;add&gt; di &lt;defaultPorts&gt;
Endpoint di comunicazione predefinito sul quale l'applicazione client è in ascolto.  
  
## Sintassi  
  
```  
  
<useRequestHeadersForMetadataAddress>  
   <defaultPorts>  
      <add port="Integer" scheme="String" />  
   </defaultPorts>  
</useRequestHeadersForMetadataAddress>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|porta|Integer che specifica il numero della porta di comunicazione predefinita.|  
|scheme|Stringa che specifica il gruppo di impostazioni del protocollo associato a una porta di comunicazione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<defaultPorts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/defaultports.md)|Raccolta di porte predefinite in cui sono elencati gli endpoint di comunicazione predefiniti sui quali l'applicazione client è in ascolto.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.DefaultPortElement>