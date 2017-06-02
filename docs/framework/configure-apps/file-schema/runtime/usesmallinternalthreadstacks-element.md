---
title: "Elemento &lt;UseSmallInternalThreadStacks&gt; | Microsoft Docs"
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
  - "<UseSmallInternalThreadStacks> (elemento)"
  - "UseSmallInternalThreadStacks (elemento)"
ms.assetid: 1e3f6ec0-1cac-4e1c-9c81-17d948ae5874
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Elemento &lt;UseSmallInternalThreadStacks&gt;
Richiede che il Common Language Runtime \(CLR\) riduca l'utilizzo della memoria specificando dimensioni dello stack esplicite quando crea determinati thread che utilizza internamente, anziché utilizzare la dimensione dello stack predefinita per quei thread.  
  
## Sintassi  
  
```  
<UseSmallInternalThreadStacks enabled="true|false" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|enabled|Attributo obbligatorio.<br /><br /> Specifica se richiedere che CLR utilizzi le dimensioni dello stack esplicite anziché la dimensione dello stack predefinita quando crea determinati thread che utilizza internamente.  Le dimensioni dello stack esplicite sono più piccole della dimensione predefinita dello stack di 1 Mb.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|true|Richiedere dimensioni dello stack esplicite.|  
|false|Utilizzare la dimensione dello stack predefinita.  L'impostazione predefinita per [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] è "Infinity".|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Questo elemento di configurazione è utilizzato per richiedere un utilizzo ridotto della memoria virtuale in un processo, in quanto le dimensioni del thread esplicito che CLR utilizza per i thread interni, se viene rispettata la richiesta, sono più piccole delle dimensioni predefinite.  
  
> [!IMPORTANT]
>  Questo elemento di configurazione è una richiesta a CLR piuttosto che un requisito assoluto.  In [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], la richiesta viene rispettata solo per l'architettura x86.  Questo elemento potrebbe essere ignorato completamente nelle future versioni di CLR o sostituito da dimensioni dello stack esplicite che vengono sempre utilizzate per i thread interni selezionati.  
  
 La specifica di questo elemento di configurazione negozia l'affidabilità per un minore utilizzo di memoria virtuale se CLR onora la richiesta, perché le minori dimensioni dello stack potrebbero potenzialmente rendere più probabile gli overflow dello stack.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come richiedere che le dimensioni esplicite dello stack che CLR utilizza per determinati  thread che utilizza internamente.  
  
```  
<configuration>  
   <runtime>  
      <UseSmallInternalThreadStacks enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)