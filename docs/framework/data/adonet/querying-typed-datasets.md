---
title: "Esecuzione di query su DataSet tipizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad712fa1-2baf-462a-b163-574cce6d376a
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Esecuzione di query su DataSet tipizzati
Se si conosce lo schema di <xref:System.Data.DataSet> in fase di progettazione dell'applicazione, è consigliabile usare <xref:System.Data.DataSet> tipizzati con [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  Un oggetto <xref:System.Data.DataSet> tipizzato è una classe che deriva da <xref:System.Data.DataSet>.  In quanto tale, tale oggetto eredita tutti i metodi, gli eventi e le proprietà di un <xref:System.Data.DataSet>.  Un <xref:System.Data.DataSet> tipizzato fornisce inoltre metodi, eventi e proprietà fortemente tipizzati.  È quindi possibile accedere a tabelle e colonne in base al nome, anziché usare metodi basati su raccolta.  Le query risultano quindi più semplici e più leggibili.  Per altre informazioni, vedere [DataSet tipizzati](../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md).  
  
 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)]supporta inoltre l'esecuzione di query su <xref:System.Data.DataSet> tipizzati.  Con un oggetto <xref:System.Data.DataSet> tipizzato non è necessario usare il metodo <xref:System.Data.DataRowExtensions.Field%2A> generico o il metodo <xref:System.Data.DataRowExtensions.SetField%2A> per accedere ai dati della colonna.  I nomi di proprietà sono disponibili in fase di compilazione perché le informazioni sul tipo sono incluse in <xref:System.Data.DataSet>. [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] fornisce accesso ai valori della colonna come tipo corretto, pertanto gli errori di mancata corrispondenza dei tipi vengono intercettati durante la compilazione del codice anziché in fase di esecuzione.  
  
 Prima di iniziare a eseguire query su un oggetto <xref:System.Data.DataSet> tipizzato, è necessario generare la classe usando Progettazione DataSet in [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  Per altre informazioni, vedere [Procedura: creare un dataset tipizzato](../Topic/Create%20and%20configure%20datasets%20in%20Visual%20Studio.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrata una query su un oggetto <xref:System.Data.DataSet> tipizzato.  
  
```csharp  
var query = from o in orders  
            where o.OnlineOrderFlag == true  
            select new { o.SalesOrderID,  
                         o.OrderDate,  
                         o.SalesOrderNumber };  
  
foreach(var order in query)   
{  
    Console.WriteLine("{0}\t{1:d}\t{2}",   
order.SalesOrderID,   
order.OrderDate,   
order.SalesOrderNumber);  
}  
```  
  
```vb  
Dim orders = ds.Tables("SalesOrderHeader")  
  
Dim query = _  
       From o In orders _  
       Where o.OnlineOrderFlag = True _  
       Select New {SalesOrderID := o.SalesOrderID, _  
                   OrderDate := o.OrderDate, _  
                   SalesOrderNumber := o.SalesOrderNumber}  
  
For Each Dim onlineOrder In query  
 Console.WriteLine("{0}\t{1:d}\t{2}", _  
 onlineOrder.SalesOrderID, _  
 onlineOrder.OrderDate, _  
 onlineOrder.SalesOrderNumber)  
Next  
```  
  
## Vedere anche  
 [Esecuzione di query su DataSet](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [Query tra tabelle](../../../../docs/framework/data/adonet/cross-table-queries-linq-to-dataset.md)   
 [Query su una singola tabella](../../../../docs/framework/data/adonet/single-table-queries-linq-to-dataset.md)