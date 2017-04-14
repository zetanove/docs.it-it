---
title: "Procedura: Implementare un provider | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "schema progettuale observer [.NET Framework], implementazione di provider"
  - "provider [.NET Framework], in schema progettuale observer"
  - "observable [.NET Framework], in schema progettuale observer"
ms.assetid: 790b5d8b-d546-40a6-beeb-151b574e5ee5
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: Implementare un provider
Il modello di progettazione osservatore richiede una divisione tra un provider, che consente di monitorare i dati e inviare notifiche, e uno o più osservatori, che ricevono le notifiche \(callback\) dal provider.  In questo argomento viene illustrato come creare un provider.  In un argomento correlato, [Procedura: Implementare un elemento Observer](../../../docs/standard/events/how-to-implement-an-observer.md), viene illustrato come creare un osservatore.  
  
### Per creare un provider  
  
1.  Definire i dati che dovranno essere inviati dal provider agli osservatori.  Sebbene il provider e i dati inviati agli osservatori possano anche essere di un solo tipo, in genere sono rappresentati da tipi diversi.  In un'applicazione di monitoraggio della temperatura, ad esempio, la struttura `Temperature` definisce i dati che devono essere monitorati dal provider \(che è rappresentato dalla classe `TemperatureMonitor` definita nel passaggio successivo\) e che vengono sottoscritti dagli osservatori.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/data.cs#1)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/data.vb#1)]  
  
2.  Definire il provider di dati, che è un tipo che implementa l'interfaccia <xref:System.IObservable%601?displayProperty=fullName>.  L'argomento di tipo generico del provider è il tipo che il provider invia agli osservatori.  Nell'esempio seguente viene definita una classe `TemperatureMonitor`, che costituisce un'implementazione di <xref:System.IObservable%601?displayProperty=fullName> costruita con un argomento di tipo generico di `Temperature`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#2)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#2)]  
  
3.  Determinare come verranno archiviati i riferimenti agli osservatori dal provider, in modo da poter inviare una notifica a ogni osservatore, quando necessario.  Nella maggior parte dei casi, a questo scopo viene utilizzato un oggetto Collection, ad esempio un oggetto <xref:System.Collections.Generic.List%601>.  Nell'esempio seguente viene definito un oggetto <xref:System.Collections.Generic.List%601> privato di cui viene creata un'istanza nel costruttore della classe `TemperatureMonitor`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#3)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#3)]  
  
4.  Definire un'implementazione di <xref:System.IDisposable> che il provider possa restituire ai sottoscrittori in modo che possano smettere di ricevere notifiche in qualsiasi momento.  Nell'esempio seguente viene definita una classe `Unsubscriber` annidata a cui viene passato un riferimento alla raccolta di sottoscrittori e al sottoscrittore quando viene creata un'istanza della classe.  Questo codice consente al sottoscrittore di chiamare l'implementazione di <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> dell'oggetto per rimuovere se stesso dalla raccolta di sottoscrittori.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#4)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#4)]  
  
5.  Implementare il metodo <xref:System.IObservable%601.Subscribe%2A?displayProperty=fullName>.  Al metodo viene passato un riferimento all'interfaccia <xref:System.IObserver%601?displayProperty=fullName> e il metodo deve essere archiviato nell'oggetto progettato per questo scopo nel passaggio 3.  Il metodo deve quindi restituire l'implementazione di <xref:System.IDisposable> sviluppata nel passaggio 4.  Nell'esempio seguente viene illustrata l'implementazione del metodo <xref:System.IObservable%601.Subscribe%2A> nella classe `TemperatureMonitor`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#5)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#5)]  
  
6.  Inviare agli osservatori una notifica quando appropriato chiamando le relative implementazioni di <xref:System.IObserver%601.OnNext%2A?displayProperty=fullName>, <xref:System.IObserver%601.OnError%2A?displayProperty=fullName> e di <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName>.  In alcuni casi, un provider non può chiamare il metodo <xref:System.IObserver%601.OnError%2A> quando si verifica un errore.  Il metodo `GetTemperature` seguente simula ad esempio uno strumento di monitoraggio che legge i dati della temperatura ogni cinque secondi e invia una notifica agli osservatori se la temperatura è cambiata di almeno 0,1 gradi rispetto alla lettura precedente.  Se il dispositivo non segnala una temperatura \(ovvero, se il valore è null\), il provider invia agli osservatori una notifica per segnalare che la trasmissione è completa.  Si noti che, oltre a chiamare il metodo <xref:System.IObserver%601.OnCompleted%2A> di ogni osservatore, il metodo `GetTemperature` cancella la raccolta <xref:System.Collections.Generic.List%601>.  In questo caso, il provider non fa alcuna chiamata al metodo <xref:System.IObserver%601.OnError%2A> dei suoi osservatori.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#6)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#6)]  
  
## Esempio  
 Nell'esempio seguente è incluso il codice sorgente completo per la definizione di un'implementazione di <xref:System.IObservable%601> per un'applicazione di monitoraggio della temperatura.  Sono incluse la struttura `Temperature`, ovvero i dati inviati agli osservatori, e la classe `TemperatureMonitor`, che rappresenta l'implementazione di <xref:System.IObservable%601>.  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#7)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#7)]  
  
## Vedere anche  
 <xref:System.IObservable%601>   
 [Modello di progettazione observer](../../../docs/standard/events/observer-design-pattern.md)   
 [Procedura: Implementare un elemento Observer](../../../docs/standard/events/how-to-implement-an-observer.md)   
 [Procedure consigliate per un modello di progettazione observer](../../../docs/standard/events/observer-design-pattern-best-practices.md)