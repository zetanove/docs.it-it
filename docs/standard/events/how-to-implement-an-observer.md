---
title: "Procedura: Implementare un elemento Observer | Microsoft Docs"
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
  - "observer [.NET Framework], schema progettuale"
  - "schema progettuale observer [.NET Framework], implementazione di observer"
ms.assetid: 8ecfa9f5-b500-473d-bcf0-5652ffb1e53d
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: Implementare un elemento Observer
Il modello di progettazione osservatore richiede una divisione tra un osservatore, che effettua la registrazione per le notifiche, e un provider, che consente di monitorare i dati e inviare notifiche a uno o più osservatori.  In questo argomento viene illustrato come creare un osservatore.  In un argomento correlato, [Procedura: Implementare un provider](../../../docs/standard/events/how-to-implement-a-provider.md), viene illustrato come creare un provider.  
  
### Per creare un osservatore  
  
1.  Definire l'osservatore, che è un tipo che implementa l'interfaccia <xref:System.IObserver%601?displayProperty=fullName>.  Nel codice seguente viene ad esempio definito un tipo denominato `TemperatureReporter`, che costituisce un'implementazione di <xref:System.IObserver%601?displayProperty=fullName> costruita con un argomento di tipo generico di `Temperature`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#8)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#8)]  
  
2.  Se l'osservatore può smettere di ricevere notifiche prima che il provider chiami la relativa implementazione di <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName>, definire una variabile privata che conterrà l'implementazione di <xref:System.IDisposable> restituita dal metodo <xref:System.IObservable%601.Subscribe%2A?displayProperty=fullName> del provider.  È inoltre necessario definire un metodo di sottoscrizione che chiami il metodo <xref:System.IObservable%601.Subscribe%2A> del provider e archivi l'oggetto <xref:System.IDisposable> restituito.  Il codice seguente, ad esempio, consente di definire una variabile privata denominata `unsubscriber` e un metodo `Subscribe` che chiama il metodo <xref:System.IObservable%601.Subscribe%2A> del provider e assegna l'oggetto restituito alla variabile `unsubscriber`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#9)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#9)]  
  
3.  Definire un metodo che consenta all'osservatore di interrompere la ricezione delle notifiche prima che il provider chiami la relativa implementazione di <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName>, se questa funzionalità è necessaria.  Nell'esempio seguente viene definito un metodo `Unsubscribe`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#10)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#10)]  
  
4.  Fornire le implementazioni dei tre metodi definiti dall'interfaccia <xref:System.IObserver%601>: <xref:System.IObserver%601.OnNext%2A?displayProperty=fullName>, <xref:System.IObserver%601.OnError%2A?displayProperty=fullName> e <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName>.  A seconda del provider e delle esigenze dell'applicazione, i metodi <xref:System.IObserver%601.OnError%2A> e <xref:System.IObserver%601.OnCompleted%2A> possono essere implementazioni dello stub.  Si noti che il metodo <xref:System.IObserver%601.OnError%2A> non può gestire l'oggetto <xref:System.Exception> passato come eccezione e il metodo <xref:System.IObserver%601.OnCompleted%2A> è libero di chiamare l'implementazione di <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> del provider.  Nell'esempio seguente viene illustrata l'implementazione di <xref:System.IObserver%601> della classe `TemperatureReporter`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#11)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#11)]  
  
## Esempio  
 Nell'esempio seguente è incluso il codice sorgente completo per la classe `TemperatureReporter`, che fornisce l'implementazione di <xref:System.IObserver%601> per un'applicazione di monitoraggio della temperatura.  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#12)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#12)]  
  
## Vedere anche  
 <xref:System.IObserver%601>   
 [Modello di progettazione observer](../../../docs/standard/events/observer-design-pattern.md)   
 [Procedura: Implementare un provider](../../../docs/standard/events/how-to-implement-a-provider.md)   
 [Procedure consigliate per un modello di progettazione observer](../../../docs/standard/events/observer-design-pattern-best-practices.md)