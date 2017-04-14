---
title: "&lt;debugCallback&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4073feda-1857-4be4-9947-227afb847ced
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;debugCallback&gt;
Specifica il debug del servizio per un oggetto di callback [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## Sintassi  
  
```  
  
<callbackDebug  includeExceptionDetailInFaults="Boolean" />  
```  
  
## Tipo  
 `Type`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`includeExceptionDetailInFaults`|Valore che specifica se oggetti callback del client restituiscono al servizio informazioni sulle eccezioni gestite negli errori SOAP.<br /><br /> Se questo attributo viene impostato su `true` a livello di programmazione, è possibile abilitare il flusso di informazioni sulle eccezioni gestite in un oggetto callback del client nel servizio a fini di debug. **Caution:**  La restituzione ai client di informazioni sulle eccezioni gestite può costituire un rischio per la sicurezza.  Questo perché i dettagli delle eccezioni espongono informazioni sull'implementazione interna del servizio che potrebbero venire usate da client non autorizzati.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un comportamento dell'endpoint.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.CallbackDebugElement>   
 <xref:System.ServiceModel.Description.CallbackDebugBehavior>