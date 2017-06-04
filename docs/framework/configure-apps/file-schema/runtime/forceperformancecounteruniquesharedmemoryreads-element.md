---
title: "Elemento &lt;forcePerformanceCounterUniqueSharedMemoryReads&gt; | Microsoft Docs"
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
  - "<forcePerformanceCounterUniqueSharedMemoryReads> (elemento)"
  - "forcePerformanceCounterUniqueSharedMemoryReads (elemento)"
ms.assetid: 91149858-4810-4f65-9b48-468488172c9b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Elemento &lt;forcePerformanceCounterUniqueSharedMemoryReads&gt;
Indica se PerfCounter.dll utilizza l'impostazione del registro di sistema di CategoryOptions nell'applicazione .NET Framework versione 1.1 per determinare se caricare dati del contatore delle prestazioni dalla memoria condivisa specifica della categoria o dalla memoria globale.  
  
## Sintassi  
  
```  
<forcePerformanceCounterUniqueSharedMemoryReads   
enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Indica se PerfCounter.dll utilizza l'impostazione del registro di sistema di CategoryOptions per determinare se caricare dati del contatore delle prestazioni dalla memoria condivisa specifico della categoria o dalla memoria globale.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|PerfCounter.dll non utilizza l'impostazione del registro di sistema di CategoryOptions Questa è l'impostazione predefinita.|  
|`true`|PerfCounter.dll utilizza l'impostazione del registro di sistema di CategoryOptions.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 In versioni di .NET Framework precedenti a [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], la versione di PerfCounter.dll caricata corrisponde al runtime caricato nel processo.  Se un computer dispone sia della versione 1.1 di .NET Framework sia di [!INCLUDE[dnprdnlong](../../../../../includes/dnprdnlong-md.md)], un'applicazione di .NET Framework carica la versione 1.1 di .NET Framework di PerfCounter.dll.  Iniziando con [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], la versione installata più recente di PerfCounter.dll viene caricata.  Ciò significa che un'applicazione di .NET Framework 1.1 caricherà la versione [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] di PerfCounter.dll, se [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] è installata nel computer.  
  
 Iniziando con [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], in caso di utilizzo di contatori delle prestazioni, PerfCounter.dll controlla che la voce del registro di sistema di CategoryOptions per ogni provider determini se leggere da memoria condivisa specifica della categoria o da memoria condivisa globale.  PerfCounter.dll di .NET Framework 1.1 non legge questa voce del registro di sistema, perché non tiene presente la memoria condivisa specifica della categoria; legge sempre dalla memoria condivisa globale.  
  
 Per compatibilità con le versioni precedenti, non viene effettuato il controllo della voce del Registro di sistema CategoryOptions tramite la libreria PerfCounter.dll di [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)], se quest'ultima è in esecuzione in un'applicazione .NET Framework 1.1.  Viene semplicemente utilizzata la memoria condivisa globale, come PerfCounter.dll di .NET Framework 1.1.  Tuttavia, è possibile istruire PerfCounter.dll [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] per controllare l'impostazione del registro di sistema di sistema abilitando l'elemento `<forcePerformanceCounterUniqueSharedMemoryReads>`.  
  
> [!NOTE]
>  L'abilitazione dell'elemento `<forcePerformanceCounterUniqueSharedMemoryReads>` non garantisce che sarà utilizzata memoria condivisa specifica della categoria.  L'impostazione abilitata su `true` fa in modo soltanto che PerfCounter.dll faccia riferimento all'impostazione del registro di sistema di CategoryOptions.  L'impostazione predefinita per CategoryOptions consente l'utilizzo di memoria condivisa specifica della categoria; tuttavia, è possibile modificare CategoryOptions per indicare che deve essere utilizzata la memoria condivisa globale.  
  
 La chiave del Registro di sistema che contiene l'impostazione CategoryOptions è HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\\<categoryName\>\\Performance.  Per impostazione predefinita, CategoryOptions viene impostato su 3, istruendo PerfCounter.dll a utilizzare memoria condivisa specifica della categoria.  Se CategoryOptions viene impostato su 0, PerfCounter.dll utilizza la memoria condivisa globale.  I dati dell'istanza saranno riutilizzati solo se il nome dell'istanza creata è identico a quello dell'istanza riutilizzata.  Tutte le versioni saranno in grado di scrivere nella categoria.  Se CategoryOptions viene impostato su 1, la memoria condivisa globale viene utilizzata, ma i dati dell'istanza possono essere riutilizzati se il nome della categoria ha la stessa lunghezza della categoria riutilizzata.  
  
 Le impostazioni 0 e 1 possono condurre a perdite di memoria e al riempimento della memoria del contatore delle prestazioni.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come specificare che PerfCounter.dll deve fare riferimento alla voce del registro di sistema di sistema di CategoryOptions, nel caso in cui debba utilizzare memoria condivisa specifica della categoria.  
  
```  
<configuration>  
  <runtime>  
    <forcePerformanceCounterUniqueSharedMemoryReads enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)