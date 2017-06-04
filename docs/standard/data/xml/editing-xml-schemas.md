---
title: "Modifica di schemi XML | Microsoft Docs"
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
ms.assetid: fa09c8e5-c2b9-49d2-bb0d-40330cd13e4d
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Modifica di schemi XML
La modifica di uno schema XML rappresenta una delle funzionalità più importanti del modello SOM \(Schema Object Model\).  È possibile usare tutte le proprietà del modello SOM precedenti alla compilazione dello schema per modificare i valori esistenti in uno schema XML.  Sarà quindi possibile ricompilare lo schema XML per riflettere le modifiche.  
  
 Il primo passaggio della modifica di uno schema caricato nel modello SOM consiste nell'attraversare lo schema.  Prima di tentare di modificare uno schema, è necessario essere in grado di attraversare uno schema usando un'API del SOM.  È necessario inoltre conoscere le proprietà del set PSCI \(Post\-Schema\-Compilation\-Infoset\) precedenti e successive alla compilazione dello schema.  
  
## Modifica di uno schema XML  
 Contenuto della sezione vengono forniti due esempi di codice che consentono di modificare lo schema del cliente creato nell'argomento [Compilazione di XML Schema](../../../../docs/standard/data/xml/building-xml-schemas.md).  Il primo esempio di codice aggiunge un nuovo elemento `PhoneNumber` all'elemento `Customer`, mentre il secondo aggiunge un nuovo attributo `Title` all'elemento `FirstName`.  Nel primo esempio, inoltre, per attraversare lo schema del cliente, viene usata la raccolta <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName> successiva alla compilazione dello schema, mentre nel secondo esempio di codice viene usata la raccolta <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> precedente alla compilazione dello schema.  
  
### Esempio dell'elemento PhoneNumber  
 Il primo esempio di codice aggiunge un nuovo elemento `PhoneNumber` all'elemento `Customer` dello schema del cliente.  L'esempio di codice consente di modificare lo schema del cliente eseguendo i passaggi seguenti.  
  
1.  Aggiunge lo schema del cliente a un nuovo oggetto <xref:System.Xml.Schema.XmlSchemaSet>, quindi lo compila.  Eventuali avvisi ed errori di convalida dello schema rilevati durante la lettura e la compilazione dello schema vengono gestiti dal delegato <xref:System.Xml.Schema.ValidationEventHandler>.  
  
2.  Recupera l'oggetto <xref:System.Xml.Schema.XmlSchema> compilato dal tipo <xref:System.Xml.Schema.XmlSchemaSet> scorrendo la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>.  Dal momento che lo schema è stato compilato, è possibile accedere alle proprietà di PSCI \(Post\-Schema\-Compilation\-Infoset\).  
  
3.  Crea l'elemento `PhoneNumber` mediante la classe <xref:System.Xml.Schema.XmlSchemaElement>, la restrizione del tipo semplice `xs:string` mediante le classi <xref:System.Xml.Schema.XmlSchemaSimpleType> e <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction>, aggiunge un facet pattern alla proprietà <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction.Facets%2A> della restrizione, quindi aggiunge la restrizione alla proprietà <xref:System.Xml.Schema.XmlSchemaSimpleType.Content%2A> del tipo semplice e il tipo semplice alla proprietà <xref:System.Xml.Schema.XmlSchemaElement.SchemaType%2A> dell'elemento `PhoneNumber`.  
  
4.  Scorre ciascun tipo <xref:System.Xml.Schema.XmlSchemaElement> nella raccolta <xref:System.Xml.Schema.XmlSchemaObjectTable.Values%2A> della raccolta <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName> successiva alla compilazione dello schema.  
  
5.  Se la proprietà <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A> dell'elemento è `"Customer"`, recupera il tipo complesso dell'elemento `Customer` mediante la classe <xref:System.Xml.Schema.XmlSchemaComplexType> e la particella di sequenza del tipo complesso mediante la classe <xref:System.Xml.Schema.XmlSchemaSequence>.  
  
6.  Aggiunge il nuovo elemento `PhoneNumber` alla sequenza contenente gli elementi `FirstName` e `LastName` esistenti usando la raccolta <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A> precedente allo schema della sequenza.  
  
7.  Infine, rielabora e compila l'oggetto modificato <xref:System.Xml.Schema.XmlSchema> usando i metodi <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> e <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> della classe <xref:System.Xml.Schema.XmlSchemaSet> e lo scrive nella console.  
  
 Di seguito è riportato l'esempio di codice completo.  
  
 [!code-cpp[XmlSchemaEditExample1#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaEditExample1/CPP/XmlSchemaEditExample1.cpp#1)]
 [!code-csharp[XmlSchemaEditExample1#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaEditExample1/CS/XmlSchemaEditExample1.cs#1)]
 [!code-vb[XmlSchemaEditExample1#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaEditExample1/VB/XmlSchemaEditExample1.vb#1)]  
  
 Di seguito è riportato lo schema modificato del cliente e creato nell'argomento [Compilazione di XML Schema](../../../../docs/standard/data/xml/building-xml-schemas.md).  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:element name="Customer">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="FirstName" type="xs:string" />  
        <xs:element name="LastName" type="tns:LastNameType" />  
        <xs:element name="PhoneNumber">  
          <xs:simpleType>  
            <xs:restriction base="xs:string">  
              <xs:pattern value="\d{3}-\d{3}-\d(4)" />  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:element>  
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
```  
  
### Esempio dell'attributo Title  
 Il secondo esempio di codice aggiunge un nuovo attributo `Title` all'elemento `FirstName` dello schema del cliente.  Nel primo esempio di codice il tipo dell'elemento `FirstName` è `xs:string`.  Per fare in modo che l'elemento `FirstName` presenti un attributo e un contenuto di stringa, è necessario modificarne il tipo impostandolo su un tipo complesso con un modello di contenuto derivato dall'estensione di contenuto semplice.  
  
 L'esempio di codice consente di modificare lo schema del cliente eseguendo i passaggi seguenti.  
  
1.  Aggiunge lo schema del cliente a un nuovo oggetto <xref:System.Xml.Schema.XmlSchemaSet>, quindi lo compila.  Eventuali avvisi ed errori di convalida dello schema rilevati durante la lettura e la compilazione dello schema vengono gestiti dal delegato <xref:System.Xml.Schema.ValidationEventHandler>.  
  
2.  Recupera l'oggetto <xref:System.Xml.Schema.XmlSchema> compilato dal tipo <xref:System.Xml.Schema.XmlSchemaSet> scorrendo la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>.  Dal momento che lo schema è stato compilato, è possibile accedere alle proprietà di PSCI \(Post\-Schema\-Compilation\-Infoset\).  
  
3.  Crea un nuovo tipo complesso per l'elemento `FirstName` usando la classe <xref:System.Xml.Schema.XmlSchemaComplexType>.  
  
4.  Crea una nuova estensione di contenuto semplice, con un tipo di base di `xs:string`, usando le classi <xref:System.Xml.Schema.XmlSchemaSimpleContent> e <xref:System.Xml.Schema.XmlSchemaSimpleContentExtension>.  
  
5.  Crea il nuovo attributo `Title` usando la classe <xref:System.Xml.Schema.XmlSchemaAttribute>, con una proprietà <xref:System.Xml.Schema.XmlSchemaAttribute.SchemaTypeName%2A> di `xs:string` e aggiunge l'attributo all'estensione di contenuto semplice.  
  
6.  Imposta il modello di contenuto del contenuto semplice sull'estensione di contenuto semplice e il modello di contenuto del tipo complesso sul contenuto semplice.  
  
7.  Aggiunge il nuovo tipo complesso alla raccolta <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> precedente alla compilazione dello schema.  
  
8.  Scorre ciascun tipo <xref:System.Xml.Schema.XmlSchemaObject> nella raccolta <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> precedente alla compilazione dello schema.  
  
> [!NOTE]
>  Dal momento che l'elemento `FirstName` non è un elemento globale nello schema, non è disponibile nella raccolta <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> o <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName>.  L'esempio di codice individua l'elemento `FirstName` dopo aver individuato l'elemento `Customer`.  
>   
>  Nel primo esempio di codice lo schema era stato attraversato usando la raccolta <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName> successiva alla compilazione dello schema.  In questo esempio, per attraversare lo schema viene usata la raccolta <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName> precedente alla compilazione dello schema.  Mentre entrambe le raccolte forniscono l'accesso agli elementi globali dello schema, lo scorrimento della raccolta <xref:System.Xml.Schema.XmlSchema.Items%2A> richiede più tempo, poiché è necessario scorrere tutti gli elementi globali dello schema e poiché non sono presenti proprietà PSCI.  Le raccolte PSCI \(le proprietà <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=fullName>, <xref:System.Xml.Schema.XmlSchema.Attributes%2A?displayProperty=fullName>, <xref:System.Xml.Schema.XmlSchema.SchemaTypes%2A?displayProperty=fullName> e così via\) forniscono l'accesso diretto agli elementi, agli attributi, ai tipi globali e alle relative proprietà PSCI.  
  
1.  Se la proprietà <xref:System.Xml.Schema.XmlSchemaObject> è un elemento la cui proprietà <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A> è `"Customer"`, vengono recuperati il tipo complesso dell'elemento `Customer` mediante la classe <xref:System.Xml.Schema.XmlSchemaComplexType> e la particella di sequenza del tipo complesso mediante la classe <xref:System.Xml.Schema.XmlSchemaSequence>.  
  
2.  Scorre ciascun tipo <xref:System.Xml.Schema.XmlSchemaParticle> nella raccolta <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A?displayProperty=fullName> precedente alla compilazione dello schema.  
  
3.  Se il tipo <xref:System.Xml.Schema.XmlSchemaParticle> è un elemento e la relativa proprietà <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A> è `"FirstName"`, imposta la proprietà <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> dell'elemento `FirstName` su nuovo tipo complesso `FirstName`.  
  
4.  Infine, rielabora e compila l'oggetto modificato <xref:System.Xml.Schema.XmlSchema> usando i metodi <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> e <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> della classe <xref:System.Xml.Schema.XmlSchemaSet> e lo scrive nella console.  
  
 Di seguito è riportato l'esempio di codice completo.  
  
 [!code-cpp[XmlSchemaEditExample2#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaEditExample2/CPP/XmlSchemaEditExample2.cpp#1)]
 [!code-csharp[XmlSchemaEditExample2#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaEditExample2/CS/XmlSchemaEditExample2.cs#1)]
 [!code-vb[XmlSchemaEditExample2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaEditExample2/VB/XmlSchemaEditExample2.vb#1)]  
  
 Di seguito è riportato lo schema modificato del cliente e creato nell'argomento [Compilazione di XML Schema](../../../../docs/standard/data/xml/building-xml-schemas.md).  
  
```  
<?xml version="1.0" encoding=" utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:element name="Customer">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="FirstName" type="tns:FirstNameComplexType" />  
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
  <xs:complexType name="FirstNameComplexType">  
    <xs:simpleContent>  
      <xs:extension base="xs:string">  
        <xs:attribute name="Title" type="xs:string" />  
      </xs:extension>  
    </xs:simpleContent>  
  </xs:complexType>  
</xs:schema>  
```  
  
## Vedere anche  
 [Cenni preliminari sul modello SOM XML](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)   
 [Lettura e scrittura di schemi XML](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)   
 [Compilazione di XML Schema](../../../../docs/standard/data/xml/building-xml-schemas.md)   
 [Attraversamento di schemi XML](../../../../docs/standard/data/xml/traversing-xml-schemas.md)   
 [Inclusione o importazione di schemi XML](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)   
 [XmlSchemaSet per la compilazione di schemi](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)   
 [Post\-Schema Compilation Infoset \(PSCI, infoset sulla compilazione post\-schema\)](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)