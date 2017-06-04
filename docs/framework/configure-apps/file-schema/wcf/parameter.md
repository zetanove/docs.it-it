---
title: "&lt;parametro&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0fb41e2d-64f7-44ab-993e-05892eac6d82
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;parametro&gt;
Specifica il parametro generico quando un tipo dichiarato è un tipo generico.  
  
## Sintassi  
  
```  
  
<parameter index="integer"  
                      type=String" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|indice|Quando il tipo dichiarato è un tipo generico, specifica il parametro generico che restituirà il tipo conosciuto.|  
|tipo|Stringa che descrive il tipo conosciuto usato per la serializzazione e la deserializzazione.|  
  
## Attributo index  
  
|Valore|Descrizione|  
|------------|-----------------|  
|"0"|Primo parametro del tipo generico.  Ad esempio, un elenco <xref:System.Collections.Generic.List%601> presenta un solo parametro.  Se tale parametro viene usato come tipo dichiarato, impostare l'attributo index su "0".|  
|"1"|Secondo parametro di un tipo generico.  Ad esempio, un dizionario <xref:System.Collections.Generic.Dictionary%602> presenta due parametri.  Se il tipo conosciuto viene restituito dal secondo parametro, impostare l'attributo index su "1".|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<knownType\>](../../../../../docs/framework/configure-apps/file-schema/wcf/knowntype.md)|Specifica un tipo conosciuto restituibile da un campo o da una proprietà del tipo dichiarato.|  
  
## Note  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] sui tipi noti, vedere [Tipi conosciuti di contratto dati](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md) e <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
 Per un esempio di utilizzo di questo elemento, vedere l'[\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md).  
  
 Questo elemento di configurazione non può avere contemporaneamente entrambi gli attributi.  Se si impostano entrambi gli attributi, si verifica un'eccezione <xref:System.Configuration.ConfigurationErrorsException>.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 [Tipi conosciuti di contratto dati](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)   
 [\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)