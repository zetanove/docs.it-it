---
title: "Elemento &lt;ThrowUnobservedTaskExceptions&gt; | Microsoft Docs"
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
  - "<ThrowUnobservedTaskExceptions> (elemento)"
  - "ThrowUnobservedTaskExceptions (elemento)"
ms.assetid: cea7e588-8b8d-48d2-9ad5-8feaf3642c18
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Elemento &lt;ThrowUnobservedTaskExceptions&gt;
Specifica se le eccezioni non gestite di attività devono far terminare un processo in esecuzione.  
  
## Sintassi  
  
```vb  
<ThrowUnobservedTaskExceptions  
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se le eccezioni di attività non gestite devono far terminare il processo in esecuzione.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Non termina il processo in esecuzione per un'eccezione non gestita di attività.  Questa è l'impostazione predefinita.|  
|`true`|Termina il processo in esecuzione per un'eccezione non gestita di attività.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
|||  
  
## Note  
 Se un'eccezione associata a <xref:System.Threading.Tasks.Task> non è stata osservata, non esiste alcuna operazione <xref:System.Threading.Tasks.Task.Wait%2A>, l'elemento padre non è associato e la proprietà di <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=fullName> non è stata letta l'eccezione di attività viene considerata inosservata.  
  
 In [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], per impostazione predefinita, se un <xref:System.Threading.Tasks.Task> con un'eccezione inosservata viene raccolto nel garbage collector, il finalizzatore genera un'eccezione e termina il processo.  L'interruzione del processo è determinata dall'intervallo di Garbage Collection e la finalizzazione.  
  
 Per semplificare agli sviluppatori la scrittura del codice asincrono basato sulle attività, [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)] modifica questo comportamento predefinito per le eccezioni inosservate.  Le eccezioni inosservate ancora determinano la generazione dell'evento <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException>, ma per impostazione predefinita, il processo non termina.  Invece, l'eccezione è ignorata dopo che l'evento viene generato, indipendentemente dal fatto che un gestore di eventi rilevi l'eccezione.  
  
 In [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)], è possibile utilizzare l'[elemento \<ThrowUnobservedTaskExceptions\>](../../../../../docs/framework/configure-apps/file-schema/runtime/throwunobservedtaskexceptions-element.md) in un file di configurazione dell'applicazione per abilitare il comportamento di [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] di generare un'eccezione.  
  
 È inoltre possibile specificare il comportamento dell'eccezione in uno dei modi seguenti:  
  
-   Impostando la variabile di ambiente `COMPlus_ThrowUnobservedTaskExceptions` \(`set COMPlus_ThrowUnobservedTaskExceptions=1`\).  
  
-   Impostando il valore DWORD ThrowUnobservedTaskExceptions \= 1 del Registro di sistema nella chiave HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\.NETFramework .  
  
## Esempio  
 Nell'esempio seguente viene illustrato come abilitare la generazione di eccezioni nelle attività tramite un file di configurazione dell'applicazione.  
  
```  
<configuration>   
    <runtime>   
        <ThrowUnobservedTaskExceptions enabled="true"/>   
    </runtime>   
</configuration>  
  
```  
  
## Esempio  
 Nell'esempio seguente viene illustrato come un'eccezione inosservata viene generata da un'attività.  Il codice deve essere eseguito come programma generato per funzionare correttamente.  
  
 [!code-csharp[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/throwunobservedtaskexceptions/cs/program.cs#1)]
 [!code-vb[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/throwunobservedtaskexceptions/vb/program.vb#1)]  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)