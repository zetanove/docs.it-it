---
title: "Restituire o ignorare gli elementi in una sequenza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 81a31acd-e0f1-4bca-9a12-fa1ad5752374
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Restituire o ignorare gli elementi in una sequenza
Usare l'operatore <xref:System.Linq.Queryable.Take%2A> per restituire un numero specificato di elementi in una sequenza e ignorare quindi gli elementi rimanenti.  
  
 Usare l'operatore <xref:System.Linq.Queryable.Skip%2A> per ignorare un numero specificato di elementi in una sequenza, quindi restituire gli elementi rimanenti.  
  
> [!NOTE]
>  <xref:System.Linq.Enumerable.Take%2A> e <xref:System.Linq.Enumerable.Skip%2A> presentano alcune limitazioni quando vengono usati nelle query su SQL Server 2000.  Per altre informazioni, vedere la voce relativa alle eccezioni di Skip e Take in SQL Server 2000 in [Risoluzione dei problemi](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] converte <xref:System.Linq.Queryable.Skip%2A> usando una sottoquery con la clausola SQL `NOT EXISTS`.  Di seguito vengono elencate le limitazioni di questa conversione.  
  
-   L'argomento deve essere un set.  I tipi multiset non sono supportati, anche se ordinati.  
  
-   La query generata può essere molto più complessa di quella generata per la query di base a cui viene applicato <xref:System.Linq.Queryable.Skip%2A>.  Questa complessità può provocare una riduzione delle prestazioni o il timeout dell'operazione.  
  
## Esempio  
 Nell'esempio seguente viene usato `Take` per selezionare i primi cinque dipendenti assunti in `Employees`.  Notare che la raccolta viene prima ordinata per `HireDate`.  
  
 [!code-csharp[DLinqQueryExamples#16](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#16)]
 [!code-vb[DLinqQueryExamples#16](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#16)]  
  
## Esempio  
 Nell'esempio seguente viene usato <xref:System.Linq.Queryable.Skip%2A> per selezionare tutti i prodotti tranne i 10 più costosi nella tabella `Products`.  
  
 [!code-csharp[DLinqQueryExamples#17](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#17)]
 [!code-vb[DLinqQueryExamples#17](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#17)]  
  
## Esempio  
 Nell'esempio seguente vengono combinati i metodi <xref:System.Linq.Queryable.Skip%2A> e <xref:System.Linq.Queryable.Take%2A> per ignorare i primi 50 record e restituire quindi i 10 successivi.  
  
 [!code-csharp[DLinqQueryExamples#18](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#18)]
 [!code-vb[DLinqQueryExamples#18](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#18)]  
  
 Le operazioni <xref:System.Linq.Queryable.Take%2A> e <xref:System.Linq.Queryable.Skip%2A> sono definite correttamente solo per i set ordinati,  mentre la semantica per i set non ordinati o i tipi multiset non è definita.  
  
 A causa delle limitazioni relative all'ordinamento in SQL, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tenta di spostare l'ordinamento dell'argomento dell'operatore <xref:System.Linq.Queryable.Take%2A> o <xref:System.Linq.Queryable.Skip%2A> nel risultato dell'operatore.  
  
> [!NOTE]
>  La conversione è diversa per [!INCLUDE[ss2k](../../../../../../includes/ss2k-md.md)] e [!INCLUDE[sqprsqlong](../../../../../../includes/sqprsqlong-md.md)].  Se si prevede di usare <xref:System.Linq.Queryable.Skip%2A> con una query di qualsiasi complessità, usare [!INCLUDE[sqprsqlong](../../../../../../includes/sqprsqlong-md.md)].  
  
 Considerare la query [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] seguente per [!INCLUDE[ss2k](../../../../../../includes/ss2k-md.md)]:  
  
 [!code-csharp[DLinqQueryExamples#19](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#19)]
 [!code-vb[DLinqQueryExamples#19](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#19)]  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sposta l'ordinamento alla fine nel codice SQL, come segue:  
  
```  
SELECT TOP 1 [t0].[CustomerID], [t0].[CompanyName],  
FROM [Customers] AS [t0]  
WHERE (NOT (EXISTS(  
    SELECT NULL AS [EMPTY]  
    FROM (  
        SELECT TOP 1 [t1].[CustomerID]  
        FROM [Customers] AS [t1]  
        WHERE [t1].[City] = @p0  
        ORDER BY [t1].[CustomerID]  
        ) AS [t2]  
    WHERE [t0].[CustomerID] = [t2].[CustomerID]  
    ))) AND ([t0].[City] = @p1)  
ORDER BY [t0].[CustomerID]  
```  
  
 Quando <xref:System.Linq.Queryable.Take%2A> e <xref:System.Linq.Queryable.Skip%2A> sono concatenati, tutti i tipi di ordinamento specificati devono essere coerenti.  In caso contrario i risultati non saranno definiti.  
  
 Per gli argomenti di tipo integrale costante non negativi, basati sulla specifica SQL, <xref:System.Linq.Queryable.Take%2A> e <xref:System.Linq.Queryable.Skip%2A> sono definiti correttamente.  
  
## Vedere anche  
 [Esempi di query](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md)   
 [Conversione dell'operatore di query standard](../../../../../../docs/framework/data/adonet/sql/linq/standard-query-operator-translation.md)