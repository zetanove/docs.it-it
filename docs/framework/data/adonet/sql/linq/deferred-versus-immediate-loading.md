---
title: "Caricamento rinviato e immediato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d1d7247f-a3b7-460b-b342-5c1a2365aa1a
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Caricamento rinviato e immediato
Quando si esegue una query per un oggetto, si recupera in effetti solo l'oggetto richiesto.  Gli oggetti *correlati* non vengono recuperati contemporaneamente in modo automatico.  Per altre informazioni, vedere [Esecuzione di query tra relazioni](../../../../../../docs/framework/data/adonet/sql/linq/querying-across-relationships.md). Non è possibile verificare che gli oggetti correlati non siano già stati caricati, perché un tentativo di accedervi produce una richiesta che ne comporta il recupero.  
  
 Ad esempio, è possibile eseguire una query per un particolare set di ordini, quindi inviare saltuariamente un avviso tramite posta elettronica a clienti particolari.  Inizialmente potrebbe non essere necessario recuperare tutti i dati del cliente con ogni ordine.  In questo caso è possibile usare il caricamento posticipato per rinviare il recupero di informazioni aggiuntive finché non sarà assolutamente necessario.  Si consideri l'esempio seguente:  
  
 [!code-csharp[DLinqQueryConcepts#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#1)]
 [!code-vb[DLinqQueryConcepts#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#1)]  
  
 Potrebbe anche essere vero il contrario.  Si dispone di un'applicazione che richiede la visualizzazione contemporanea dei dati dei clienti e degli ordini.  È noto che sono necessari entrambi i set di dati  e che l'applicazione richiede informazioni sugli ordini per ogni cliente non appena vengono restituiti i risultati.  Non si desidera inviare singole query per gli ordini di ogni cliente,  bensì recuperare i dati degli ordini insieme ai clienti.  
  
 [!code-csharp[DLinqQueryConcepts#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#2)]
 [!code-vb[DLinqQueryConcepts#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#2)]  
  
 È inoltre possibile creare un join tra clienti e ordini in una query definendo il prodotto incrociato e recuperando tutti i relativi bit di dati come un'unica grande proiezione.  Tali risultati non sono tuttavia entità.  Per altre informazioni, vedere [Il modello a oggetti LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md).  Le entità sono oggetti con un'identità che è possibile modificare, mentre i risultati in questione sono proiezioni che non possono essere modificate né salvate in modo permanente.  È inoltre possibile che vengano recuperati molti dati ridondanti, in quanto ogni cliente viene ripetuto per ogni ordine nell'output del join bidimensionale.  
  
 È invece utile disporre di un modo per recuperare contemporaneamente un set di oggetti correlati.  Il set è una sezione delineata di un grafico che consente di recuperare sempre solo la quantità di dati necessaria per l'uso desiderato.  A questo scopo in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è disponibile <xref:System.Data.Linq.DataLoadOptions> che consente il caricamento immediato di una parte del modello a oggetti.  I metodi comprendono:  
  
-   Il metodo <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> per caricare immediatamente dati relativi alla destinazione principale.  
  
-   Il metodo <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> per filtrare gli oggetti recuperati per una determinata relazione.  
  
## Vedere anche  
 [Concetti relativi alle query](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)