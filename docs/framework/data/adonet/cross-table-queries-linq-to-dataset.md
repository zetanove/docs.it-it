---
title: "Query tra tabelle (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6819a16f-8656-41af-a54d-dfec0cb66366
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Query tra tabelle (LINQ to DataSet)
Oltre alle query su singola tabella, è possibile eseguire query tra tabelle in [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] utilizzando un *join*.  Per join si intende l'associazione degli oggetti di un'origine dati con oggetti di un'altra origine dati che condividono un attributo comune, ad esempio un ID prodotto o contatto.  Nella programmazione orientata a oggetti, lo spostamento nelle relazioni tra oggetti è relativamente semplice, perché ogni oggetto include un membro che fa riferimento a un altro oggetto. Nelle tabelle di database esterne, tuttavia, lo spostamento nelle relazioni non è un processo così semplice.  Le tabelle di database non contengono relazioni predefinite. In questi casi, l'operazione di join può essere usata per far corrispondere gli elementi di ogni origine.  Ad esempio, date due tabelle contenenti informazioni sui prodotti e sulle vendite, è possibile usare un'operazione join per creare una corrispondenza tra le informazioni sulle vendite e i prodotti relativi allo stesso ordine di vendita.  
  
 Nel framework [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] sono disponibili due operatori di join, <xref:System.Linq.Enumerable.Join%2A> e <xref:System.Linq.Enumerable.GroupJoin%2A>. Questi operatori eseguono *equijoin*, ossia join che creano una corrispondenza tra due origini dati solo quando le relative chiavi sono uguali.  Al contrario, in [!INCLUDE[tsql](../../../../includes/tsql-md.md)] sono supportati operatori di join diversi da `equals`, ad esempio l'operatore `less than`.  
  
 In termini di database relazionale, il metodo <xref:System.Linq.Enumerable.Join%2A> implementa un inner join.  Un inner join è un tipo di join in cui vengono restituiti solo gli oggetti che dispongono di una corrispondenza nel set di dati opposto.  
  
 Gli operatori <xref:System.Linq.Enumerable.GroupJoin%2A> non dispongono di equivalenti diretti in termini di database relazionale; essi implementano un superset di inner join e left outer join. Un left outer join è un join che restituisce ogni elemento della prima raccolta \(a sinistra\), anche se non ha elementi correlati nella seconda raccolta.  
  
 Per altre informazioni sui join, vedere [Join Operations](../../../../ocs/visual-basic/programming-guide/concepts/linq/join-operations.md).  
  
## Esempio  
 Nell'esempio seguente viene eseguito un join tradizionale delle tabelle `SalesOrderHeader` e `SalesOrderDetail` del database di esempio AdventureWorks per ottenere gli ordini effettuati online dal mese di agosto.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Join](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#join)]
 [!code-vb[DP LINQ to DataSet Examples#Join](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#join)]  
  
## Vedere anche  
 [Esecuzione di query su DataSet](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [Query su una singola tabella](../../../../docs/framework/data/adonet/single-table-queries-linq-to-dataset.md)   
 [Esecuzione di query su DataSet tipizzati](../../../../docs/framework/data/adonet/querying-typed-datasets.md)   
 [Join Operations](../../../../ocs/visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [Esempi relativi a LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)