---
title: "Formulare join e query di prodotto incrociato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d8072ede-0521-4670-9bec-1778ceeb875b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Formulare join e query di prodotto incrociato
Negli esempi riportati di seguito viene illustrato come combinare risultati da più tabelle.  
  
## Esempio  
 Nell'esempio seguente viene usata la navigazione con chiave esterna nella clausola `From` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] \(la clausola `from` in C\#\) per selezionare tutti gli ordini per i clienti nell'area londinese.  
  
 [!code-csharp[DLinqQueryExamples#47](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#47)]
 [!code-vb[DLinqQueryExamples#47](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#47)]  
  
## Esempio  
 Nell'esempio seguente viene usata la navigazione con chiave esterna nella clausola `Where` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] \(la clausola `where` in C\#\) per filtrare `Products` senza scorta il cui `Supplier` risiede negli Stati Uniti.  
  
 [!code-csharp[DLinqQueryExamples#48](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#48)]
 [!code-vb[DLinqQueryExamples#48](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#48)]  
  
## Esempio  
 Nell'esempio seguente viene usata la navigazione con chiave esterna nella clausola `From` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] \(la clausola `from` in C\#\) per filtrare i dipendenti di Seattle ed elencare i territori.  
  
 [!code-csharp[DLinqQueryExamples#49](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#49)]  
  
## Esempio  
 Nell'esempio seguente viene usata la navigazione con chiave esterna nella clausola `Select` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] \(la clausola `select` in C\#\) per filtrare le coppie di dipendenti in cui un dipendente riporta all'altro ed entrambi sono della stessa `City`.  
  
 [!code-csharp[DLinqQueryExamples#50](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#50)]
 [!code-vb[DLinqQueryExamples#50](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#50)]  
  
## Esempio  
 Nell'esempio di [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] seguente vengono cercati tutti i clienti e gli ordini, viene controllato che gli ordini siano associati ai clienti e viene assicurato che per ogni cliente nell'elenco sia presente un nome del contatto.  
  
 [!code-vb[DLinqQueryExamples#50v](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#50v)]  
  
## Esempio  
 Nell'esempio seguente vengono unite in join in modo esplicito due tabelle e vengono proiettati i risultati da entrambe le tabelle.  
  
 [!code-csharp[DLinqQueryExamples#51](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#51)]
 [!code-vb[DLinqQueryExamples#51](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#51)]  
  
## Esempio  
 Nell'esempio seguente vengono unite in join in modo esplicito tre tabelle e vengono proiettati i risultati da ogni tabella.  
  
 [!code-csharp[DLinqQueryExamples#52](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#52)]
 [!code-vb[DLinqQueryExamples#52](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#52)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come ottenere `LEFT OUTER JOIN` usando `DefaultIfEmpty()`.  Il metodo `DefaultIfEmpty()` restituisce null se non è presente alcun `Order` per `Employee`.  
  
 [!code-csharp[DLinqQueryExamples#53](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#53)]
 [!code-vb[DLinqQueryExamples#53](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#53)]  
  
## Esempio  
 Nell'esempio seguente viene proiettata l'espressione `let` risultante da un join.  
  
 [!code-csharp[DLinqQueryExamples#54](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#54)]
 [!code-vb[DLinqQueryExamples#54](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#54)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato un `join` con una chiave composita.  
  
 [!code-csharp[DLinqQueryExamples#55](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#55)]
 [!code-vb[DLinqQueryExamples#55](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#55)]  
  
## Esempio  
 Nell'esempio seguente viene descritto come costruire un `join` in cui un solo lato è nullable.  
  
 [!code-csharp[DLinqQueryExamples#56](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#56)]
 [!code-vb[DLinqQueryExamples#56](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#56)]  
  
## Vedere anche  
 [Esempi di query](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)