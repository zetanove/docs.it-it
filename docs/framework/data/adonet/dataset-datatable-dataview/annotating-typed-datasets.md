---
title: "Inserimento di annotazioni in DataSet tipizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f82aaa62-321e-4c8a-b51b-9d1114700170
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Inserimento di annotazioni in DataSet tipizzati
Le annotazioni consentono di modificare i nomi degli elementi nel <xref:System.Data.DataSet> tipizzato senza modificare lo schema sottostante.  Se si modificassero i nomi degli elementi dello schema sottostante, i riferimenti presenti nel **DataSet** punterebbero a oggetti non più esistenti nell'origine dati e si perderebbe un riferimento agli oggetti esistenti nell'origine dati.  
  
 L'uso delle annotazioni consente di personalizzare i nomi degli oggetti presenti nel **DataSet** tipizzato assegnando nomi più significativi, in modo da migliorare la leggibilità del codice e facilitare l'uso del **DataSet** da parte dei client, mantenendo intatto lo schema sottostante.  Dal seguente elemento di schema per la tabella **Customers** del database **Northwind**, ad esempio, si ottiene come risultato un nome oggetto **DataRow** corrispondente a **CustomersRow** e un oggetto <xref:System.Data.DataRowCollection> denominato **Customers**.  
  
```  
<xs:element name="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 Il nome **Customers** per un oggetto **DataRowCollection** risulta significativo nel codice del client, mentre il nome **CustomersRow** per **DataRow** potrebbe generare confusione, poiché si tratta di un unico oggetto.  Negli scenari più comuni inoltre ci si riferisce all'oggetto senza specificare l'identificatore **Row** e indicando tale oggetto nel riferimento semplicemente come oggetto **Customer**.  La soluzione consiste nell'inserire annotazioni nello schema e nell'identificare nuovi nomi per gli oggetti **DataRow** e **DataRowCollection**.  Di seguito viene riportata una versione annotata dello schema precedente.  
  
```  
<xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 Se si specifica un valore **typedName** pari a **Customer**, si otterrà un nome per l'oggetto **DataRow** corrispondente a **Customer**.  Specificando un valore **typedPlural** pari a **Customers**, si conserva il nome **Customers** per **DataRowCollection**.  
  
 Nella seguente tabella sono indicate le annotazioni disponibili.  
  
|Annotazione|Descrizione|  
|-----------------|-----------------|  
|**typedName**|Nome dell'oggetto.|  
|**typedPlural**|Nome della raccolta di oggetti.|  
|**typedParent**|Nome dell'oggetto quando si fa riferimento a tale oggetto in una relazione padre.|  
|**typedChildren**|Nome del metodo per la restituzione di oggetti da una relazione figlio.|  
|**nullValue**|Valore specificato se il valore sottostante è **DBNull**.  Per le annotazioni di tipo **nullValue**, vedere la tabella seguente.  Il valore predefinito è **\_throw**.|  
  
 Nella tabella seguente vengono elencati i valori che è possibile usare per le annotazioni di tipo **nullValue**.  
  
|Valore nullValue|Descrizione|  
|----------------------|-----------------|  
|*Valore di sostituzione*|Specifica il valore da restituire.  È necessario che il valore restituito corrisponda al tipo dell'elemento.  Usare ad esempio `nullValue="0"` per restituire 0 per i campi integer null.|  
|**\_throw**|Generazione di un'eccezione.  Questa è l'impostazione predefinita.|  
|**\_null**|Consente di restituire un riferimento null o di generare un'eccezione se viene rilevato un tipo primitivo.|  
|**\_empty**|Nel caso delle stringhe consente di restituire **String.Empty**, negli altri casi consente di restituire un oggetto creato da un costruttore vuoto.  Se viene rilevato un tipo primitivo, consente di generare un'eccezione.|  
  
 Nella tabella seguente vengono elencati i valori predefiniti per gli oggetti di un **DataSet** tipizzato e le annotazioni disponibili.  
  
|Oggetto\/Metodo\/Evento|Default|Annotazione|  
|-----------------------------|-------------|-----------------|  
|**DataTable**|TableNameDataTable|typedPlural|  
|Metodi **DataTable**|NewTableNameRow<br /><br /> AddTableNameRow<br /><br /> DeleteTableNameRow|typedName|  
|**DataRowCollection**|TableName|typedPlural|  
|**DataRow**|TableNameRow|typedName|  
|**DataColumn**|DataTable.ColumnNameColumn<br /><br /> DataRow.ColumnName|typedName|  
|**Proprietà**|PropertyName|typedName|  
|Funzione di accesso **Child**|GetChildTableNameRows|typedChildren|  
|Funzione di accesso **Parent**|TableNameRow|typedParent|  
|Eventi **DataSet**|TableNameRowChangeEvent<br /><br /> TableNameRowChangeEventHandler|typedName|  
  
 Per usare le annotazioni del **DataSet** tipizzato, è necessario includere il seguente riferimento **xmlns** nello schema XSD \(Schema Definition Language\) di XML.  Per creare un file XSD dalle tabelle di database, vedere <xref:System.Data.DataSet.WriteXmlSchema%2A> o [Uso di dataset in Visual Studio](http://msdn.microsoft.com/library/8bw9ksd6.aspx).  
  
```  
xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
```  
  
 Di seguito viene riportato un esempio di schema annotato in cui viene esposta la tabella **Customers** del database **Northwind** con inclusa una relazione alla tabella **Orders**.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet"   
      xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
      xmlns=""   
      xmlns:xs="http://www.w3.org/2001/XMLSchema"   
      xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers" codegen:typedName="Customer"  
codegen:typedPlural="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID" type="xs:string" minOccurs="0" />  
              <xs:element name="CompanyName"  
codegen:typedName="CompanyName" type="xs:string" minOccurs="0" />  
              <xs:element name="Phone" codegen:typedName="Phone"  
codegen:nullValue="" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
        <xs:element name="Orders" codegen:typedName="Order"  
codegen:typedPlural="Orders">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="OrderID" codegen:typedName="OrderID"  
type="xs:int" minOccurs="0" />  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID"  
                 codegen:nullValue="" type="xs:string" minOccurs="0" />  
              <xs:element name="EmployeeID"  
codegen:typedName="EmployeeID" codegen:nullValue="0"   
type="xs:int" minOccurs="0" />  
              <xs:element name="OrderAdapter"  
codegen:typedName="OrderAdapter"  
codegen:nullValue="1980-01-01T00:00:00"   
type="xs:dateTime" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
    <xs:unique name="Constraint1">  
      <xs:selector xpath=".//Customers" />  
      <xs:field xpath="CustomerID" />  
    </xs:unique>  
    <xs:keyref name="CustOrders" refer="Constraint1"  
codegen:typedParent="Customer" codegen:typedChildren="GetOrders">  
      <xs:selector xpath=".//Orders" />  
      <xs:field xpath="CustomerID" />  
    </xs:keyref>  
  </xs:element>  
</xs:schema>  
```  
  
 Nell'esempio di codice seguente viene usato un **DataSet** fortemente tipizzato creato dallo schema di esempio.  Un <xref:System.Data.SqlClient.SqlDataAdapter> viene usato per compilare la tabella **Customers** e un altro <xref:System.Data.SqlClient.SqlDataAdapter> per compilare la tabella **Orders**.  Il **DataSet** fortemente tipizzato definisce l'oggetto **DataRelations**.  
  
```vb  
' Assumes a valid SqlConnection object named connection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT CustomerID, CompanyName, Phone FROM Customers", &  
    connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders", &  
    connection)  
  
' Populate a strongly typed DataSet.  
connection.Open()  
Dim customers As CustomerDataSet = New CustomerDataSet()  
customerAdapter.Fill(customers, "Customers")  
orderAdapter.Fill(customers, "Orders")  
connection.Close()  
  
' Add a strongly typed event.  
AddHandler customers.Customers.CustomerChanged, &  
    New CustomerDataSet.CustomerChangeEventHandler( _  
    AddressOf OnCustomerChanged)  
  
' Add a strongly typed DataRow.  
Dim newCustomer As CustomerDataSet.Customer = _  
    customers.Customers.NewCustomeromer()  
newCustomer.CustomerID = "NEW01"  
newCustomer.CompanyName = "My New Company"  
customers.Customers.AddCustomer(newCustomer)  
  
' Navigate the child relation.  
Dim customer As CustomerDataSet.Customer  
Dim order As CustomerDataSet.Order  
  
For Each customer In customers.Customers  
  Console.WriteLine(customer.CustomerID)  
  For Each order In customer.GetOrders()  
    Console.WriteLine(vbTab & order.OrderID)  
  Next  
Next  
  
Private Shared Sub OnCustomerChanged( _  
    sender As Object, e As CustomerDataSet.CustomerChangeEvent)  
  
End Sub  
  
```  
  
```csharp  
// Assumes a valid SqlConnection object named connection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
    "SELECT CustomerID, CompanyName, Phone FROM Customers",  
    connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders",   
    connection);  
  
// Populate a strongly typed DataSet.  
connection.Open();  
CustomerDataSet customers = new CustomerDataSet();  
customerAdapter.Fill(customers, "Customers");  
orderAdapter.Fill(customers, "Orders");  
connection.Close();  
  
// Add a strongly typed event.  
customers.Customers.CustomerChanged += new   
  CustomerDataSet.CustomerChangeEventHandler(OnCustomerChanged);  
  
// Add a strongly typed DataRow.  
CustomerDataSet.Customer newCustomer =   
    customers.Customers.NewCustomeromer();  
newCustomer.CustomerID = "NEW01";  
newCustomer.CompanyName = "My New Company";  
customers.Customers.AddCustomer(newCustomer);  
  
// Navigate the child relation.  
foreach(CustomerDataSet.Customer customer in customers.Customers)  
{  
  Console.WriteLine(customer.CustomerID);  
  foreach(CustomerDataSet.Order order in customer.GetOrders())  
    Console.WriteLine("\t" + order.OrderID);  
}  
  
protected static void OnCustomerChanged(object sender, CustomerDataSet.CustomerChangeEvent e)  
    {  
  
    }  
```  
  
## Vedere anche  
 <xref:System.Data.DataColumnCollection>   
 <xref:System.Data.DataSet>   
 [DataSet tipizzati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)