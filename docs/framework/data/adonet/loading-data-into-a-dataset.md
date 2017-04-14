---
title: "Caricamento di dati in un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a53e5dc1-9669-49d4-828d-efa633237066
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Caricamento di dati in un DataSet
Per poter eseguire query su un oggetto <xref:System.Data.DataSet> con [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], è prima necessario popolarlo.  Sono disponibili diversi modi per popolare <xref:System.Data.DataSet>.  Ad esempio, è possibile usare [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] per eseguire una query sul database e caricare i risultati in <xref:System.Data.DataSet>.  Per altre informazioni, vedere [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md).  
  
 Per caricare i dati in <xref:System.Data.DataSet>, è inoltre usare la classe <xref:System.Data.Common.DataAdapter> per recuperare i dati dal database,  come illustrato nell'esempio seguente.  
  
## Esempio  
 In questo esempio viene usato un oggetto <xref:System.Data.Common.DataAdapter> per eseguire una query sul database AdventureWorks relativa alle informazioni sulle vendite dell'anno 2002. I risultati vengono quindi caricati in un oggetto <xref:System.Data.DataSet>.  Dopo aver popolato <xref:System.Data.DataSet>, è possibile scrivere query da eseguire su di esso con [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  Il metodo `FillDataSet` di questo esempio viene usato nelle query di esempio in [Esempi relativi a LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md).  Per altre informazioni, vedere [Esecuzione di query su DataSet](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md).  
  
 [!code-csharp[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#filldataset)]
 [!code-vb[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#filldataset)]  
  
## Vedere anche  
 [Cenni preliminari su LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-overview.md)   
 [Esecuzione di query su DataSet](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [Esempi relativi a LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)