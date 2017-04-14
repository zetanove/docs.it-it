---
title: "Panoramica di BlockingCollection | Microsoft Docs"
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
  - "BlockingCollection, panoramica"
ms.assetid: 987ea3d7-0ad5-4238-8b64-331ce4eb3f0b
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# Panoramica di BlockingCollection
<xref:System.Collections.Concurrent.BlockingCollection%601> è una classe di raccolte thread\-safe che fornisce le funzionalità seguenti:  
  
-   Implementazione del modello producer\-consumer.  
  
-   Aggiunta e rimozione simultanea di elementi da più thread.  
  
-   Capacità massima facoltativa.  
  
-   Operazioni di inserimento e rimozione che si bloccano quando la raccolta è vuota o piena.  
  
-   Operazioni "di tentativo" di inserimento e rimozione che non si bloccano o che si bloccano per un determinato periodo di tempo.  
  
-   Incapsulamento di qualsiasi tipo di raccolta che implementa <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>.  
  
-   Annullamento con i token di annullamento.  
  
-   Due tipi di enumerazione con `foreach` \(`For Each` in Visual Basic\):  
  
    1.  Enumerazione di sola lettura.  
  
    2.  Enumerazione che rimuove gli elementi quando vengono enumerati.  
  
## Supporto di limitazione e blocco  
 <xref:System.Collections.Concurrent.BlockingCollection%601> supporta la limitazione e il blocco.  La limitazione consente di impostare la capacità massima della raccolta.  La limitazione è importante in determinati scenari poiché consente di controllare la dimensione massima della raccolta in memoria. Inoltre, impedisce ai thread di tipo producer di spostarsi troppo oltre i thread di tipo consumer.  
  
 Più thread o attività possono aggiungere contemporaneamente elementi alla raccolta. In tal caso, se viene raggiunta la capacità massima specificata per la raccolta, i thread di tipo producer si bloccheranno finché non viene rimosso un elemento.  Più consumer possono rimuovere contemporaneamente elementi. In tal caso, se la raccolta diventa vuota, i thread di tipo consumer si bloccheranno finché un producer non aggiunge un elemento.  Un thread di tipo producer può chiamare <xref:System.Collections.Concurrent.BlockingCollection%601.CompleteAdding%2A> per indicare che non verranno aggiunti altri elementi.  I consumer monitorano la proprietà <xref:System.Collections.Concurrent.BlockingCollection%601.IsCompleted%2A> per sapere quando la raccolta è vuota e non verranno aggiunti altri elementi.  Nell'esempio seguente viene mostrato un oggetto BlockingCollection semplice con un limite di capacità di 100.  Un'attività di tipo producer aggiunge elementi alla raccolta finché una condizione esterna è vera, quindi chiama <xref:System.Collections.Concurrent.BlockingCollection%601.CompleteAdding%2A>.  L'attività di tipo consumer accetta elementi finché la proprietà <xref:System.Collections.Concurrent.BlockingCollection%601.IsCompleted%2A> non è true.  
  
 [!code-csharp[CDS_BlockingCollection#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/blockingcollection.cs#04)]
 [!code-vb[CDS_BlockingCollection#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/introsnippetsbc.vb#04)]  
  
 Per un esempio completo, vedere [Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-add-and-take-items.md).  
  
## Operazioni di blocco temporizzate  
 Nelle operazioni di blocco temporizzate <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> e <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> sulle raccolte limitate, il metodo tenta di aggiungere o rimuovere un elemento.  Se è disponibile un elemento, questo viene posizionato nella variabile passata per riferimento e il metodo restituisce true.  Se dopo un periodo di timeout specificato non viene recuperato alcun elemento, il metodo restituisce false.  Il thread è quindi libero di fare altre operazioni utili prima di ritentare di accedere alla raccolta.  Per un esempio di accesso con blocco temporizzato, vedere il secondo esempio di [Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-add-and-take-items.md).  
  
## Annullamento di operazioni di aggiunta e rimozione  
 In genere le operazioni di aggiunta e rimozione vengono eseguite in un ciclo.  Per annullare un ciclo è possibile passare un <xref:System.Threading.CancellationToken> al metodo <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> o <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A>, quindi controllare il valore della proprietà <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> del token in ogni iterazione.  Se il valore è true è possibile decidere se rispondere alla richiesta di annullamento pulendo qualsiasi risorsa e uscendo dal ciclo.  Nell'esempio seguente viene illustrato un overload di <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> che accetta un token di annullamento e il codice che lo utilizza:  
  
 [!code-csharp[CDS_BlockingCollection#05](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/blockingcollection.cs#05)]
 [!code-vb[CDS_BlockingCollection#05](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/introsnippetsbc.vb#05)]  
  
 Per un esempio di come aggiungere il supporto per l'annullamento, vedere il secondo esempio di [Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-add-and-take-items.md).  
  
## Specifica del tipo di raccolta  
 Quando si crea un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601>, oltre al limite di capacità è possibile specificare anche il tipo di raccolta da utilizzare.  Ad esempio, è possibile specificare un oggetto <xref:System.Collections.Concurrent.ConcurrentQueue%601> per applicare un comportamento first in\-first out \(FIFO\) o un oggetto <xref:System.Collections.Concurrent.ConcurrentStack%601> per applicare un comportamento last in\-first out \(LIFO\).  È possibile utilizzare una classe di raccolte che implementa l'interfaccia <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>.  Il tipo di raccolta predefinito per <xref:System.Collections.Concurrent.BlockingCollection%601> è <xref:System.Collections.Concurrent.ConcurrentQueue%601>.  Nell'esempio di codice seguente viene mostrato come creare un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601> di stringhe avente una capacità di 1000 e che utilizza un oggetto <xref:System.Collections.Concurrent.ConcurrentBag%601>:  
  
```vb  
Dim bc = New BlockingCollection(Of String)(New ConcurrentBag(Of String()), 1000)  
```  
  
```csharp  
BlockingCollection<string> bc = new BlockingCollection<string>(new ConcurrentBag<string>(), 1000 );  
```  
  
 Per ulteriori informazioni, vedere [Procedura: Aggiungere funzionalità di delimitazione e blocco a una raccolta](../../../../docs/standard/collections/thread-safe/how-to-add-bounding-and-blocking.md).  
  
## Supporto di IEnumerable  
 <xref:System.Collections.Concurrent.BlockingCollection%601> fornisce un metodo <xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A> che consente ai consumer di utilizzare `foreach` \(`For Each` in [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\) per rimuovere elementi fino al completamento della raccolta, ovvero finché non è vuoto e non verranno aggiunti altri elementi.  Per ulteriori informazioni, vedere [Procedura: utilizzare ForEach per rimuovere elementi in un oggetto BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-use-foreach-to-remove.md).  
  
## Utilizzo di molti oggetti BlockingCollections come uno solo  
 Per gli scenari in cui un consumer deve rimuovere elementi simultaneamente da più raccolte è possibile creare matrici di <xref:System.Collections.Concurrent.BlockingCollection%601> e utilizzare i metodi statici quali <xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny%2A> e <xref:System.Collections.Concurrent.BlockingCollection%601.AddToAny%2A> che eseguiranno operazioni di aggiunta o rimozione in qualsiasi raccolta nella matrice.  Se una data raccolta è bloccata, il metodo tenta immediatamente di accedere a un'altra raccolta finché non ne individua una che può eseguire l'operazione.  Per ulteriori informazioni, vedere [Procedura: utilizzare matrici di raccolte di blocco in una pipeline](../../../../docs/standard/collections/thread-safe/how-to-use-arrays-of-blockingcollections.md).  
  
## Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Raccolte e strutture di dati](../../../../docs/standard/collections/index.md)   
 [Raccolte thread\-safe](../../../../docs/standard/collections/thread-safe/index.md)