---
title: "Concatenare due sequenze | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 76767e7c-0607-4e1d-9ca2-a94f311f45eb
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Concatenare due sequenze
Usare l'operatore <xref:System.Linq.Queryable.Concat%2A> per concatenare due sequenze.  
  
 L'operatore <xref:System.Linq.Queryable.Concat%2A> viene definito per multiset ordinati in cui gli ordini del ricevente e dell'argomento sono gli stessi.  
  
 L'ordinamento in SQL è il passaggio finale prima della generazione dei risultati.  Per questo motivo l'operatore <xref:System.Linq.Queryable.Concat%2A> viene implementato usando `UNION ALL` e non mantiene l'ordine dei relativi argomenti.  Per essere certi che l'ordine nei risultati sia corretto, ordinarli in modo esplicito.  
  
## Esempio  
 In questo esempio viene usato <xref:System.Linq.Queryable.Concat%2A> per restituire una sequenza di tutti i numeri di telefono e di fax relativi a `Customer` e `Employee`.  
  
 [!code-csharp[DLinqQueryExamples#39](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#39)]
 [!code-vb[DLinqQueryExamples#39](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#39)]  
  
## Esempio  
 In questo esempio viene usato <xref:System.Linq.Queryable.Concat%2A> per restituire una sequenza di tutti i mapping di nomi e numeri di telefono relativi a `Customer` e `Employee`.  
  
 [!code-csharp[DLinqQueryExamples#40](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#40)]
 [!code-vb[DLinqQueryExamples#40](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#40)]  
  
## Vedere anche  
 [Esempi di query](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)   
 [Conversione dell'operatore di query standard](../../../../../../docs/framework/data/adonet/sql/linq/standard-query-operator-translation.md)