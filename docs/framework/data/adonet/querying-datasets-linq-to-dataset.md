---
title: "Esecuzione di query su DataSet (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bb68d2e4-623d-4d60-85e3-965254f6fee7
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Esecuzione di query su DataSet (LINQ to DataSet)
È possibile iniziare a eseguire query su un oggetto <xref:System.Data.DataSet> dopo averlo popolato con i dati.  La formulazione di query con [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] è simile all'utilizzo di [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] su altre origini dati con supporto [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)].  Tenere tuttavia presente che quando si usano query [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] su un oggetto <xref:System.Data.DataSet>, si esegue una query su un'enumerazione di oggetti <xref:System.Data.DataRow>, anziché su un'enumerazione di un tipo personalizzato.  È quindi possibile usare nelle query [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] tutti i membri della classe <xref:System.Data.DataRow> e creare query dettagliate e complesse.  
  
 Come con altre implementazioni di [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)], è possibile creare query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] in due formati diversi, ovvero usando la sintassi delle espressioni di query e la sintassi delle query basate su metodo.  Per altre informazioni su questi due formati, vedere [Getting Started with LINQ](http://msdn.microsoft.com/it-it/6cc9af04-950a-4cc3-83d4-2aeb4abe4de9). È possibile usare la sintassi delle espressioni di query o la sintassi delle query basate su metodo per eseguire query su singole tabelle di <xref:System.Data.DataSet>, più tabelle di <xref:System.Data.DataSet> o tabelle di oggetti <xref:System.Data.DataSet> tipizzati.  
  
## Contenuto della sezione  
 [Query su una singola tabella](../../../../docs/framework/data/adonet/single-table-queries-linq-to-dataset.md)  
 Viene descritto come eseguire query su una singola tabella.  
  
 [Query tra tabelle](../../../../docs/framework/data/adonet/cross-table-queries-linq-to-dataset.md)  
 Viene descritto come eseguire query tra tabelle.  
  
 [Esecuzione di query su DataSet tipizzati](../../../../docs/framework/data/adonet/querying-typed-datasets.md)  
 Viene descritto come eseguire una query su oggetti <xref:System.Data.DataSet> tipizzati.  
  
## Vedere anche  
 [Esempi relativi a LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)   
 [Caricamento di dati in un DataSet](../../../../docs/framework/data/adonet/loading-data-into-a-dataset.md)