---
title: Riferimenti deboli
description: Riferimenti deboli
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/19/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 22319f2f-0008-4ace-815e-545892a0512a
translationtype: Human Translation
ms.sourcegitcommit: 213ce098bcc2b5e31c55e759d895254d5ca33caa
ms.openlocfilehash: a966f430c00f07d48f2210d64f03d6805f4e3097

---

# <a name="weak-references"></a>Riferimenti deboli

Il Garbage Collector non può raccogliere un oggetto usato da un'applicazione finché il codice dell'applicazione è in grado raggiungere tale oggetto. Si dice che l'applicazione ha un riferimento sicuro all'oggetto. 

Un riferimento debole consente al Garbage Collector di raccogliere l'oggetto, pur senza impedire all'applicazione di accedervi. Un riferimento debole è valido solo durante il periodo di tempo indeterminato fino a quando l'oggetto viene raccolto, se non è presente nessun riferimento sicuro. Quando si usa un riferimento debole, l'applicazione può comunque ottenere un riferimento sicuro all'oggetto, che ne impedirà la raccolta. Tuttavia esiste sempre il rischio che il Garbage Collector raggiunga l'oggetto prima che venga ristabilito un riferimento sicuro.

I riferimenti deboli sono utili per gli oggetti che usano grandi quantità di memoria ma possono essere ricreati facilmente se vengono raccolti dall'operazione di Garbage Collection. 

Si supponga che una visualizzazione struttura ad albero mostri una gamma gerarchica complessa di opzioni all'utente. Se i dati sottostanti sono di grandi dimensioni, non è efficiente mantenere la struttura in memoria mentre l'utente esegue altre operazioni nell'applicazione. 

Quando l'utente passa a un'altra parte dell'applicazione, è possibile usare la classe [WeakReference](xref:System.WeakReference) o [WeakReference&lt;T&gt;](xref:System.WeakReference%601) per creare un riferimento debole alla struttura ad albero ed eliminare tutti i riferimenti sicuri. Quando l'utente torna alla struttura, l'applicazione cerca di ottenere un riferimento sicuro alla struttura ad albero e, se vi riesce, evita la ricostruzione della struttura.

Per stabilire un riferimento debole a un oggetto è necessario creare una classe [WeakReference](xref:System.WeakReference) usando l'istanza dell'oggetto da rilevare. È quindi necessario impostare la proprietà [Target](xref:System.WeakReference.Target) sull'oggetto e impostare il riferimento originale all'oggetto su null. 

## <a name="short-and-long-weak-references"></a>Riferimenti deboli brevi e lunghi

È possibile creare un riferimento debole breve o lungo: 

* Short

  La destinazione di un riferimento debole breve diventa `null` quando l'oggetto viene raccolto dall'operazione di Garbage Collection. Il riferimento debole è in sé un oggetto gestito ed è soggetto a Garbage Collection come qualsiasi altro oggetto gestito. Un riferimento debole breve è il costruttore predefinito per [WeakReference](xref:System.WeakReference). 

* Long

  Un riferimento debole lungo viene mantenuto dopo la chiamata del metodo [Finalize](xref:System.Object.Finalize) dell'oggetto. Ciò consente che l'oggetto venga ricreato, ma lo stato dell'oggetto non è prevedibile. Per usare un riferimento lungo, specificare `true` nel costruttore [WeakReference](xref:System.WeakReference). 

  Se il tipo dell'oggetto non dispone di un metodo [Finalize](xref:System.Object.Finalize) viene applicata la funzionalità del riferimento debole breve e il riferimento debole è valido solo fino alla raccolta del target, che può verificarsi in qualsiasi momento dopo l'esecuzione del metodo Finalize.

Per stabilire un riferimento sicuro e usare nuovamente l'oggetto, eseguire il cast della proprietà [Target](xref:System.WeakReference.Target) di una classe [WeakReference](xref:System.WeakReference) al tipo dell'oggetto. Se la proprietà [Target](xref:System.WeakReference.Target) restituisce `null` l'oggetto è stato raccolto; in caso contrario è possibile continuare a usare l'oggetto, perché l'applicazione ha recuperato un riferimento sicuro all'oggetto stesso.

## <a name="guidelines-for-using-weak-references"></a>Linee guida per l'uso dei riferimenti deboli

Usare i riferimenti deboli lunghi solo in caso di necessità, perché dopo la finalizzazione lo stato dell'oggetto è imprevedibile. 

Evitare di usare riferimenti deboli a oggetti di piccole dimensioni, poiché il puntatore può avere dimensioni equivalenti o superiori. 

Evitare di usare i riferimenti deboli come soluzione automatica per i problemi di gestione della memoria. In alternativa, sviluppare un criterio di memorizzazione nella cache efficiente per gestire gli oggetti dell'applicazione. 

## <a name="see-also"></a>Vedere anche

[Garbage Collection in .NET](index.md)



<!--HONumber=Nov16_HO3-->


