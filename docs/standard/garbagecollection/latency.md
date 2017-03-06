---
title: "Modalità di latenza"
description: "Modalità di latenza"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/18/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 810bd8be-5a48-42c6-b080-3afdb31fc61b
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 1d99ac95527cae80b74c96f5a2e6be81b94176c5
ms.lasthandoff: 03/02/2017

---

# <a name="latency-modes"></a>Modalità di latenza

Per recuperare oggetti, tramite il Garbage Collector devono essere arrestati tutti i thread in esecuzione in un'applicazione. In alcune situazioni, ad esempio quando un'applicazione recupera dati o visualizza contenuto, un'operazione completa di Garbage Collection può verificarsi in un momento critico e può ostacolare le prestazioni. È possibile rettificare l'ingerenza del Garbage Collector impostando la proprietà [GCSettings.LatencyMode](xref:System.Runtime.GCSettings.LatencyMode) su uno dei valori [System.Runtime.GCLatencyMode](xref:System.Runtime.GCLatencyMode). 

La latenza si riferisce al momento dell'intrusione del Garbage Collector nell'applicazione. Durante i periodi di bassa latenza, il Garbage Collector è più conservativo e meno intrusivo nel recupero degli oggetti. Tramite l'enumerazione [System.Runtime.GCLatencyMode](xref:System.Runtime.GCLatencyMode) vengono fornite due impostazioni a bassa latenza:

* [LowLatency](xref:System.Runtime.GCLatencyMode.LowLatency) elimina le raccolte di generazione 2 ed esegue solo le raccolte di generazione 0 e 1. Può essere usato solo per brevi periodi di tempo. In caso di lunghi periodi, se viene usata una quantità elevata di memoria, tramite il Garbage Collector verrà attivata una raccolta mediante la quale è possibile mettere in pausa brevemente l'applicazione e interrompere un'operazione critica rispetto al tempo. Questa impostazione è disponibile solo per le operazioni di Garbage Collection per workstation. 

* [SustainedLowLatency](xref:System.Runtime.GCLatencyMode.SustainedLowLatency) elimina le raccolte di generazione 2 in primo piano ed esegue solo le raccolte di generazione 0, 1 e di generazione 2 in background. Può essere usato per periodi di tempo più lunghi ed è disponibile per le operazioni di Garbage Collection per workstation e per server. Questa impostazione non può essere usata se l'operazione di [Garbage Collection in modalità simultanea](https://msdn.microsoft.com/library/yhwwzef8.aspx) è disabilitata.

Durante i periodi di bassa latenza, le raccolte di generazione 2 vengono soppresse eccetto nei seguenti casi:

* Il sistema riceve una notifica di memoria insufficiente dal sistema operativo.

* Il codice dell'applicazione induce una raccolta chiamando il metodo [GC.Collect](xref:System.GC.Collect(System.Int32)) e specificando 2 per il parametro di generazione.

La tabella seguente elenca gli scenari di applicazione per l'uso dei valori [GCLatencyMode](xref:System.Runtime.GCLatencyMode).

Modalità di latenza | Scenari di applicazione
------------ | --------------------- 
[Batch](xref:System.Runtime.GCLatencyMode.Batch) | Per applicazioni che non hanno nessuna interfaccia utente o operazioni lato server. Si tratta della modalità predefinita quando l'operazione di [Garbage Collection in modalità simultanea](https://msdn.microsoft.com/library/yhwwzef8.aspx) è disabilitata.
[Interactive](xref:System.Runtime.GCLatencyMode.Interactive) | Per la maggior parte delle applicazioni che hanno una interfaccia utente. Per applicazioni che non hanno nessuna interfaccia utente o operazioni lato server. Si tratta della modalità predefinita quando l'operazione di [Garbage Collection in modalità simultanea](https://msdn.microsoft.com/library/yhwwzef8.aspx) è abilitata.
[LowLatency](xref:System.Runtime.GCLatencyMode.LowLatency) | Per le applicazioni con operazioni a breve termine, per cui il tempo riveste un'importanza significativa, durante le quali le interruzioni del Garbage Collector potrebbero rivelarsi dannose. Ad esempio, applicazioni di rendering delle animazioni o che hanno funzioni di acquisizione dei dati.
[SustainedLowLatency](xref:System.Runtime.GCLatencyMode.SustainedLowLatency) | Per le applicazioni con operazioni per cui i tempi sono importanti per una durata contenuta, ma potenzialmente lunga, durante la quale le interruzioni del Garbage Collector potrebbero rivelarsi dannose. Ad esempio, le applicazioni per cui sono richiesti tempi di risposta rapidi come i cambiamenti dei dati di mercato durante le ore di negoziazione.   Questa modalità comporta dimensioni dell'heap gestito maggiori rispetto ad altre. Poiché non consente di comprimere l'heap gestito, è possibile avere una maggiore frammentazione. Assicurarsi che sia disponibile memoria sufficiente.
 
## <a name="guidelines-for-using-low-latency"></a>Linee guida per l'uso della bassa latenza

Quando si usa la modalità [LowLatency](xref:System.Runtime.GCLatencyMode.LowLatency), tenere in considerazione le linee guida seguenti:

* Mantenere il periodo di tempo in bassa latenza più brevemente possibile.

* Evitare di allocare quantità di memoria elevate durante i periodi di bassa latenza. Possono verificarsi notifiche di memoria insufficiente perché le operazioni di Garbage Collection recuperano meno oggetti. 

* In modalità di bassa latenza, ridurre al minimo il numero delle allocazioni effettuate, in particolare le allocazioni su Large Object Heap e oggetti bloccati. 

* Tenere presenti i thread che potrebbero essere in corso di allocazione. Poiché l'impostazione della proprietà [LatencyMode](xref:System.Runtime.GCSettings.LatencyMode) interessa l'intero processo, è possibile generare un'eccezione [OutOfMemoryException](xref:System.OutOfMemoryException) in ogni thread eventualmente in corso di allocazione. 

* È possibile forzare le raccolte di generazione 2 durante un periodo di bassa latenza chiamando il metodo [GC.Collect(Int32, GCCollectionMode)](xref:System.GC.Collect(System.Int32,System.GCCollectionMode)).

## <a name="see-also"></a>Vedere anche

[System.GC](xref:System.GC)

[Raccolte indotte](induced.md)

[Garbage Collection in .NET](index.md)

