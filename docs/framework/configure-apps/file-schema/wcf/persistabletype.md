---
title: "&lt;persistableType&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5425fe6-523a-4076-aab4-2c2515b1d830
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;persistableType&gt;
Specifica tutti i tipi persistenti.  
  
## Sintassi  
  
```  
  
<comContracts>  
  <comContract>  
      <persistableTypes>  
         <persistableType id="string"  
            name="string">  
         </persistableType>  
      </persistableTypes>  
  </comContract>  
</comContracts>  
```  
  
## Tipo  
 `Type`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|id|Un attributo obbligatorio che contiene una stringa che specifica un identificatore univoco per un tipo persistente.|  
|name|Attributo facoltativo contenente una stringa che specifica il nome del tipo persistente.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<persistableTypes\>](../../../../../docs/framework/configure-apps/file-schema/wcf/persistabletypes.md)|Raccolta di elementi `persistableType`.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ComPersistableTypeElementCollection>   
 <xref:System.ServiceModel.Configuration.ComPersistableTypeElement>   
 [\<comContracts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/comcontracts.md)   
 [Integrazione con applicazioni COM\+](../../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)   
 [Procedura: configurare le impostazioni del servizio COM\+](../../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)