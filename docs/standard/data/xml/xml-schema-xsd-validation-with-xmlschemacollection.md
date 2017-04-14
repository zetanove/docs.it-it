---
title: "Convalida XSD (XML Schema) con XmlSchemaCollection | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: ad0b5717-3d32-41ad-a4d7-072c3e492b82
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Convalida XSD (XML Schema) con XmlSchemaCollection
È possibile usare il tipo <xref:System.Xml.Schema.XmlSchemaCollection> per convalidare un documento XML in base a schemi XSD \(XML Schema Definition Language\).  Il tipo <xref:System.Xml.Schema.XmlSchemaCollection> migliora le prestazioni archiviando gli schemi nella raccolta in modo che non vengano caricati in memoria ogni volta che viene eseguita la convalida.  Se lo schema esiste nella raccolta di schemi, l'attributo `schemaLocation` verrà usato per cercare lo schema nella raccolta.  
  
> [!IMPORTANT]
>  La classe <xref:System.Xml.Schema.XmlSchemaCollection> è obsoleta ed è stata sostituita dalla classe <xref:System.Xml.Schema.XmlSchemaSet>.  Per altre informazioni sulla classe <xref:System.Xml.Schema.XmlSchemaSet>, vedere [XmlSchemaSet per la compilazione di schemi](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md).  
  
 Nell'esempio seguente viene illustrato l'elemento radice di un file di dati.  
  
```  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns="urn:bookstore-schema"  
    elementFormDefault="qualified"  
    targetNamespace="urn:bookstore-schema">  
```  
  
 In questo esempio, il valore dell'attributo `targetNamespace` è `urn:bookstore-schema`, ovvero lo stesso spazio dei nomi usato quando si aggiunge lo schema all'oggetto <xref:System.Xml.Schema.XmlSchemaCollection>.  
  
 Nell'esempio di codice seguente viene aggiunto uno schema XML al tipo <xref:System.Xml.Schema.XmlSchemaCollection>.  
  
```vb  
Dim xsc As New XmlSchemaCollection()  
' XML Schema.  
xsc.Add("urn:bookstore-schema", schema)   
reader = New XmlTextReader(filename)  
vreader = New XmlValidatingReader(reader)  
vreader.Schemas.Add(xsc)  
```  
  
```csharp  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
// XML Schema.  
xsc.Add("urn:bookstore-schema", schema);  
reader = new XmlTextReader (filename);  
vreader = new XmlValidatingReader (reader);  
vreader.Schemas.Add(xsc);  
```  
  
 In genere, l'attributo `targetNamespace` viene usato per aggiungere la proprietà `namespaceURI` nel metodo <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> per l'oggetto <xref:System.Xml.Schema.XmlSchemaCollection>.  È possibile specificare un riferimento null prima di aggiungere lo schema al tipo <xref:System.Xml.Schema.XmlSchemaCollection>.  Per gli schemi senza uno spazio dei nomi è necessario usare una stringa vuota \(""\).  Nel tipo <xref:System.Xml.Schema.XmlSchemaCollection> può essere presente solo uno schema senza uno spazio dei nomi.  
  
 Nell'esempio di codice seguente viene aggiunto uno schema XML, HeadCount.xsd, al tipo <xref:System.Xml.Schema.XmlSchemaCollection> e viene eseguita la convalida di HeadCount.xml.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Schema  
  
Namespace ValidationSample  
  
   Class Sample  
  
      Public Shared Sub Main()  
         Dim tr As New XmlTextReader("HeadCount.xml")  
         Dim vr As New XmlValidatingReader(tr)  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd")  
         vr.ValidationType = ValidationType.Schema  
         AddHandler vr.ValidationEventHandler, AddressOf ValidationHandler  
  
         While vr.Read()  
         End While  
         Console.WriteLine("Validation finished")  
      End Sub  
      ' Main  
  
      Public Shared Sub ValidationHandler(sender As Object, args As ValidationEventArgs)  
         Console.WriteLine("***Validation error")  
         Console.WriteLine("Severity:{0}", args.Severity)  
         Console.WriteLine("Message:{0}", args.Message)  
      End Sub  
      ' ValidationHandler  
   End Class  
   ' Sample  
End Namespace  
' ValidationSample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Schema;  
  
namespace ValidationSample  
{  
   class Sample  
   {  
      public static void Main()  
      {  
         XmlTextReader tr = new XmlTextReader("HeadCount.xml");  
         XmlValidatingReader vr = new XmlValidatingReader(tr);  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd");  
         vr.ValidationType = ValidationType.Schema;  
         vr.ValidationEventHandler += new ValidationEventHandler (ValidationHandler);  
  
         while(vr.Read());  
         Console.WriteLine("Validation finished");  
      }  
  
      public static void ValidationHandler(object sender, ValidationEventArgs args)  
      {  
         Console.WriteLine("***Validation error");  
         Console.WriteLine("\tSeverity:{0}", args.Severity);  
         Console.WriteLine("\tMessage  :{0}", args.Message);  
      }  
   }  
}  
```  
  
 Di seguito viene indicato il contenuto del file di input, HeadCount.xml, da convalidare.  
  
```  
<!--Load HeadCount.xsd in SchemaCollection for Validation-->  
<hc:HeadCount xmlns:hc='xsdHeadCount'>  
   <Name>Waldo Pepper</Name>  
   <Name>Red Pepper</Name>  
</hc:HeadCount>  
```  
  
 Di seguito viene indicato il contenuto del file di XML Schema, HeadCount.xsd, in base al quale eseguire la convalida.  
  
```  
<xs:schema xmlns="xsdHeadCount" targetNamespace="xsdHeadCount" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
   <xs:element name='HeadCount' type="HEADCOUNT"/>  
   <xs:complexType name="HEADCOUNT">  
      <xs:sequence>  
         <xs:element name='Name' type='xs:string' maxOccurs='unbounded'/>  
      </xs:sequence>  
      <xs:attribute name='division' type='xs:int' use='optional' default='8'/>  
   </xs:complexType>  
</xs:schema>  
```  
  
 Nell'esempio di codice seguente viene creato un <xref:System.Xml.XmlValidatingReader> che accetta un <xref:System.Xml.XmlTextReader>.  Il file di input, sample4.xml, viene convalidato in base a XML Schema, sample4.xsd.  
  
```vb  
Dim tr As New XmlTextReader("sample4.xml")  
Dim vr As New XmlValidatingReader(tr)  
vr.ValidationType = ValidationType.Schema  
vr.Schemas.Add("datatypesTest", "sample4.xsd")  
AddHandler vr.ValidationEventHandler, AddressOf ValidationCallBack  
While vr.Read()  
   Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name)  
End While  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("sample4.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
vr.ValidationType = ValidationType.Schema;  
        vr.Schemas.Add("datatypesTest", "sample4.xsd");  
vr.ValidationEventHandler += new ValidationEventHandler(ValidationCallBack);  
while(vr.Read()) {  
    Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name);  
    }  
```  
  
 Di seguito viene indicato il contenuto del file di input, sample4.xml, da convalidare.  
  
```  
<datatypes xmlns="datatypesTest">  
    <number>  
        <number_1>123</number_1>  
    </number>  
</datatypes>  
```  
  
 Di seguito viene indicato il contenuto del file di XML Schema, sample4.xsd, in base al quale eseguire la convalida.  
  
```  
<xs:schema   
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    xmlns:tns="datatypesTest"   
    targetNamespace="datatypesTest"  
    elementFormDefault="qualified">  
  
<xs:element name = "datatypes">  
  <xs:complexType>  
    <xs:all>  
        <xs:element name="number">  
            <xs:complexType>  
                <xs:sequence>  
                    <xs:element name="number_1" type="xs:decimal" maxOccurs="unbounded"/>  
                </xs:sequence>  
            </xs:complexType>  
        </xs:element>  
    </xs:all>  
  </xs:complexType>  
</xs:element>  
</xs:schema>  
```  
  
## Vedere anche  
 <xref:System.Xml.XmlParserContext>   
 <xref:System.Xml.XmlValidatingReader.ValidationEventHandler?displayProperty=fullName>   
 <xref:System.Xml.XmlValidatingReader.Schemas%2A?displayProperty=fullName>   
 [Compilazione dello schema XmlSchemaCollection](../../../../docs/standard/data/xml/xmlschemacollection-schema-compilation.md)