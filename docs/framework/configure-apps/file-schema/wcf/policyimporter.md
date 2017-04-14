---
title: "&lt;policyImporter&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b0d03456-546f-44bb-ab12-1b2ce7f98fca
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;policyImporter&gt;
Specifica un'unità di importazione dei criteri che controlla l'importazione di asserzioni di criteri personalizzati sulle associazioni.  
  
## Sintassi  
  
```  
  
<metadata>  
   <policyImporters>  
      <policyImporter type="string" />  
   </policyImporters>  
</metadata>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`type`|Tipo di questo elemento.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<policyImporters\>](../../../../../docs/framework/configure-apps/file-schema/wcf/policyimporters.md)|Specifica tutte le unità di importazione dei criteri che controllano l'importazione di asserzioni di criteri personalizzati sulle associazioni.|  
  
## Note  
 Un'unità di importazione dei criteri viene usata per la ricerca di asserzioni di criteri personalizzati sulle funzionalità delle associazioni e per allegare un elemento di associazione personalizzato che implementa le funzionalità richieste dall'asserzione.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.PolicyImporterElementCollection>   
 <xref:System.ServiceModel.Configuration.PolicyImporterElement>   
 <xref:System.ServiceModel.Configuration.MetadataElement>   
 <xref:System.ServiceModel.Description.MetadataImporter>   
 [Configurazione del client WCF](../../../../../docs/framework/wcf/feature-details/client-configuration.md)   
 [Client](../../../../../docs/framework/wcf/feature-details/clients.md)