---
title: "Raggruppare gli elementi in una sequenza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d50c8b4-f550-4775-bbb6-eab6e874cb43
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Raggruppare gli elementi in una sequenza
L'operatore <xref:System.Linq.Enumerable.GroupBy%2A> consente di raggruppare gli elementi di una sequenza.  Negli esempi riportati di seguito viene usato il database Northwind.  
  
> [!NOTE]
>  I valori di colonna null nelle query <xref:System.Linq.Enumerable.GroupBy%2A> possono a volte generare una <xref:System.InvalidOperationException>.  Per altre informazioni, vedere la sezione relativa all'eccezione InvalidOperationException di GroupBy in [Risoluzione dei problemi](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md).  
  
## Esempio  
 Nell'esempio riportato di seguito `Products` viene partizionato per `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#27](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#27)]
 [!code-vb[DLinqQueryExamples#27](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#27)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene usata <xref:System.Linq.Enumerable.Max%2A> per trovare il prezzo unitario massimo per ogni `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#28](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#28)]
 [!code-vb[DLinqQueryExamples#28](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#28)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene usata la funzione Average per trovare la media di `UnitPrice` per ogni `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#29](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#29)]
 [!code-vb[DLinqQueryExamples#29](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#29)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene usata <xref:System.Linq.Queryable.Sum%2A> per trovare il totale di `UnitPrice` per ogni `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#30](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#30)]
 [!code-vb[DLinqQueryExamples#30](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#30)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene usata <xref:System.Linq.Queryable.Count%2A> per trovare il numero di `Products` rimossi in ogni `CategoryID`.  
  
 [!code-csharp[DLinqQueryExamples#31](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#31)]
 [!code-vb[DLinqQueryExamples#31](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#31)]  
  
## Esempio  
 Negli esempi riportati di seguito viene usata la clausola `where` seguente per trovare tutte le categorie con almeno 10 prodotti.  
  
 [!code-csharp[DLinqQueryExamples#32](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#32)]
 [!code-vb[DLinqQueryExamples#32](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#32)]  
  
## Esempio  
 Nell'esempio riportato di seguito i prodotti vengono raggruppati per `CategoryID` e `SupplierID`.  
  
 [!code-csharp[DLinqQueryExamples#33](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#33)]
 [!code-vb[DLinqQueryExamples#33](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#33)]  
  
## Esempio  
 Nell'esempio riportato di seguito vengono restituite due sequenze di prodotti.  La prima sequenza contiene prodotti con prezzo unitario minore o uguale a 10.  La seconda sequenza contiene prodotti con prezzo unitario maggiore di 10.  
  
 [!code-csharp[DLinqQueryExamples#34](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#34)]
 [!code-vb[DLinqQueryExamples#34](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#34)]  
  
## Esempio  
 L'operatore <xref:System.Linq.Queryable.GroupBy%2A> può accettare solo un argomento a chiave singola.  Se è necessario raggruppare in base a più chiavi, è necessario creare un tipo anonimo, come nell'esempio seguente:  
  
 [!code-csharp[DLinqQueryExamples#35](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#35)]
 [!code-vb[DLinqQueryExamples#35](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#35)]  
  
## Vedere anche  
 [Esempi di query](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)   
 [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)