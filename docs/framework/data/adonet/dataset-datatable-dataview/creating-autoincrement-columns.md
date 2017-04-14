---
title: "Creazione di colonne AutoIncrement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf09732a-ab54-4d98-89e2-4d0a1f28fbce
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Creazione di colonne AutoIncrement
Per assicurarsi che i valori contenuti in una colonna siano univoci, è possibile impostare l'incremento automatico dei valori di colonna a ogni aggiunta di nuove colonne alla tabella.  Per creare un <xref:System.Data.DataColumn> a incremento automatico, impostare la proprietà <xref:System.Data.DataColumn.AutoIncrement%2A> della colonna su **true**.  Il valore iniziale di <xref:System.Data.DataColumn> corrisponderà al valore definito nella proprietà <xref:System.Data.DataColumn.AutoIncrementSeed%2A> e a ogni aggiunta di riga il valore presente nella colonna **AutoIncrement** aumenterà in base al valore contenuto nella proprietà <xref:System.Data.DataColumn.AutoIncrementStep%2A> della colonna.  
  
 Per le colonne **AutoIncrement** si consiglia di impostare su **true** la proprietà <xref:System.Data.DataColumn.ReadOnly%2A> di **DataColumn**.  
  
 Nell'esempio seguente viene illustrato come creare una colonna con valore iniziale pari a 200 e con incrementi in 3 passaggi.  
  
```vb  
Dim workColumn As DataColumn = workTable.Columns.Add( _  
    "CustomerID", typeof(Int32))  
workColumn.AutoIncrement = true  
workColumn.AutoIncrementSeed = 200  
workColumn.AutoIncrementStep = 3  
  
```  
  
```csharp  
DataColumn workColumn = workTable.Columns.Add(  
    "CustomerID", typeof(Int32));  
workColumn.AutoIncrement = true;  
workColumn.AutoIncrementSeed = 200;  
workColumn.AutoIncrementStep = 3;  
```  
  
## Vedere anche  
 <xref:System.Data.DataColumn>   
 [Definizione dello schema di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)