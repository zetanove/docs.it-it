---
title: "Compilazione di XML Schema | Microsoft Docs"
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
ms.assetid: 8a5ea56c-0140-4b51-8997-875ae6a8e0cb
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Compilazione di XML Schema
Le classi nello spazio dei nomi <xref:System.Xml.Schema?displayProperty=fullName> sono associate alle strutture definite nella raccomandazione W3C \(World Wide Web Consortium\) XML Schema e possono essere usate per compilare schemi XML in memoria.  
  
## Compilazione di un XML Schema  
 Nei seguenti esempi di codice, per compilare in memoria uno schema XML del cliente viene usata l'API del modello SOM \(Schema Object Model\).  
  
### Creazione di elementi e attributi  
 Negli esempi di codice, lo schema del cliente viene compilato dal basso verso l'alto, ovvero vengono creati prima gli elementi e gli attributi figlio con i tipi corrispondenti, poi gli elementi principali.  
  
 Nel seguente esempio di codice gli elementi `FirstName`, `LastName` e l'attributo `CustomerId` dello schema del cliente vengono creati usando le classi <xref:System.Xml.Schema.XmlSchemaElement> e <xref:System.Xml.Schema.XmlSchemaAttribute> del modello SOM.  A parte le proprietà <xref:System.Xml.Schema.XmlSchemaElement.Name%2A> delle classi <xref:System.Xml.Schema.XmlSchemaElement> e <xref:System.Xml.Schema.XmlSchemaAttribute>, che corrispondono all'attributo "name" degli elementi `<xs:element />` e `<xs:attribute />` in XML Schema, tutti gli altri attributi consentiti dallo schema \(`defaultValue`, `fixedValue`, `form` e così via\) contengono le proprietà corrispondenti nelle classi <xref:System.Xml.Schema.XmlSchemaElement> e <xref:System.Xml.Schema.XmlSchemaAttribute>.  
  
 [!code-cpp[XmlSchemaCreateExample#2](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaCreateExample/CPP/XmlSchemaCreateExample.cpp#2)]
 [!code-csharp[XmlSchemaCreateExample#2](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaCreateExample/CS/XmlSchemaCreateExample.cs#2)]
 [!code-vb[XmlSchemaCreateExample#2](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaCreateExample/VB/XmlSchemaCreateExample.vb#2)]  
  
### Creazione di tipi di schema  
 Il contenuto degli elementi e degli attributi è definito dai relativi tipi.  Per creare elementi e attributi i cui tipi corrispondano a uno dei tipi incorporati nello schema, la proprietà <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> della classe <xref:System.Xml.Schema.XmlSchemaElement> o <xref:System.Xml.Schema.XmlSchemaAttribute> viene impostata con il nome completo corrispondente del tipo incorporato usando la classe <xref:System.Xml.XmlQualifiedName>.  Per creare un tipo definito dall'utente per gli elementi e gli attributi, viene creato un nuovo tipo semplice o complesso usando la classe <xref:System.Xml.Schema.XmlSchemaSimpleType> o <xref:System.Xml.Schema.XmlSchemaComplexType>.  
  
> [!NOTE]
>  Per creare tipi semplici o complessi senza nomi che siano elementi o attributi figlio anonimi di un elemento o attributo \(agli attributi è possibile applicare solo tipi semplici\), invece di impostare la proprietà <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> della classe <xref:System.Xml.Schema.XmlSchemaElement> o <xref:System.Xml.Schema.XmlSchemaAttribute>, impostare la proprietà <xref:System.Xml.Schema.XmlSchemaElement.SchemaType%2A> sul tipo complesso o semplice senza nome.  
  
 Gli schemi XML consentono di derivare per restrizione da altri tipi semplici \(incorporati o definiti dall'utente\) sia i tipi semplici anonimi sia i tipi semplici denominati oppure di crearli come un elenco o un'unione di altri tipi semplici.  La classe <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction> consente di creare un tipo semplice per restrizione dal tipo `xs:string` incorporato.  Per creare tipi di unione o di elenco, è possibile usare anche la classe <xref:System.Xml.Schema.XmlSchemaSimpleTypeList> o <xref:System.Xml.Schema.XmlSchemaSimpleTypeUnion>.  La proprietà <xref:System.Xml.Schema.XmlSchemaSimpleType.Content%2A?displayProperty=fullName> indica se è una restrizione, un elenco o un'unione di tipi semplici.  
  
 Nel seguente esempio di codice il tipo dell'elemento `FirstName` è un tipo `xs:string` incorporato, il tipo dell'elemento `LastName` è un tipo semplice denominato che è una restrizione del tipo `xs:string` incorporato, il valore del facet `MaxLength` è 20 e il tipo dell'attributo `CustomerId` è il tipo `xs:positiveInteger` incorporato.  L'elemento `Customer` è un tipo complesso anonimo la cui particella è rappresentata dalla sequenza degli elementi `FirstName` e `LastName` e i cui attributi contengono l'attributo `CustomerId`.  
  
> [!NOTE]
>  È inoltre possibile usare le classi <xref:System.Xml.Schema.XmlSchemaChoice> o <xref:System.Xml.Schema.XmlSchemaAll> come particella del tipo complesso per replicare la semantica `<xs:choice />` o `<xs:all />`.  
  
 [!code-cpp[XmlSchemaCreateExample#3](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaCreateExample/CPP/XmlSchemaCreateExample.cpp#3)]
 [!code-csharp[XmlSchemaCreateExample#3](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaCreateExample/CS/XmlSchemaCreateExample.cs#3)]
 [!code-vb[XmlSchemaCreateExample#3](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaCreateExample/VB/XmlSchemaCreateExample.vb#3)]  
  
### Creazione e compilazione di schemi  
 A questo punto, usando l'API del modello SOM, sono stati creati in memoria gli elementi e attributi figlio, i tipi corrispondenti e l'elemento di livello principale `Customer`.  Nel seguente esempio di codice l'elemento dello schema viene creato usando la classe <xref:System.Xml.Schema.XmlSchema>, vi vengono aggiunti i tipi e gli elementi di livello principale tramite la proprietà <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=fullName>, quindi lo schema completo viene compilato usando la classe <xref:System.Xml.Schema.XmlSchemaSet> e viene scritto nella console.  
  
 [!code-cpp[XmlSchemaCreateExample#4](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaCreateExample/CPP/XmlSchemaCreateExample.cpp#4)]
 [!code-csharp[XmlSchemaCreateExample#4](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaCreateExample/CS/XmlSchemaCreateExample.cs#4)]
 [!code-vb[XmlSchemaCreateExample#4](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaCreateExample/VB/XmlSchemaCreateExample.vb#4)]  
  
 Il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A?displayProperty=fullName> convalida lo schema del cliente in base alle regole per gli schemi XML e rende disponibili le proprietà successive alla compilazione dello schema.  
  
> [!NOTE]
>  Tutte le proprietà nell'API del modello SOM successive alla compilazione dello schema sono diverse dall'infoset sulla convalida post\-schema.  
  
 Il tipo <xref:System.Xml.Schema.ValidationEventHandler> aggiunto al tipo <xref:System.Xml.Schema.XmlSchemaSet> è un delegato che chiama il metodo di callback `ValidationCallback` per gestire gli avvisi e gli errori di convalida dello schema.  
  
 Di seguito è riportato l'esempio di codice completo e lo schema del cliente scritto nella console.  
  
 [!code-cpp[XmlSchemaCreateExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaCreateExample/CPP/XmlSchemaCreateExample.cpp#1)]
 [!code-csharp[XmlSchemaCreateExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaCreateExample/CS/XmlSchemaCreateExample.cs#1)]
 [!code-vb[XmlSchemaCreateExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaCreateExample/VB/XmlSchemaCreateExample.vb#1)]  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
   <xs:element name="Customer">  
      <xs:complexType>  
         <xs:sequence>  
            <xs:element name="FirstName" type="xs:string" />  
            <xs:element name="LastName" type="tns:LastNameType" />  
         </xs:sequence>  
         <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" />  
      </xs:complexType>  
   </xs:element>  
   <xs:simpleType name="LastNameType">  
      <xs:restriction base="xs:string">  
         <xs:maxLength value="20" />  
      </xs:restriction>  
   </xs:simpleType>  
</xs:schema>  
```  
  
## Vedere anche  
 [Cenni preliminari sul modello SOM XML](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)   
 [Lettura e scrittura di schemi XML](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)   
 [Attraversamento di schemi XML](../../../../docs/standard/data/xml/traversing-xml-schemas.md)   
 [Modifica di schemi XML](../../../../docs/standard/data/xml/editing-xml-schemas.md)   
 [Inclusione o importazione di schemi XML](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)   
 [XmlSchemaSet per la compilazione di schemi](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)   
 [Post\-Schema Compilation Infoset \(PSCI, infoset sulla compilazione post\-schema\)](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)