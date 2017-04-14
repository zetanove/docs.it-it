---
title: "Elemento &lt;Directives&gt; (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 444846f3-48d5-4341-a43e-69f7221389eb
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Elemento &lt;Directives&gt; (.NET Native)
Elemento radice in ogni file di direttive di runtime per [!INCLUDE[net_native](../../../includes/net-native-md.md)].  
  
 **\<Directives xmlns\="http:\/\/schemas.microsoft.com\/netfx\/2013\/01\/metadata"\>**  
  
## Sintassi  
  
```xml  
  
        <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <!-- child elements -->   
</Directives>  
```  
  
## Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`xmlns`|Spazio dei nomi XML.  Il valore è sempre **"http:\/\/schemas.microsoft.com\/netfx\/2013\/01\/metadata"**.|  
  
## Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<Application\>](../../../docs/framework/net-native/application-element-net-native.md)|Viene usato come contenitore per i tipi e i membri dei tipi a livello di applicazione i cui metadati sono disponibili per la reflection.|  
|[\<Library\>](../../../docs/framework/net-native/library-element-net-native.md)|Definisce l'assembly i cui tipi di figlio e i membri di tipo richiedono metadati in fase di esecuzione.|  
  
## Note  
 Ogni file di direttive di runtime può contenere un solo elemento `<Directives>`.  
  
 L'elemento `<Directives>` può contenere zero o un elemento [\<Application\>](../../../docs/framework/net-native/application-element-net-native.md) e zero, uno o più elementi [\<Library\>](../../../docs/framework/net-native/library-element-net-native.md).  
  
## Vedere anche  
 [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)