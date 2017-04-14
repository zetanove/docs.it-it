---
title: "Creazione di colonne di espressioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0af3bd64-92a2-4b47-ae62-f5df35f131a6
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Creazione di colonne di espressioni
È possibile definire un'espressione per una colonna per consentire che questa contenga un valore calcolato sulla base di altri valori di colonna nella stessa riga o sulla base di valori di colonna di più righe della tabella.  Per definire l'espressione da valutare, usare la proprietà <xref:System.Data.DataColumn.Expression%2A> della colonna di destinazione e la proprietà <xref:System.Data.DataColumn.ColumnName%2A> per fare riferimento ad altre colonne nell'espressione.  La proprietà <xref:System.Data.DataColumn.DataType%2A> specificata per la colonna di espressioni deve essere adeguata per il valore restituito dall'espressione.  
  
 La tabella seguente indica diversi usi possibili delle colonne di espressioni in una tabella.  
  
|Tipo di espressione|Esempio|  
|-------------------------|-------------|  
|Confronto|"Total \>\= 500"|  
|Calcolo|"UnitPrice \* Quantity"|  
|Aggregazione|Sum\(Price\)|  
  
 È possibile impostare la proprietà **Expression** per un oggetto **DataColumn** esistente oppure includere la proprietà come terzo argomento passato al costruttore <xref:System.Data.DataColumn>, come illustrato nell'esempio seguente.  
  
```vb  
workTable.Columns.Add("Total",Type.GetType("System.Double"))  
workTable.Columns.Add("SalesTax", Type.GetType("System.Double"), _  
  "Total * 0.086")  
  
```  
  
```csharp  
workTable.Columns.Add("Total", typeof(Double));  
workTable.Columns.Add("SalesTax", typeof(Double), "Total * 0.086");  
```  
  
 Le espressioni possono fare riferimento ad altre colonne di espressioni. Viene tuttavia generata un'eccezione se è presente un riferimento circolare, ovvero quando due espressioni fanno riferimento l'una all'altra.  Per le regole sulla scrittura di espressioni, vedere la proprietà <xref:System.Data.DataColumn.Expression%2A> della classe **DataColumn**.  
  
## Vedere anche  
 <xref:System.Data.DataColumn>   
 <xref:System.Data.DataSet>   
 <xref:System.Data.DataTable>   
 [Definizione dello schema di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)