---
title: "Inclusione o importazione di schemi XML | Microsoft Docs"
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
ms.assetid: fe1b4a11-37f4-4e1a-93c9-239f4fe736c0
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Inclusione o importazione di schemi XML
Uno schema XML può contenere elementi `<xs:import />`, `<xs:include />` e `<xs:redefine />`.  Questi elementi dello schema fanno riferimento ad altri schemi XML che possono essere usati per integrare la struttura dello schema che li include o importa.  Nell'API del modello SOM \(Schema Object Model\), a questi elementi sono associate le classi <xref:System.Xml.Schema.XmlSchemaImport>, <xref:System.Xml.Schema.XmlSchemaInclude> e <xref:System.Xml.Schema.XmlSchemaRedefine>.  
  
## Inclusione o importazione di uno schema XML  
 Nel seguente esempio di codice, allo schema del cliente creato nell'argomento [Compilazione di XML Schema](../../../../docs/standard/data/xml/building-xml-schemas.md) viene integrato lo schema dell'indirizzo.  L'integrazione dello schema del cliente con lo schema dell'indirizzo rende disponibili i tipi di indirizzo nello schema del cliente.  
  
 È possibile incorporare lo schema dell'indirizzo mediante l'elemento `<xs:include />` o `<xs:import />` per usare i componenti dello schema dell'indirizzo senza apportarvi modifiche oppure mediante un elemento `<xs:redefine />` per modificare i componenti in modo che soddisfino le esigenze dello schema del cliente.  Poiché nello schema dell'indirizzo `targetNamespace` è diverso da quello dello schema del cliente, vengono usati l'elemento `<xs:import />` e quindi la semantica di importazione.  
  
 L'esempio di codice consente di includere lo schema dell'indirizzo eseguendo i passaggi seguenti.  
  
1.  Aggiunge lo schema del cliente e lo schema dell'indirizzo a un nuovo oggetto <xref:System.Xml.Schema.XmlSchemaSet>, quindi li compila.  Eventuali avvisi ed errori di convalida dello schema rilevati durante la lettura e la compilazione degli schemi vengono gestiti dal delegato <xref:System.Xml.Schema.ValidationEventHandler>.  
  
2.  Recupera gli oggetti <xref:System.Xml.Schema.XmlSchema> compilati per gli schemi del cliente e dell'indirizzo dal tipo <xref:System.Xml.Schema.XmlSchemaSet> scorrendo la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>.  Dal momento che gli schemi sono stati compilati, è possibile accedere alle proprietà del set PSCI \(Post\-Schema\-Compilation\-Infoset\).  
  
3.  Crea un oggetto <xref:System.Xml.Schema.XmlSchemaImport>, imposta la proprietà <xref:System.Xml.Schema.XmlSchemaImport.Namespace%2A> dell'elemento import sullo spazio dei nomi dello schema dell'indirizzo, imposta la proprietà <xref:System.Xml.Schema.XmlSchemaExternal.Schema%2A> dell'elemento import sull'oggetto <xref:System.Xml.Schema.XmlSchema> dello schema dell'indirizzo e aggiunge l'elemento import alla proprietà <xref:System.Xml.Schema.XmlSchema.Includes%2A> dello schema del cliente.  
  
4.  Rielabora e compila l'oggetto modificato <xref:System.Xml.Schema.XmlSchema> dello schema del cliente usando i metodi <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> e <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> della classe <xref:System.Xml.Schema.XmlSchemaSet> e lo scrive nella console.  
  
5.  Infine, usando la proprietà <xref:System.Xml.Schema.XmlSchema.Includes%2A> dello schema del cliente, scrive in modo ricorsivo nella console tutti gli schemi importati nello schema del cliente.  La proprietà <xref:System.Xml.Schema.XmlSchema.Includes%2A> fornisce l'accesso a tutti gli elementi include, import o redefine aggiunti a uno schema.  
  
 Di seguito è riportato l'esempio di codice completo e gli schemi del cliente e dell'indirizzo scritti nella console.  
  
 [!code-cpp[XmlSchemaImportExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaImportExample/CPP/XmlSchemaImportExample.cpp#1)]
 [!code-csharp[XmlSchemaImportExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaImportExample/CS/XmlSchemaImportExample.cs#1)]
 [!code-vb[XmlSchemaImportExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaImportExample/VB/XmlSchemaImportExample.vb#1)]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:import namespace="http://www.example.com/IPO" />  
  <xs:element name="Customer">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="FirstName" type="xs:string" />  
        <xs:element name="LastName" type="tns:LastNameType" />  
      </xs:sequence>  
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" /  
>  
    </xs:complexType>  
  </xs:element>  
  <xs:simpleType name="LastNameType">  
    <xs:restriction base="xs:string">  
      <xs:maxLength value="20" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
<schema targetNamespace="http://www.example.com/IPO" xmlns="http://www.w3.org/2001/XMLSchema" xmlns:ipo="http://www.example.com/IPO">  
  <annotation>  
    <documentation xml:lang="en">  
      Addresses for International Purchase order schema  
      Copyright 2000 Example.com. All rights reserved.  
    </documentation>  
  </annotation>  
  <complexType name="Address">  
    <sequence>  
      <element name="name"   type="string"/>  
      <element name="street" type="string"/>  
      <element name="city"   type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="USAddress">  
    <complexContent>  
      <extension base="ipo:Address">  
        <sequence>  
          <element name="state" type="ipo:USState"/>  
          <element name="zip"   type="positiveInteger"/>  
        </sequence>  
      </extension>  
    </complexContent>  
  </complexType>  
  <!-- other Address derivations for more countries or regions -->  
  <simpleType name="USState">  
    <restriction base="string">  
      <enumeration value="AK"/>  
      <enumeration value="AL"/>  
      <enumeration value="AR"/>  
      <!-- and so on ... -->  
    </restriction>  
  </simpleType>  
</schema>  
```  
  
 Per altre informazioni sugli elementi `<xs:import />`, `<xs:include />` e `<xs:redefine />`, nonché sulle classi <xref:System.Xml.Schema.XmlSchemaImport>, <xref:System.Xml.Schema.XmlSchemaInclude> e <xref:System.Xml.Schema.XmlSchemaRedefine>, vedere il documento [W3C XML Schema](http://go.microsoft.com/fwlink/?LinkId=45242) e la documentazione di riferimento per la classe dello spazio dei nomi <xref:System.Xml.Schema?displayProperty=fullName>.  
  
## Vedere anche  
 [Cenni preliminari sul modello SOM XML](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)   
 [Lettura e scrittura di schemi XML](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)   
 [Compilazione di XML Schema](../../../../docs/standard/data/xml/building-xml-schemas.md)   
 [Attraversamento di schemi XML](../../../../docs/standard/data/xml/traversing-xml-schemas.md)   
 [Modifica di schemi XML](../../../../docs/standard/data/xml/editing-xml-schemas.md)   
 [XmlSchemaSet per la compilazione di schemi](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)