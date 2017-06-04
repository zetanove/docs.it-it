---
title: "Esempi di operatori specifici del DataSet (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fdd64af-6ad0-46cd-91c8-dbe26620eeb1
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Esempi di operatori specifici del DataSet (LINQ to DataSet)
Negli esempi di questo argomento viene illustrato l'uso del metodo <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> e della classe <xref:System.Data.DataRowComparer>.  
  
 Il metodo `FillDataSet` usato in questi esempi viene specificato in [Caricamento di dati in un DataSet](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md).  
  
 Negli esempi di questo argomento vengono usate le tabelle Contact, Address, Product, SalesOrderHeader e SalesOrderDetail del database di esempio AdventureWorks.  
  
 Negli esempi di questo argomento vengono usate le istruzioni `using`\/`Imports` seguenti:  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 Per altre informazioni, vedere [Procedura: creare un progetto LINQ to DataSet in Visual Studio](../../../../docs/framework/data/adonet/how-to-create-a-linq-to-dataset-project-in-vs.md).  
  
## CopyToDataTable  
  
### Esempio  
 In questo esempio viene caricato un oggetto <xref:System.Data.DataTable> con i risultati della query usando il metodo <xref:System.Data.DataTableExtensions.CopyToDataTable%2A>.  
  
 [!code-csharp[DP LINQ to DataSet Examples#LoadDataTableWithQueryResults](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#loaddatatablewithqueryresults)]
 [!code-vb[DP LINQ to DataSet Examples#LoadDataTableWithQueryResults](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#loaddatatablewithqueryresults)]  
  
```  
  
```  
  
## DataRowComparer  
  
### Esempio  
 In questo esempio vengono confrontate due righe di dati diverse usando <xref:System.Data.DataRowComparer>.  
  
 [!code-csharp[DP LINQ to DataSet Examples#CompareDifferentDataRows](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#comparedifferentdatarows)]  
  
## Vedere anche  
 [Caricamento di dati in un DataSet](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md)   
 [Esempi relativi a LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)