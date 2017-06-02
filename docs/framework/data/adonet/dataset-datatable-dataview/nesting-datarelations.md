---
title: "DataRelation annidati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9530f9c9-dd98-4b93-8cdb-40d7f1e8d0ab
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataRelation annidati
In una rappresentazione relazionale dei dati, le singole tabelle contengono righe correlate tra loro tramite una colonna o un set di colonne.  Nel <xref:System.Data.DataSet> di ADO.NET la relazione tra le tabelle viene implementata mediante l'oggetto <xref:System.Data.DataRelation>.  Quando si crea un oggetto **DataRelation**, le relazioni padre\-figlio tra le colonne vengono gestite solo tramite tale relazione.  Le tabelle e le colonne sono entità separate.  Nella rappresentazione gerarchica dei dati fornita dall'XML, le relazioni padre\-figlio sono rappresentate da elementi padre contenenti elementi figlio annidati.  
  
 Per facilitare l'annidamento di oggetti figlio durante la sincronizzazione di un **DataSet** con un <xref:System.Xml.XmlDataDocument> o la scrittura sotto forma di dati XML mediante **WriteXml**, l'oggetto **DataRelation** espone una proprietà **Nested**.  L'impostazione della proprietà **Nested** di un oggetto **DataRelation** su **true** provoca l'annidamento delle righe figlio all'interno della colonna padre durante la scrittura sotto forma di dati XML o la sincronizzazione con un **XmlDataDocument**.  L'impostazione predefinita per la proprietà **Nested** di **DataRelation** è **false**.  
  
 Si consideri, ad esempio, il seguente **DataSet**.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT OrderID, CustomerID, OrderDate FROM Orders", connection)  
  
connection.Open()  
  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
customerAdapter.Fill(dataSet, "Customers")  
orderAdapter.Fill(dataSet, "Orders")  
  
connection.Close()  
  
Dim customerOrders As DataRelation = dataSet.Relations.Add( _  
  "CustOrders", dataSet.Tables("Customers").Columns("CustomerID"), _  
  dataSet.Tables("Orders").Columns("CustomerID"))  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT OrderID, CustomerID, OrderDate FROM Orders", connection);  
  
connection.Open();  
  
DataSet dataSet = new DataSet("CustomerOrders");  
customerAdapter.Fill(dataSet, "Customers");  
orderAdapter.Fill(dataSet, "Orders");  
  
connection.Close();  
  
DataRelation customerOrders = dataSet.Relations.Add(  
  "CustOrders", dataSet.Tables["Customers"].Columns["CustomerID"],  
  dataSet.Tables["Orders"].Columns["CustomerID"]);  
```  
  
 Dal momento che la proprietà **Nested** dell'oggetto **DataRelation** non è impostata su **true** per questo **DataSet**, gli oggetti figlio non verranno annidati all'interno degli elementi padre quando tale **DataSet** viene rappresentato sotto forma di dati XML.  La trasformazione della rappresentazione XML di un **Dataset** che contiene **Dataset** correlati con relazioni dati non annidate può causare un rallentamento delle prestazioni.  È consigliabile annidare le relazioni dati.  A tale scopo, impostare la proprietà **Nested** su **true**,  quindi scrivere codice nel foglio di stile XSLT che usa espressioni di query XPath gerarchiche basate su un approccio dall'alto verso il basso per individuare e trasformare i dati.  
  
 Nell'esempio di codice seguente viene illustrato il risultato della chiamata di **WriteXml** nel **DataSet**.  
  
```  
<CustomerOrders>  
  <Customers>  
    <CustomerID>ALFKI</CustomerID>  
    <CompanyName>Alfreds Futterkiste</CompanyName>  
  </Customers>  
  <Customers>  
    <CustomerID>ANATR</CustomerID>  
    <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
  </Customers>  
  <Orders>  
    <OrderID>10643</OrderID>  
    <CustomerID>ALFKI</CustomerID>  
    <OrderDate>1997-08-25T00:00:00</OrderDate>  
  </Orders>  
  <Orders>  
    <OrderID>10692</OrderID>  
    <CustomerID>ALFKI</CustomerID>  
    <OrderDate>1997-10-03T00:00:00</OrderDate>  
  </Orders>  
  <Orders>  
    <OrderID>10308</OrderID>  
    <CustomerID>ANATR</CustomerID>  
    <OrderDate>1996-09-18T00:00:00</OrderDate>  
  </Orders>  
</CustomerOrders>  
```  
  
 Notare che l'elemento **Customers** e gli elementi **Orders** vengono mostrati come elementi di pari livello.  Per visualizzare gli elementi **Orders** come elementi figlio dei rispettivi elementi padre, è necessario impostare la proprietà **Nested** dell'oggetto **DataRelation** su **true** e aggiungere il seguente codice:  
  
```vb  
customerOrders.Nested = True  
```  
  
```csharp  
customerOrders.Nested = true;  
```  
  
 Nel codice seguente viene mostrato l'output risultante, con gli elementi **Orders** annidati all'interno dei rispettivi elementi padre.  
  
```  
<CustomerOrders>  
  <Customers>  
    <CustomerID>ALFKI</CustomerID>  
    <Orders>  
      <OrderID>10643</OrderID>  
      <CustomerID>ALFKI</CustomerID>  
      <OrderDate>1997-08-25T00:00:00</OrderDate>  
    </Orders>  
    <Orders>  
      <OrderID>10692</OrderID>  
      <CustomerID>ALFKI</CustomerID>  
      <OrderDate>1997-10-03T00:00:00</OrderDate>  
    </Orders>  
    <CompanyName>Alfreds Futterkiste</CompanyName>  
  </Customers>  
  <Customers>  
    <CustomerID>ANATR</CustomerID>  
    <Orders>  
      <OrderID>10308</OrderID>  
      <CustomerID>ANATR</CustomerID>  
      <OrderDate>1996-09-18T00:00:00</OrderDate>  
    </Orders>  
    <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
  </Customers>  
</CustomerOrders>  
```  
  
## Vedere anche  
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [Aggiunta di DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)