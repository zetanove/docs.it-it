---
title: "&lt;clientVia&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c27ee94e-babd-459b-9574-2a6d67d11314
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# &lt;clientVia&gt;
Specifica l'URI per il quale creare il canale del trasporto.  Per altre informazioni, vedere <xref:System.ServiceModel.Description.ClientViaBehavior>.  
  
## Sintassi  
  
```  
  
<clientVia viaUri="String"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`viaUri`|Stringa che specifica un Uri che indica la route che deve essere presa da un messaggio.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un comportamento dell'endpoint.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ClientViaElement>   
 <xref:System.ServiceModel.Description.ClientViaBehavior>