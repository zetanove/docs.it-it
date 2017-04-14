---
title: "Generazione di DataSet fortemente tipizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54333cbf-bb43-4314-a7d4-6dc1dd1c44b3
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Generazione di DataSet fortemente tipizzati
Dato un XML Schema conforme allo standard XSD \(XML Schema Definition Language\), è possibile generare un <xref:System.Data.DataSet> fortemente tipizzato usando lo strumento XSD.exe fornito con [!INCLUDE[winsdklong](../../../../../includes/winsdklong-md.md)].  
  
 Per creare un file XSD dalle tabelle di database, vedere <xref:System.Data.DataSet.WriteXmlSchema%2A> o [Uso di dataset in Visual Studio](http://msdn.microsoft.com/library/8bw9ksd6.aspx).  
  
 Nell'esempio seguente viene mostrata la sintassi per la generazione di un **DataSet** con questo strumento.  
  
```  
xsd.exe /d /l:CS XSDSchemaFileName.xsd /eld /n:XSDSchema.Namespace  
```  
  
 In questa sintassi la direttiva `/d` consente di richiedere allo strumento la generazione di un **DataSet** e `/l:` consente di fornire allo strumento informazioni relative al linguaggio da usare \(ad esempio C\# o Visual Basic .NET\).  La direttiva `/eld` facoltativa specifica che è possibile usare [!INCLUDE[linq_dataset](../../../../../includes/linq-dataset-md.md)] per eseguire query sul **DataSet** generato. Questa opzione viene usata quando si specifica anche l'opzione `/d`.  Per altre informazioni, vedere [Esecuzione di query su DataSet tipizzati](../../../../../docs/framework/data/adonet/querying-typed-datasets.md).  La direttiva facoltativa `/n:` consente di richiedere allo strumento anche la generazione di uno spazio dei nomi per il **DataSet** denominato **XSDSchema.Namespace**.  L'output del comando è costituito dal file XSDSchemaFileName.dll, che può essere compilato e usato in un'applicazione ADO.NET.  È possibile compilare il codice generato come libreria o modulo.  
  
 Nel codice seguente viene mostrata la sintassi per la compilazione del codice generato come libreria usando il compilatore C\# \(csc.exe\).  
  
```  
csc.exe /t:library XSDSchemaFileName.cs /r:System.dll /r:System.Data.dll  
```  
  
 La direttiva `/t:` consente di richiedere allo strumento la compilazione in una libreria e la direttiva `/r:` consente di specificare le librerie dipendenti necessarie per la compilazione.  L'output del comando è costituito dal file XSDSchemaFileName.dll, che può essere passato al compilatore quando si compila un'applicazione ADO.NET con la direttiva `/r:`.  
  
 Nel codice seguente viene mostrata la sintassi usata per l'accesso allo spazio dei nomi passato a XSD.exe in un'applicazione ADO.NET.  
  
```vb  
Imports XSDSchema.Namespace  
  
```  
  
```csharp  
using XSDSchema.Namespace;  
```  
  
 Nel seguente esempio di codice un **DataSet** tipizzato denominato **CustomerDataSet** viene usato per caricare un elenco di clienti dal database **Northwind**.  Una volta caricati i dati usando il metodo **Fill**, l'esempio scorre in ciclo ogni cliente nella tabella **Customers** tramite l'oggetto tipizzato **CustomersRow** \(**DataRow**\).  Questa operazione consente di accedere direttamente alla colonna **CustomerID**, anziché accedervi tramite **DataColumnCollection**.  
  
```vb  
Dim customers As CustomerDataSet= New CustomerDataSet()  
Dim adapter As SqlDataAdapter New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers;", _  
  "Data Source=(local);Integrated " & _  
  "Security=SSPI;Initial Catalog=Northwind")  
  
adapter.Fill(customers, "Customers")  
  
Dim customerRow As CustomerDataSet.CustomersRow  
For Each customerRow In customers.Customers  
  Console.WriteLine(customerRow.CustomerID)  
Next  
  
```  
  
```csharp  
CustomerDataSet customers = new CustomerDataSet();  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers;",  
  "Data Source=(local);Integrated " +  
  "Security=SSPI;Initial Catalog=Northwind");  
  
adapter.Fill(customers, "Customers");  
  
foreach(CustomerDataSet.CustomersRow customerRow in customers.Customers)  
  Console.WriteLine(customerRow.CustomerID);  
```  
  
 Di seguito viene riportato l'XML Schema usato per l'esempio.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet" xmlns="" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
## Vedere anche  
 <xref:System.Data.DataColumnCollection>   
 <xref:System.Data.DataSet>   
 [DataSet tipizzati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)