---
title: "Elemento &lt;Thread_UseAllCpuGroups&gt; | Microsoft Docs"
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
ms.assetid: d30fe7c5-8469-46e2-b804-e3eec7b24256
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Elemento &lt;Thread_UseAllCpuGroups&gt;
Specifica se il runtime distribuisce thread gestiti in tutti i gruppi della CPU.  
  
## Sintassi  
  
```vb  
<Thread_UseAllCpuGroups    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se il runtime distribuisce thread gestiti in tutti i gruppi della CPU.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Il runtime non distribuisce i thread gestiti su più gruppi di CPU.  Impostazione predefinita.|  
|`true`|Il runtime distribuisce i thread gestiti su più gruppi della CPU, se il computer ha più gruppi di CPU e l'elemento [\<GCCpuGroup\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md) è abilitato.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Quando un computer include più gruppi di CPU, l'abilitazione di questo elemento fa sì che il runtime distribuisca i thread gestiti in tutti i gruppi di CPU.  Per utilizzare questa funzionalità, è possibile attivare l'elemento [\<\<GCCpuGroup\>\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md), che estende la Garbage Collection a tutti i gruppi di CPU e prende in considerazione tutti i core durante la creazione e il bilanciamento degli heap.  L'abilitazione dell'elemento [\<GCCpuGroup\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md) richiede l'abilitazione dell'elemento [\<gcServer\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcserver-element.md).  Se questi elementi non sono abilitati, l'attivazione dell'elemento `<Thread_UseAllCpuGroups>` non produrrà alcun effetto.  
  
## Esempio  
 L'esempio seguente mostra come abilitare il supporto per più gruppi di CPU.  
  
```  
<configuration>  
   <runtime>  
      <Thread_UseAllCpuGroups enabled="true"/>  
      <GCCpuGroup enabled="true"/>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Elemento \<GCCpuGroup\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gccpugroup-element.md)