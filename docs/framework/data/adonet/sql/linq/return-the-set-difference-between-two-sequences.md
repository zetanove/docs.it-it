---
title: "Restituire la differenza di set tra due sequenze | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 62efb546-c898-408f-af21-36e7c6fed217
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Restituire la differenza di set tra due sequenze
Per restituire la differenza dei set tra due sequenze, usare l'operatore <xref:System.Linq.Queryable.Except%2A>.  
  
## Esempio  
 In questo esempio viene usato <xref:System.Linq.Queryable.Except%2A> per restituire una sequenza di tutti i paesi in cui sono presenti `Customers` ma non `Employees`.  
  
 [!code-csharp[DLinqQueryExamples#41](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#41)]
 [!code-vb[DLinqQueryExamples#41](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#41)]  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] l'operazione <xref:System.Linq.Queryable.Except%2A> è definita correttamente solo sui set,  mentre la semantica per i tipi multiset non è definita.  
  
## Vedere anche  
 [Esempi di query](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)   
 [Conversione dell'operatore di query standard](../../../../../../docs/framework/data/adonet/sql/linq/standard-query-operator-translation.md)