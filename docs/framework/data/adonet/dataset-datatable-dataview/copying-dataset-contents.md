---
title: "Copia del contenuto di un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cb846617-2b1a-44ff-bd7f-5835f5ea37fa
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Copia del contenuto di un DataSet
È possibile creare una copia di un <xref:System.Data.DataSet> per usare i dati senza influire su quelli originali o per poter usare un subset dei dati contenuti in un **DataSet**.  Quando si copia un **DataSet**, è possibile:  
  
-   Creare una copia esatta del **DataSet**, inclusi lo schema, i dati, le informazioni relative allo stato della riga e le versioni di riga.  
  
-   Creare un **DataSet** contenente lo schema di un **DataSet** esistente ma solo le righe a cui sono state apportate modifiche.  È possibile restituire tutte le righe modificate oppure specificare un determinato **DataRowState**.  Per altre informazioni sugli stati delle righe, vedere [Stati delle righe e versioni delle righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md).  
  
-   Copiare solo lo schema, o struttura relazionale, del **DataSet**, senza copiare alcuna riga.  È possibile importare le righe in un tipo <xref:System.Data.DataTable> esistente usando il metodo <xref:System.Data.DataTable.ImportRow%2A>.  
  
 Per creare una copia esatta del **DataSet** in cui siano inclusi sia lo schema che i dati, usare il metodo <xref:System.Data.DataSet.Copy%2A> del **DataSet**.  Nell'esempio di codice seguente viene illustrata la creazione di una copia esatta del **DataSet**.  
  
```vb  
Dim copyDataSet As DataSet = customerDataSet.Copy()  
  
```  
  
```csharp  
DataSet copyDataSet = customerDataSet.Copy();  
```  
  
 Per creare una copia di un **DataSet** in cui siano inclusi lo schema e solo i dati che rappresentano righe **Added**, **Modified** o **Deleted**, usare il metodo <xref:System.Data.DataSet.GetChanges%2A> del **DataSet**.  Se si passa il valore **DataRowState** durante la chiamata del metodo **GetChanges**, è inoltre possibile usare tale metodo per restituire solo le righe a cui sia associato uno stato della riga specificato.  Nell'esempio di codice seguente viene illustrato come passare un valore **DataRowState** quando si chiama il metodo **GetChanges**.  
  
```vb  
' Copy all changes.  
Dim changeDataSet As DataSet = customerDataSet.GetChanges()  
' Copy only new rows.  
Dim addedDataSetAs DataSet = _  
    customerDataSet.GetChanges(DataRowState.Added)  
  
```  
  
```csharp  
// Copy all changes.  
DataSet changeDataSet = customerDataSet.GetChanges();  
// Copy only new rows.  
DataSet addedDataSet= customerDataSet.GetChanges(DataRowState.Added);  
```  
  
 Per creare una copia di un **DataSet** in cui sia incluso solo lo schema, usare il metodo <xref:System.Data.DataSet.Clone%2A> del **DataSet**.  È inoltre possibile aggiungere righe esistenti al **DataSet** duplicato, usando il metodo **ImportRow** della **DataTable**.  Il metodo **ImportRow** consente di aggiungere dati e informazioni relative allo stato e alla versione di riga alla tabella specificata.  I valori di colonna vengono aggiunti solo nel caso in cui i nomi di colonna corrispondano e il tipo di dati sia compatibile.  
  
 Nell'esempio di codice seguente viene creato un duplicato di un **DataSet** e vengono aggiunte le righe del **DataSet** originale alla tabella **Customers** nel **DataSet** duplicato per i clienti la cui colonna **CountryRegion** presenta il valore "Germany".  
  
```vb  
  
Dim customerDataSet As New DataSet  
        customerDataSet.Tables.Add(New DataTable("Customers"))  
        customerDataSet.Tables("Customers").Columns.Add("Name", GetType(String))  
        customerDataSet.Tables("Customers").Columns.Add("CountryRegion", GetType(String))  
        customerDataSet.Tables("Customers").Rows.Add("Juan", "Spain")  
        customerDataSet.Tables("Customers").Rows.Add("Johann", "Germany")  
        customerDataSet.Tables("Customers").Rows.Add("John", "UK")  
  
Dim germanyCustomers As DataSet = customerDataSet.Clone()  
  
Dim copyRows() As DataRow = _  
  customerDataSet.Tables("Customers").Select("CountryRegion = 'Germany'")  
  
Dim customerTable As DataTable = germanyCustomers.Tables("Customers")  
Dim copyRow As DataRow  
  
For Each copyRow In copyRows  
  customerTable.ImportRow(copyRow)  
Next  
  
```  
  
```csharp  
DataSet customerDataSet = new DataSet();  
customerDataSet.Tables.Add(new DataTable("Customers"));  
customerDataSet.Tables["Customers"].Columns.Add("Name", typeof(string));  
customerDataSet.Tables["Customers"].Columns.Add("CountryRegion", typeof(string));  
customerDataSet.Tables["Customers"].Rows.Add("Juan", "Spain");  
customerDataSet.Tables["Customers"].Rows.Add("Johann", "Germany");  
customerDataSet.Tables["Customers"].Rows.Add("John", "UK");  
  
DataSet germanyCustomers = customerDataSet.Clone();  
  
DataRow[] copyRows =   
  customerDataSet.Tables["Customers"].Select("CountryRegion = 'Germany'");  
  
DataTable customerTable = germanyCustomers.Tables["Customers"];  
  
foreach (DataRow copyRow in copyRows)  
  customerTable.ImportRow(copyRow);  
```  
  
## Vedere anche  
 <xref:System.Data.DataSet>   
 <xref:System.Data.DataTable>   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)