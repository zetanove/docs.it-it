---
title: Raccolte indotte
description: Raccolte indotte
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3e09b9dd-a800-4e56-b468-619f910ae22e
translationtype: Human Translation
ms.sourcegitcommit: 213ce098bcc2b5e31c55e759d895254d5ca33caa
ms.openlocfilehash: a10822518f0687dc7bbb06dd0fb77f6d9a3196fb

---

# <a name="induced-collections"></a>Raccolte indotte

Nella maggior parte dei casi, tramite il Garbage Collector è possibile determinare il momento migliore per eseguire una raccolta ed è consigliabile consentire l'esecuzione in modo indipendente. In rari casi una raccolta forzata può migliorare le prestazioni dell'applicazione. In questi casi, si può indurre un'operazione di Garbage Collection usando il metodo [GC.Collect](xref:System.GC.Collect). 

Usare il metodo [Collect](xref:System.GC.Collect) quando si verifica una riduzione significativa della quantità di memoria usata in un momento specifico nel codice dell'applicazione. Se ad esempio l'applicazione usa una finestra di dialogo complessa con numerosi comandi, la chiamata del metodo [Collect](xref:System.GC.Collect) quando la finestra di dialogo è chiusa può migliorare le prestazioni mediante l'immediato recupero della memoria usata dalla finestra di dialogo. Assicurarsi che l'applicazione non induca troppo spesso l'operazione di Garbage Collection, in quanto può causare una riduzione delle prestazioni se il Garbage Collector tenta di recuperare oggetti in momenti non ottimali. È possibile specificare un valore di enumerazione [GCCollectionMode.Optimized](xref:System.GCCollectionMode.Optimized) nel metodo [Collect](xref:System.GC.Collect) in modo che la raccolta venga eseguita solo quando è produttivo, come descritto nella sezione successiva.

## <a name="gc-collection-mode"></a>Modalità di raccolta Garbage Collection

È possibile usare uno degli overload del metodo [GC.Collect](xref:System.GC.Collect) che include un valore [GCCollectionMode](xref:System.GCCollectionMode) per specificare il comportamento di una raccolta forzata, come indicato di seguito.

Valore GCCollectionMode | Descrizione
---------------------- | ----------- 
[Default](xref:System.GCCollectionMode.Default) | Usa l'impostazione di Garbage Collection predefinita per la versione di .NET Framework in esecuzione.
[Forced](xref:System.GCCollectionMode.Forced) | Forza l'esecuzione immediata dell'operazione di Garbage Collection. Equivale alla chiamata dell'overload di [GC.Collect()](xref:System.GC.Collect). Restituisce una raccolta di blocco completa di tutte le generazioni. Prima di forzare l'esecuzione immediata di un'operazione completa di Garbage Collection di blocco, è anche possibile comprimere gli heap di oggetti di grandi dimensioni impostando la proprietà [GCSettings.LargeObjectHeapCompactionMode](xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode) su [GCLargeObjectHeapCompactionMode.CompactOnce](xref:System.Runtime.GCLargeObjectHeapCompactionMode.CompactOnce). 
[Optimized](xref:System.GCCollectionMode.Optimized) | Consente al Garbage Collector di determinare se il momento corrente è ottimale per recuperare oggetti. Il Garbage Collector può determinare che una raccolta non è sufficientemente produttiva per giustificarne l'esecuzione, nel qual caso esce dalla funzione senza recuperare oggetti.
 
## <a name="background-or-blocking-collections"></a>Raccolte in background o di blocco

È possibile chiamare l'overload del metodo [GC.Collect(Int32, GCCollectionMode, Boolean)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean)) per specificare se una raccolta indotta è di blocco o meno. Il tipo della raccolta eseguita dipende da una combinazione dei parametri *mode* e *blocking* del metodo. Il parametro *mode* è parte dell'enumerazione [GCCollectionMode](xref:System.GCCollectionMode) e *blocking* è un valore [booleano](xref:System.Boolean). La tabella seguente riepiloga l'interazione degli argomenti Mode e Blocking. 

*mode* | *blocking* = true | *blocking* = false
------ | ----------------- | ------------------
[Forzata](xref:System.GCCollectionMode.Forced) o [Predefinita](xref:System.GCCollectionMode.Default) | Viene eseguita una raccolta di blocco il prima possibile. Se è in corso una raccolta in background e la generazione è 0 o 1, il metodo [Collect(Int32, GCCollectionMode, Boolean)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean)) attiva immediatamente una raccolta di blocco e viene restituito quando la raccolta viene completata. Se è in corso una raccolta in background e il parametro della generazione è 2, il metodo attende fino a quando la raccolta in background non viene completata, attiva una raccolta di blocco di generazione 2 e viene restituito. | Viene eseguita una raccolta il prima possibile. Il metodo [Collect(Int32, GCCollectionMode, Boolean)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean)) richiede una raccolta in background, ma non è garantita. A seconda del caso, può essere ancora eseguita una raccolta di blocco. Se è già in corso una raccolta in background, il metodo viene restituito immediatamente. 
[Optimized](xref:System.GCCollectionMode.Optimized) | È possibile eseguire una raccolta di blocco, a seconda dello stato del Garbage Collector e del parametro di generazione. Il Garbage Collector tenta di garantire prestazioni ottimali. | È possibile eseguire una raccolta, a seconda dello stato del Garbage Collector. Il metodo [Collect(Int32, GCCollectionMode, Boolean)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean)) richiede una raccolta in background, ma non è garantita. A seconda del caso, può essere ancora eseguita una raccolta di blocco. Il Garbage Collector tenta di garantire prestazioni ottimali. Se è già in corso una raccolta in background, il metodo viene restituito immediatamente. 
 
## <a name="see-also"></a>Vedere anche

[Modalità di latenza](latency.md)

[Garbage Collection in .NET](index.md)



<!--HONumber=Nov16_HO1-->


