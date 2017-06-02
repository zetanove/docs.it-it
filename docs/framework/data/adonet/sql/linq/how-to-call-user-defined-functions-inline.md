---
title: "Procedura: chiamare funzioni inline definite dall&#39;utente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f80d4327-b6a5-4aa8-a743-e95d09a2a02e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: chiamare funzioni inline definite dall&#39;utente
Anche se è possibile chiamare le funzioni inline definite dall'utente, le funzioni incluse in una query la cui esecuzione è rinviata non vengono eseguite finche non verrà eseguita la query.  Per altre informazioni, vedere [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md).  
  
 Quando si chiama la stessa funzione al di fuori di una query, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] crea una semplice query dall'espressione della chiamata al metodo.  Di seguito è riportata la sintassi SQL, in cui il parametro `@p0` è associato alla costante passata:  
  
```  
SELECT dbo.ReverseCustName(@p0)  
```  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene creato quanto segue:  
  
 [!code-csharp[DLinqUDFS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/Program.cs#4)]
 [!code-vb[DLinqUDFS#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/Module1.vb#4)]  
  
## Esempio  
 Nella query [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] seguente, è possibile visualizzare una chiamata inline al metodo generato della funzione definita dall'utente `ReverseCustName`.  La funzione non viene eseguita immediatamente poiché l'esecuzione della query è rinviata.  Il codice SQL compilato per questa query viene convertito in una chiamata alla funzione definita dall'utente nel database. Vedere il codice SQL che segue la query.  
  
 [!code-csharp[DLinqUDFS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/Program.cs#5)]
 [!code-vb[DLinqUDFS#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/Module1.vb#5)]  
  
```  
SELECT [t0].[ContactName],  
    dbo.ReverseCustName([t0].[ContactTitle]) AS [Title]  
FROM [Customers] AS [t0]  
```  
  
## Vedere anche  
 [Funzioni definite dall'utente](../../../../../../docs/framework/data/adonet/sql/linq/user-defined-functions.md)