---
title: "Creazione di un DataView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b1cc02d1-23b1-4439-a998-0da1899f3442
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Creazione di un DataView
Per creare un <xref:System.Data.DataView>, sono disponibili due modalità.  È possibile usare il costruttore **DataView** oppure creare un riferimento alla proprietà <xref:System.Data.DataTable.DefaultView%2A> della <xref:System.Data.DataTable>.  Il costruttore **DataView** può essere vuoto oppure può accettare una **DataTable** come unico argomento o una **DataTable** insieme a criteri di filtro, criteri di ordinamento e un filtro relativo allo stato di riga.  Per altre informazioni sugli argomenti aggiuntivi disponibili per l'uso con **DataView**, vedere [Ordinamento e filtro dei dati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md).  
  
 Dal momento che l'indice per un **DataView** viene compilato sia al momento della creazione del **DataView** che a ogni modifica della proprietà **Sort**, **RowFilter** o **RowStateFilter**, per ottenere prestazioni ottimali, si consiglia di fornire eventuali criteri di ordinamento o di filtro iniziali come argomenti del costruttore quando si crea il **DataView**.  Se si crea un oggetto **DataView** senza specificare criteri di filtro o di ordinamento e successivamente si imposta la proprietà **Sort**, **RowFilter** o **RowStateFilter**, l'indice verrà compilato almeno due volte: una volta durante la creazione di **DataView** e una seconda volta quando viene modificata una delle proprietà di ordinamento o filtro.  
  
 Notare che se si crea un **DataView** usando un costruttore che non accetta argomenti, non sarà possibile usare il **DataView** fino a quando non sarà stata impostata la proprietà **Table**.  
  
 Nell'esempio di codice seguente viene illustrata la creazione di un **DataView** mediante il costruttore **DataView**.  Insieme alla **DataTable** vengono forniti un **RowFilter**, una colonna **Sort** e **DataViewRowState**.  
  
```vb  
Dim custDV As DataView = New DataView(custDS.Tables("Customers"), _  
    "Country = 'USA'", _  
    "ContactName", _  
    DataViewRowState.CurrentRows)  
  
```  
  
```csharp  
DataView custDV = new DataView(custDS.Tables["Customers"],   
    "Country = 'USA'",   
    "ContactName",   
    DataViewRowState.CurrentRows);  
```  
  
 Nell'esempio di codice seguente viene illustrato come ottenere un riferimento al **DataView** predefinito di una **DataTable** mediante la proprietà **DefaultView** della tabella.  
  
```vb  
Dim custDV As DataView = custDS.Tables("Customers").DefaultView  
  
```  
  
```csharp  
DataView custDV = custDS.Tables["Customers"].DefaultView;  
```  
  
## Vedere anche  
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [Ordinamento e filtro dei dati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)