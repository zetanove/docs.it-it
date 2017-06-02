---
title: "Definizione di chiavi primarie | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2ea85959-e763-4669-8bd9-46a9dab894bd
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Definizione di chiavi primarie
In genere, in una tabella di database è presente una colonna o un gruppo di colonne che consente l'identificazione univoca di ogni riga della tabella.  Tale colonna o gruppo di colonne di identificazione è definito chiave primaria.  
  
 Quando si identifica un singolo tipo <xref:System.Data.DataColumn> come proprietà <xref:System.Data.DataTable.PrimaryKey%2A> per un tipo <xref:System.Data.DataTable>, la proprietà <xref:System.Data.DataColumn.AllowDBNull%2A> della colonna viene automaticamente impostata su **false** e la proprietà <xref:System.Data.DataColumn.Unique%2A> su **true**.  Nel caso di chiavi primarie di più colonne, viene impostata automaticamente su **false** solo la proprietà **AllowDBNull**.  
  
 La proprietà **PrimaryKey** di un tipo <xref:System.Data.DataTable> riceve come valore una matrice contenente uno o più oggetti **DataColumn**, come illustrato negli esempi seguenti.  Il primo esempio consente di definire una singola colonna come chiave primaria.  
  
```vb  
workTable.PrimaryKey = New DataColumn() {workTable.Columns("CustID")}  
  
' Or  
  
Dim columns(1) As DataColumn  
columns(0) = workTable.Columns("CustID")  
workTable.PrimaryKey = columns  
  
```  
  
```csharp  
workTable.PrimaryKey = new DataColumn[] {workTable.Columns["CustID"]};  
  
// Or  
  
DataColumn[] columns = new DataColumn[1];  
columns[0] = workTable.Columns["CustID"];  
workTable.PrimaryKey = columns;  
```  
  
 L'esempio seguente consente di definire due colonne come chiave primaria.  
  
```vb  
workTable.PrimaryKey = New DataColumn() {workTable.Columns("CustLName"), _  
                                         workTable.Columns("CustFName")}  
  
' Or  
  
Dim keyColumn(2) As DataColumn  
keyColumn(0) = workTable.Columns("CustLName")  
keyColumn(1) = workTable.Columns("CustFName")  
workTable.PrimaryKey = keyColumn  
  
```  
  
```csharp  
workTable.PrimaryKey = new DataColumn[] {workTable.Columns["CustLName"],   
                                         workTable.Columns["CustFName"]};  
  
// Or  
  
DataColumn[] keyColumn = new DataColumn[2];  
keyColumn[0] = workTable.Columns["CustLName"];  
keyColumn[1] = workTable.Columns["CustFName"];  
workTable.PrimaryKey = keyColumn;  
```  
  
## Vedere anche  
 <xref:System.Data.DataTable>   
 [Definizione dello schema di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)