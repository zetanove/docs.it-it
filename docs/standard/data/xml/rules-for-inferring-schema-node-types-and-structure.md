---
title: "Regole per l&#39;inferenza dello schema per tipi di nodo e struttura | Microsoft Docs"
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
ms.assetid: d74ce896-717d-4871-8fd9-b070e2f53cb0
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Regole per l&#39;inferenza dello schema per tipi di nodo e struttura
In questo argomento viene descritto in che modo il processo di inferenza converte in una struttura XSD \(XML Schema Definition Language\) i tipi di nodo di un documento XML.  
  
## Regole di inferenza dell'elemento  
 Contenuto della sezione vengono descritte le regole di inferenza per le dichiarazioni dell'elemento.  Vengono inferite otto strutture di dichiarazioni dell'elemento:  
  
1.  Elemento di tipo semplice  
  
2.  Elemento vuoto  
  
3.  Elemento vuoto con attributi  
  
4.  Elemento con attributi e contenuto semplice  
  
5.  Elemento con una sequenza di elementi figlio  
  
6.  Elemento con una sequenza di elementi figlio e attributi  
  
7.  Elemento con una sequenza di opzioni di elementi figlio  
  
8.  Elemento con una sequenza di opzioni di elementi figlio e attributi  
  
> [!NOTE]
>  Tutte le dichiarazioni `complexType` sono inferite come tipi anonimi.  L'unico elemento globale inferito è l'elemento radice, tutti gli altri elementi sono locali.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
### Elemento di tipo semplice  
 Nella tabella seguente viene mostrato l'input XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> e lo schema XML generato.  L'elemento in grassetto mostra lo schema inferito per l'elemento di tipo semplice.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schema|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>text</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root" type="xs:string" />`<br /><br /> `\</xs:schema>`|  
  
### Elemento vuoto  
 Nella tabella seguente viene mostrato l'input XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> e lo schema XML generato.  L'elemento in grassetto mostra lo schema inferito per l'elemento vuoto.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schema|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<empty/>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="empty" />`<br /><br /> `\</xs:schema>`|  
  
### Elemento vuoto con attributi  
 Nella tabella seguente viene mostrato l'input XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> e lo schema XML generato.  L'elemento in grassetto mostra lo schema inferito per l'elemento vuoto con attributi.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schema|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<empty attribute1="text"/>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="empty">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### Elemento con attributi e contenuto semplice  
 Nella tabella seguente viene mostrato l'input XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> e lo schema XML generato.  Gli elementi in grassetto mostrano lo schema inferito per un elemento con attributi e contenuto semplice.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schema|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">value</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:simpleContent>`<br /><br /> `\<xs:extension base="xs:string">`<br /><br /> `\<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `\</xs:extension>`<br /><br /> `\</xs:simpleContent>`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### Elemento con una sequenza di elementi figlio  
 Nella tabella seguente viene mostrato l'input XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> e lo schema XML generato.  Gli elementi in grassetto mostrano lo schema inferito per un elemento con una sequenza di elementi figlio.  
  
> [!NOTE]
>  Anche se un elemento contiene solo un elemento figlio, viene ancora considerato come una sequenza.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schema|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>`<br /><br /> `<subElement/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:sequence>`<br /><br /> `\<xs:element name="subElement" />`<br /><br /> `\</xs:sequence>`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### Elemento con una sequenza di elementi figlio e attributi  
 Nella tabella seguente viene mostrato l'input XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> e lo schema XML generato.  Gli elementi in grassetto mostrano lo schema inferito per un elemento con una sequenza di elementi figlio e attributi.  
  
> [!NOTE]
>  Anche se un elemento contiene solo un elemento figlio, viene ancora considerato come una sequenza.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schema|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:sequence>`<br /><br /> `\<xs:element name="subElement1" />`<br /><br /> `\<xs:element name="subElement2" />`<br /><br /> `\</xs:sequence>`<br /><br /> `\<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### Elemento con una sequenza e opzioni di elementi figlio  
 Nella tabella seguente viene mostrato l'input XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> e lo schema XML generato.  Gli elementi in grassetto mostrano lo schema inferito per un elemento con una sequenza e opzione di elementi figlio.  
  
> [!NOTE]
>  L'attributo `maxOccurs` dell'elemento `xs:choice` è impostato su `"unbounded"` nello schema inferito.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schema|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root>`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `<subElement1/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:sequence>`<br /><br /> `\<xs:choice maxOccurs="unbounded">`<br /><br /> `\<xs:element name="subElement1" />`<br /><br /> `\<xs:element name="subElement2" />`<br /><br /> `\</xs:choice>`<br /><br /> `\</xs:sequence>`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### Elemento con una sequenza e opzione di elementi figlio e attributi  
 Nella tabella seguente viene mostrato l'input XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> e lo schema XML generato.  Gli elementi in grassetto mostrano lo schema inferito per un elemento con una sequenza e opzione di elementi figlio e attributi.  
  
> [!NOTE]
>  L'attributo `maxOccurs` dell'elemento `xs:choice` è impostato su `"unbounded"` nello schema inferito.  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
|XML|Schema|  
|---------|------------|  
|`<?xml version="1.0"?>`<br /><br /> `<root attribute1="text">`<br /><br /> `<subElement1/>`<br /><br /> `<subElement2/>`<br /><br /> `<subElement1/>`<br /><br /> `</root>`|`<?xml version="1.0" encoding="utf-8"?>`<br /><br /> `<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xml`<br /><br /> `ns:xs="http://www.w3.org/2001/XMLSchema">`<br /><br /> ``   `\<xs:element name="root">`<br /><br /> `\<xs:complexType>`<br /><br /> `\<xs:sequence>`<br /><br /> `\<xs:choice maxOccurs="unbounded">`<br /><br /> `\<xs:element name="subElement1" />`<br /><br /> `\<xs:element name="subElement2" />`<br /><br /> `\</xs:choice>`<br /><br /> `\</xs:sequence>`<br /><br /> `\<xs:attribute name="attribute1" type="xs:string" use="required" />`<br /><br /> `\</xs:complexType>`<br /><br /> `\</xs:element>`<br /><br /> `\</xs:schema>`|  
  
### Elaborazione degli attributi  
 Ogni volta che in un nodo viene rilevato un nuovo attributo, questo viene aggiunto alla definizione inferita del nodo con `use="required"`.  Al successivo rilevamento dello stesso nodo nell'istanza, il processo di inferenza confronterà gli attributi dell'istanza corrente con quelli già inferiti.  Se mancano alcuni nodi già inferiti nell'istanza, `use="optional"` viene aggiunto alla definizione dell'attributo.  I nuovo attributi vengono aggiunti alle dichiarazioni esistenti con `use="optional"`.  
  
### Vincoli di occorrenza  
 Durante il processo di inferenza dello schema, vengono generati gli attributi `minOccurs` e `maxOccurs`, per i componenti inferiti di uno schema, con valori uguali a `"0"` o `"1"` e `"1"` o `"unbounded"`.  I valori `"1"` e `"unbounded"` sono usati solo quando i valori `"0"` e `"1"` non sono in grado di convalidare il documento XML \(ad esempio, se `MinOccurs="0"` non descrive con precisione un elemento, si utilizzerà `minOccurs="1"`\).  
  
### Contenuto misto  
 Se in un elemento è presente contenuto misto \(ad esempio del testo frammisto a elementi\), viene generato l'attributo `mixed="true"` per la definizione del tipo complesso inferito.  
  
## Altre regole di inferenza del tipo di nodo  
 Nella tabella seguente vengono descritte le regole di inferenza per istruzioni di elaborazione, commenti, riferimenti all'entità, CDATA, tipo di documento e nodi dello spazio dei nomi.  
  
|Tipo di nodo|Conversione|  
|------------------|-----------------|  
|Istruzione di elaborazione|Ignorato.|  
|Commento|Ignorato.|  
|Riferimento all'entità|La classe <xref:System.Xml.Schema.XmlSchemaInference> non gestisce i riferimenti all'entità.  Se un documento XML contiene riferimenti all'entità, è necessario usare un lettore che espande le entità.  Ad esempio, è possibile passare un tipo <xref:System.Xml.XmlTextReader> con la proprietà <xref:System.Xml.XmlTextReader.EntityHandling%2A> impostata su <xref:System.Xml.EntityHandling> come parametro.  Se si rilevano riferimenti all'entità che il lettore non espande, viene generata un'eccezione.|  
|CDATA|Le sezioni `<![CDATA[ … ]]` di un documento XML verranno inferite come `xs:string`.|  
|Document type|Ignorato.|  
|Spazi dei nomi|Ignorato.|  
  
 Per altre informazioni sul processo di inferenza dello schema, vedere [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md).  
  
## Vedere anche  
 <xref:System.Xml.Schema.XmlSchemaInference>   
 [SOM \(Schema Object Model\) XML](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)   
 [Inferenza di uno schema XML](../../../../docs/standard/data/xml/inferring-an-xml-schema.md)   
 [Inferenza degli schemi da documenti XML](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)   
 [Regole per l'inferenza di tipi semplici](../../../../docs/standard/data/xml/rules-for-inferring-simple-types.md)