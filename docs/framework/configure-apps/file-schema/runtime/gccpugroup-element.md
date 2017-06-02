---
title: "Elemento &lt;GCCpuGroup&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<GCCpuGroup> (elemento)"
  - "GCCpuGroup (elemento)"
ms.assetid: c1fc7d6c-7220-475c-a312-5b8b201f66e0
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Elemento &lt;GCCpuGroup&gt;
Specifica se la Garbage Collection supporta più gruppi di CPU.  
  
## Sintassi  
  
```  
<GCCpuGroup    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se la Garbage Collection supporta più gruppi di CPU.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|La Garbage Collection non supporta più gruppi di CPU.  Questa è l'impostazione predefinita.|  
|`true`|La Garbage Collection supporta più gruppi di CPU se il Server della garbage collection è abilitato.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Quando un computer ha più gruppi di CPU e il Server garbage collection è abilitato \(vedere l'elemento [\<gcServer\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcserver-element.md)\), attivare questo elemento estende la Garbage Collection in tutti i gruppi di CPU e tiene in considerazione tutti i core durante la creazione e il bilanciamento degli heap.  
  
> [!NOTE]
>  Questo elemento è valido solo per la thread di Garbage Collection.  Per consentire al runtime di distribuire le thread utente in tutti i gruppi della CPU, è inoltre necessario abilitare l'elemento [\<Thread\_UseAllCpuGroups\>](../../../../../docs/framework/configure-apps/file-schema/runtime/thread-useallcpugroups-element.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come attivare la Garbage Collection per più gruppi di CPU.  
  
```  
<configuration>  
   <runtime>  
      <GCCpuGroup enabled="true"/>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [How to: Disable Concurrent Garbage Collection](http://msdn.microsoft.com/it-it/ba2c6c67-5778-497c-9fac-5f793b5500c7)   
 [Operazione di Garbage Collection per workstation e server](../../../../../docs/standard/garbage-collection/fundamentals.md#workstation_and_server_garbage_collection)