---
title: "CLR ETW Keywords and Levels | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "CLR ETW keywords"
  - "CLR ETW levels"
  - "ETW, CLR keywords"
  - "ETW, CLR levels"
ms.assetid: fdf5856d-516b-4042-849d-911c4518a6cb
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# CLR ETW Keywords and Levels
<a name="top"></a> Gli eventi Event Tracing for Windows \(ETW\) possono essere filtrati in base a categoria e livello. Le [Parole chiave ETW di CLR](#keywords) degli eventi permettono di filtrare gli eventi per categoria e vengono usate in diverse combinazioni per i provider di runtime e rundown. I [livelli evento](#levels) vengono identificati da flag.  
  
<a name="keywords"></a>   
## Parole chiave ETW di CLR  
 Le parole chiave sono flag che possono essere combinati per generare valori. In pratica, è possibile usare i valori esadecimali delle parole chiave invece dei nomi delle parole chiave quando si chiamano le utilità della riga di comando.  
  
 Le parole chiave vengono descritte nelle tabelle seguenti.  
  
-   [Parole chiave di runtime ETW di CLR](#runtime)  
  
-   [Parole chiave di rundown ETW di CLR](#rundown)  
  
-   [Combinazioni di parole chiave per la risoluzione dei simboli per il provider di runtime](#runtime_combo)  
  
-   [Combinazioni di parole chiave per la risoluzione dei simboli per il provider di rundown](#rundown_combo)  
  
<a name="runtime"></a>   
### Parole chiave di runtime ETW di CLR  
 La tabella seguente contiene le parole chiave di runtime ETW di CLR, i rispettivi valori e informazioni sullo scopo per cui vengono usate.  
  
|Nome parola chiave di runtime|Valore|Scopo|  
|-----------------------------------|------------|-----------|  
|`GCKeyword`|0x00000001|Consente la raccolta di [eventi di Garbage Collection](../../../docs/framework/performance/garbage-collection-etw-events.md).|  
|`LoaderKeyword`|0x00000008|Consente la raccolta di [eventi del caricatore](../../../docs/framework/performance/loader-etw-events.md).|  
|`JITKeyword`|0x00000010|Consente la raccolta di [eventi JIT \(Just\-In\-Time\)](../../../docs/framework/performance/jit-tracing-etw-events.md).|  
|`NGenKeyword`|0x00000020|Consente la raccolta di eventi per metodi delle immagini native \(metodi elaborati dal generatore di immagini native, Ngen.exe\). Viene usata con `StartEnumerationKeyword` e `EndEnumerationKeyword`. Questa parola chiave ha un overhead elevato. Genera eventi per ogni metodo incluso in ogni modulo NGen caricato. Se possibile, invece di usare questa parola chiave è consigliabile usare database di programma \(PDB\) generati da strumenti di profilatura che recuperano informazioni sui metodi dai moduli NGen. Vedere anche `OverrideAndSuppressNGenEventsKeyword` più avanti in questa tabella.|  
|`StartEnumerationKeyword`|0x00000040|Consente l'enumerazione di tutti i metodi nel runtime. Viene usata in combinazione con `NGenKeyword`.|  
|`EndEnumerationKeyword`|0x00000080|Consente l'enumerazione di tutti i metodi eliminati nel runtime. Viene usata in combinazione con `JITKeyword` e `NGenKeyword`.|  
|`SecurityKeyword`|0x00000400|Consente la raccolta di [eventi di sicurezza](../../../docs/framework/performance/security-etw-events.md).|  
|`AppDomainResourceManagementKeyword`|0x00000800|Consente la raccolta di eventi di monitoraggio delle risorse a livello di dominio applicazione.|  
|`JITTracingKeyword`|0x00001000|Consente la raccolta di [eventi di traccia JIT](../../../docs/framework/performance/jit-tracing-etw-events.md).|  
|`InteropKeyword`|0x00002000|Consente la raccolta di [eventi di interoperabilità](../../../docs/framework/performance/interop-etw-events.md).|  
|`ContentionKeyword`|0x00004000|Consente la raccolta di [eventi di conflitto](../../../docs/framework/performance/contention-etw-events.md).|  
|`ExceptionKeyword`|0x00008000|Consente la raccolta di [eventi di eccezione](../../../docs/framework/performance/exception-thrown-v1-etw-event.md).|  
|`ThreadingKeyword`|0x00010000|Consente la raccolta di [eventi del pool di thread](../../../docs/framework/performance/thread-pool-etw-events.md).|  
|`OverrideAndSuppressNGenEventsKeyword`|0x00040000|\(Disponibile in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] e versioni successive\). Elimina la parola chiave `NGenKeyword` con overhead elevato e impedisce la generazione di eventi per i metodi inclusi nei moduli NGen. A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], gli strumenti di profilatura devono usare `OverrideAndSuppressNGenEventsKeyword` e `NGenKeyword` insieme per eliminare la generazione di eventi per i metodi nei moduli NGen. In questo modo, lo strumento di profilatura può usare i più efficienti PDB NGen per ottenere informazioni sui metodi nei moduli NGen. CLR in .NET Framework 4 e versioni precedenti non supporta la creazione di PDB NGen. In queste versioni precedenti CLR non riconosce `OverrideAndSuppressNGenEventsKeyword` ed elabora `NGenKeyword` per generare eventi per i metodi nei moduli NGen.|  
|`PerfTrackKeyWord`|0x2000000|Consente la raccolta di eventi `ModuleLoad` e `ModuleRange`.|  
|`StackKeyword`|0x40000000|Consente la raccolta di [eventi di analisi dello stack](../../../docs/framework/performance/stack-etw-event.md) di CLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="rundown"></a>   
### Parole chiave di rundown ETW di CLR  
 La tabella seguente contiene le parole chiave di rundown ETW di CLR, i rispettivi valori e informazioni sullo scopo per cui vengono usate.  
  
|Nome parola chiave di rundown|Valore|Scopo|  
|-----------------------------------|------------|-----------|  
|`LoaderRundownKeyword`|0x00000008|Consente la raccolta di eventi del caricatore se usata con `StartRundownKeyword` e `EndRundownKeyword`.|  
|`JitRundownKeyword`|0x00000010|Consente la raccolta di eventi `DCStart` e `DCEnd` per metodi compilati tramite JIT se usata con `StartRundownKeyword` e `EndRundownKeyword`.|  
|`NGenRundownKeyword`|0x00000020|Consente la raccolta di eventi `DCStart` e `DCEnd` per metodi delle immagini native NGen se usata con `StartRundownKeyword` e `EndRundownKeyword`. Questa parola chiave ha un overhead elevato. Genera eventi per ogni metodo incluso in ogni modulo NGen caricato. Se possibile, invece di usare questa parola chiave è consigliabile usare database di programma \(PDB\) generati da strumenti di profilatura che recuperano informazioni sui metodi dai moduli NGen. Vedere anche `OverrideAndSuppressNGenEventsRundownKeyword` più avanti in questa tabella.|  
|`StartRundownKeyword`|0x00000040|Consente l'enumerazione dello stato del sistema durante un rundown di avvio.|  
|`EndRundownKeyword`|0x00000100|Consente l'enumerazione dello stato del sistema durante un rundown di fine.|  
|`AppDomainResourceManagementRundownKeyword`|0x00000800|Consente la raccolta di eventi per il monitoraggio delle risorse a livello di <xref:System.AppDomain> se usata con `StartRundownKeyword` o `EndRundownKeyword`.|  
|`ThreadingKeyword`|0x00010000|Consente la raccolta di eventi del pool di thread.|  
|`OverrideAndSuppressNGenEventsRundownKeyword`|0x00040000|Disponibile in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] e versioni successive. Elimina la parola chiave `NGenRundownKeyword` con overhead elevato e impedisce la generazione di eventi per i metodi inclusi nei moduli NGen. A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], gli strumenti di profilatura devono usare `OverrideAndSuppressNGenEventsRundownKeyword` e `NGenRundownKeyword` insieme per eliminare la generazione di eventi per i metodi nei moduli NGen. In questo modo, lo strumento di profilatura può usare i più efficienti PDB NGen per ottenere informazioni sui metodi nei moduli NGen. CLR in .NET Framework 4 e versioni precedenti non supporta la creazione di PDB NGen. In queste versioni precedenti CLR non riconosce `OverrideAndSuppressNGenEventsRundownKeyword` ed elabora `NGenRundownKeyword` per generare eventi per i metodi nei moduli NGen.|  
|`PerfTrackKeyWord`|0x2000000|Consente la raccolta degli eventi `ModuleDCStart`, `ModuleDCEnd`, `ModuleRangeDCStart`e `ModuleRangeDCEnd`.|  
  
 [Torna all'inizio](#top)  
  
<a name="runtime_combo"></a>   
### Combinazioni di parole chiave per la risoluzione dei simboli per il provider di runtime  
  
|Parole chiave e flag|Eventi di caricamento\/scaricamento di domini applicazione, assembly e moduli|Eventi di caricamento\/scaricamento di metodi \(tranne gli eventi dinamici\)|Eventi dinamici di caricamento\/eliminazione di metodi|  
|--------------------------|-----------------------------------------------------------------------------------|----------------------------------------------------------------------------------|------------------------------------------------------------|  
|`LoaderKeyword`|Eventi di caricamento e scaricamento di moduli.|Nessuno.|Nessuno.|  
|`JITKeyword`<br /><br /> \(\+ `StartEnumerationKeyword` non aggiunge nulla\)|Nessuno.|Eventi di caricamento.|Eventi di caricamento e scaricamento di moduli.|  
|`JITKeyword` \+<br /><br /> `EndEnumerationKeyword`|Nessuno.|Eventi di caricamento e scaricamento di moduli.|Eventi di caricamento e scaricamento di moduli.|  
|`NGenKeyword`|Nessuno.|Nessuno.|Non applicabile.|  
|`NGenKeyword` \+<br /><br /> `StartEnumerationKeyword`|Nessuno.|Eventi di caricamento.|Non applicabile.|  
|`NGenKeyword` \+<br /><br /> `EndEnumerationKeyword`|Nessuno.|Eventi di scaricamento.|Non applicabile.|  
  
 [Torna all'inizio](#top)  
  
<a name="rundown_combo"></a>   
### Combinazioni di parole chiave per la risoluzione dei simboli per il provider di rundown  
  
|Parole chiave e flag|Eventi DCStart\/DCEnd di domini applicazione, assembly e moduli|Eventi DCStart\/DCEnd di metodi \(inclusi gli eventi di metodi dinamici\)|  
|--------------------------|---------------------------------------------------------------------|-------------------------------------------------------------------------------|  
|`LoaderRundownKeyword` \+<br /><br /> `StartRundownKeyword`|Eventi `DCStart`.|Nessuno.|  
|`LoaderRundownKeyword` \+<br /><br /> `EndRundownKeyword`|Eventi `DCEnd`.|Nessuno.|  
|`JITKeyword` \+<br /><br /> `StartRundownKeyword`|Nessuno.|Eventi `DCStart`.|  
|`JITKeyword` \+<br /><br /> `EndRundownKeyword`|Nessuno.|Eventi `DCEnd`.|  
|`NGenKeyword` \+<br /><br /> `StartRundownKeyword`|Nessuno.|Eventi `DCStart`.|  
|`NGenKeyword` \+<br /><br /> `EndRundownKeyword`|Nessuno.|Eventi `DCEnd`.|  
  
 [Torna all'inizio](#top)  
  
<a name="levels"></a>   
## Livelli evento ETW  
 Gli eventi ETW possono essere filtrati in base al livello. Se il livello è impostato su 0x5, vengono generati gli eventi di tutti i livelli, inclusi il livello 0x5 e quelli inferiori \(ovvero gli eventi che appartengono alle categorie abilitate tramite le parole chiave\). Se il livello è impostato su 0x2, vengono generati solo gli eventi che appartengono al livello 0x2 e a quelli inferiori.  
  
 I livelli hanno i significati seguenti:  
  
 0x5 \- Dettagliato  
  
 0x4 \- Informativo  
  
 0x3 \- Avviso  
  
 0x2 \- Errore  
  
 0x1 \- Critico  
  
 0x0 \- LogAlways  
  
## Vedere anche  
 [CLR ETW Providers](../../../docs/framework/performance/clr-etw-providers.md)   
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)   
 [ETW Events in the Common Language Runtime](../../../docs/framework/performance/etw-events-in-the-common-language-runtime.md)