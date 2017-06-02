---
title: "Scrittura delle informazioni relative allo schema di un DataSet come XSD | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e530831-695e-49ff-8f0b-e5b0c526b8eb
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Scrittura delle informazioni relative allo schema di un DataSet come XSD
È possibile scrivere lo schema di un tipo <xref:System.Data.DataSet> sotto forma di schema XSD \(XML Schema Definition Language\), in modo da consentirne il trasporto, con o senza dati correlati, in un documento XML.  XML Schema, che può essere scritto in un file, un flusso, un oggetto <xref:System.Xml.XmlWriter> o una stringa, risulta utile per la generazione di un **DataSet** tipizzato in modo sicuro.  Per altre informazioni sugli oggetti **DataSet** fortemente tipizzati, vedere [DataSet tipizzati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md).  
  
 La proprietà **ColumnMapping** dell'oggetto <xref:System.Data.DataColumn> consente di specificare la modalità di rappresentazione di una colonna di una tabella in un XML Schema.  Per altre informazioni, vedere "Mapping di colonne a elementi, attributi e testo XML" in [Scrittura del contenuto di DataSet come dati XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md).  
  
 Per scrivere lo schema di un **DataSet** sotto forma di XML Schema in un file, un flusso o un **XmlWriter**, usare il metodo **WriteXmlSchema** del **DataSet**.  **WriteXmlSchema** accetta un parametro che consente di specificare la destinazione dell'XML Schema risultante.  Negli esempi di codice seguenti viene illustrato come scrivere l'XML Schema di un oggetto **DataSet** in un file tramite il passaggio di una stringa contenente un nome file e un oggetto <xref:System.IO.StreamWriter>.  
  
```vb  
dataSet.WriteXmlSchema("Customers.xsd")  
```  
  
```csharp  
dataSet.WriteXmlSchema("Customers.xsd");  
```  
  
```vb  
Dim writer As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xsd")  
dataSet.WriteXmlSchema(writer)  
writer.Close()  
```  
  
```csharp  
System.IO.StreamWriter writer = new System.IO.StreamWriter("Customers.xsd");  
dataSet.WriteXmlSchema(writer);  
writer.Close();  
```  
  
 Per ottenere lo schema di un **DataSet** e scriverlo sotto forma di stringa di XML Schema, usare il metodo **GetXmlSchema**, come illustrato nell'esempio seguente.  
  
```vb  
Dim schemaString As String = dataSet.GetXmlSchema()  
```  
  
```csharp  
string schemaString = dataSet.GetXmlSchema();  
```  
  
## Vedere anche  
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [Scrittura del contenuto di DataSet come dati XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)   
 [DataSet tipizzati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)