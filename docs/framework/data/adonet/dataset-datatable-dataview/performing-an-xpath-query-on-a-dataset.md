---
title: "Esecuzione di una query XPath in un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7e828566-fffe-4d38-abb2-4d68fd73f663
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Esecuzione di una query XPath in un DataSet
La relazione tra un <xref:System.Data.DataSet> sincronizzato con un oggetto <xref:System.Xml.XmlDataDocument> consente di usare i servizi XML, ad esempio le query XPath \(XML Path Language\), che anziché accedere direttamente al **DataSet**, accedono all'oggetto **XmlDataDocument** e possono eseguire determinate funzionalità in modo più semplice.  Ad esempio, anziché usare il metodo **Select** della <xref:System.Data.DataTable> per navigare tra le relazioni ad altre tabelle del **DataSet**, è possibile eseguire una query XPath in un oggetto **XmlDataDocument** sincronizzato con il **DataSet**, in modo da ottenere un elenco di elementi XML sotto forma di un <xref:System.Xml.XmlNodeList>.  È quindi possibile passare i nodi presenti in **XmlNodeList**, il cui cast è stato eseguito come nodi <xref:System.Xml.XmlElement>, al metodo **GetRowFromElement** dell'oggetto **XmlDataDocument**, in modo da restituire i riferimenti <xref:System.Data.DataRow> corrispondenti alle righe della tabella del **DataSet** sincronizzato.  
  
 Nell'esempio di codice seguente viene eseguita una query XPath "nipote".  Nell'oggetto **DataSet** sono presenti tre tabelle: **Customers**, **Orders** e **OrderDetails**.  Nell'esempio viene prima di tutto creata una relazione padre\-figlio tra le tabelle **Customers** e **Orders**, quindi tra le tabelle **Orders** e **OrderDetails**.  Viene quindi eseguita una query XPath per restituire un oggetto **XmlNodeList** di nodi **Customers** in cui a un nodo nipote **OrderDetails** è associato un nodo **ProductID** con valore 43.  Nell'esempio viene in pratica usata la query XPath per determinare quali clienti hanno ordinato il prodotto il cui oggetto **ProductID** è 43.  
  
```vb  
' Assumes that connection is a valid SqlConnection.  
connection.Open()  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Customers", connection)  
customerAdapter.Fill(dataSet, "Customers")  
  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Orders", connection)  
orderAdapter.Fill(dataSet, "Orders")  
  
Dim detailAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM [Order Details]", connection)  
detailAdapter.Fill(dataSet, "OrderDetails")  
  
connection.Close()  
  
dataSet.Relations.Add("CustOrders", _  
dataSet.Tables("Customers").Columns("CustomerID"), _  
dataSet.Tables("Orders").Columns("CustomerID")).Nested = true  
  
dataSet.Relations.Add("OrderDetail", _  
  dataSet.Tables("Orders").Columns("OrderID"), _  
dataSet.Tables("OrderDetails").Columns("OrderID"), false).Nested = true  
  
Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)   
  
Dim nodeList As XmlNodeList = xmlDoc.DocumentElement.SelectNodes( _  
  "descendant::Customers[*/OrderDetails/ProductID=43]")  
  
Dim dataRow As DataRow  
Dim xmlNode As XmlNode  
  
For Each xmlNode In nodeList  
  dataRow = xmlDoc.GetRowFromElement(CType(xmlNode, XmlElement))  
  
  If Not dataRow Is Nothing then Console.WriteLine(xmlRow(0).ToString())  
Next  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection.  
connection.Open();  
  
DataSet dataSet = new DataSet("CustomerOrders");  
  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT * FROM Customers", connection);  
customerAdapter.Fill(dataSet, "Customers");  
  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT * FROM Orders", connection);  
orderAdapter.Fill(dataSet, "Orders");  
  
SqlDataAdapter detailAdapter = new SqlDataAdapter(  
  "SELECT * FROM [Order Details]", connection);  
detailAdapter.Fill(dataSet, "OrderDetails");  
  
connection.Close();  
  
dataSet.Relations.Add("CustOrders",  
  dataSet.Tables["Customers"].Columns["CustomerID"],  
 dataSet.Tables["Orders"].Columns["CustomerID"]).Nested = true;  
  
dataSet.Relations.Add("OrderDetail",  
  dataSet.Tables["Orders"].Columns["OrderID"],  
  dataSet.Tables["OrderDetails"].Columns["OrderID"],   
  false).Nested = true;  
  
XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);   
  
XmlNodeList nodeList = xmlDoc.DocumentElement.SelectNodes(  
  "descendant::Customers[*/OrderDetails/ProductID=43]");  
  
DataRow dataRow;  
foreach (XmlNode xmlNode in nodeList)  
{  
  dataRow = xmlDoc.GetRowFromElement((XmlElement)xmlNode);  
  if (dataRow != null)  
    Console.WriteLine(dataRow[0]);  
}  
```  
  
## Vedere anche  
 [Sincronizzazione di DataSet e XmlDataDocument](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)