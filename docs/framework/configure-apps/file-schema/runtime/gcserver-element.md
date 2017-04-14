---
title: "Elemento &lt;gcServer&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/gcServer"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#gcServer"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<gcServer> (elemento)"
  - "gcServer (elemento)"
ms.assetid: 8d25b80e-2581-4803-bd87-a59528e3cb03
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# Elemento &lt;gcServer&gt;
Specifica se Common Language Runtime esegue Garbage Collection per server.  
  
## Sintassi  
  
```  
<gcServer    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se il runtime esegue Garbage Collection per server.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Non esegue Garbage Collection per server.  Questa è l'impostazione predefinita.|  
|`true`|Esegue Garbage Collection per server.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione usato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Common Language Runtime \(CLR\) supporta due tipi di Garbage Collection: Garbage Collection per workstation, disponibile in tutti i sistemi, e Garbage Collection per server, disponibile nei sistemi con più processori.  Si usa l'elemento `<gcServer>` per controllare il tipo di Garbage Collection eseguito da CLR.  Usare la proprietà <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=fullName> per determinare se l'operazione Garbage Collection per server è abilitata.  
  
 Per i computer con un solo processore, l'operazione di Garbage Collection per workstation predefinita dovrebbe essere l'opzione più rapida.  Per i computer con due processori, si può usare quella per workstation o quella per server.  L'operazione di Garbage Collection per server dovrebbe essere l'opzione più rapida per più di due processori.  
  
 Questo elemento può essere usato solo nel file di configurazione dell'applicazione. Se è nel file di configurazione del computer, viene ignorato.  
  
> [!NOTE]
>  In .NET Framework 4 e versioni precedenti, la modalità di Garbage Collection simultanea non è disponibile quando l'operazione di Garbage Collection per server è abilitata.  A partire da [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)], l'operazione di Garbage Collection per server è simultanea.  Per usare l'operazione di Garbage Collection per server non simultanea, impostare l'elemento `<gcServer>` su `true` e l'elemento [\<gcConcurrent\>](../../../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) su `false`.  
  
## Esempio  
 L'esempio seguente abilita l'operazione di Garbage Collection per server.  
  
```  
  
<configuration>  
   <runtime>  
      <gcServer enabled="true"/>  
   </runtime>  
</configuration>  
  
```  
  
## Vedere anche  
 <xref:System.Runtime.GCSettings.IsServerGC%2A?displayProperty=fullName>   
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [How to: Disable Concurrent Garbage Collection](http://msdn.microsoft.com/it-it/ba2c6c67-5778-497c-9fac-5f793b5500c7)