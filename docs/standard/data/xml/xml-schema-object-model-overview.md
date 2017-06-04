---
title: "Cenni preliminari sul modello SOM XML | Microsoft Docs"
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
ms.assetid: 896a1e12-5655-42c6-8cdd-89c12862b34b
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Cenni preliminari sul modello SOM XML
Il modello SOM \(Schema Object Model\) in Microsoft .NET Framework è un'API completa che consente di creare, modificare e convalidare schemi a livello di programmazione.  L'API del modello SOM agisce sui documenti di schema XML in modo simile a come il DOM agisce sui documenti XML.  I documenti di schema XML sono file XML validi che, una volta caricati nell'API del modello SOM, contengono informazioni sulla struttura e la validità di altri documenti XML conformi allo schema.  
  
 Uno schema è un documento XML che definisce una classe di documenti XML specificando la struttura o il modello dei documenti XML per un determinato schema.  Uno schema identifica i vincoli sul contenuto dei documenti XML e descrive il vocabolario \(regole o grammatica\) che i documenti XML conformi devono seguire per essere considerati validi con quel determinato schema.  La convalida di un documento XML è il processo che garantisce che il documento sia conforme alla grammatica specificata dallo schema.  
  
 Di seguito vengono illustrati alcuni modi con cui l'API SOM in .NET Framework consente di creare, modificare e convalidare gli schemi.  
  
-   Caricare e salvare schemi validi da e in file.  
  
-   Creare schemi in memoria usando classi tipizzate in modo sicuro.  
  
-   Interagire con la classe <xref:System.Xml.Schema.XmlSchemaSet> per inserire nella cache, compilare e recuperare schemi.  
  
-   Interagire con il metodo <xref:System.Xml.XmlReader.Create%2A> della classe <xref:System.Xml.XmlReader> per convalidare documenti di istanza XML rispetto a schemi.  
  
-   Compilare editor per la creazione e la conservazione di schemi.  
  
-   Modificare in modo dinamico uno schema che può essere reso conforme e salvato per la convalida di documenti di istanza XML.  
  
## Schema Object Model \(SOM\)  
 Il modello SOM include una vasta gamma di classi nello spazio dei nomi <xref:System.Xml.Schema?displayProperty=fullName> che corrispondono agli elementi in uno schema XML.  Ad esempio, l'elemento `<xsd:schema>...</xsd:schema>` è associato alla classe <xref:System.Xml.Schema.XmlSchema?displayProperty=fullName> e tutte le informazioni che possono essere contenute in un elemento `<xsd:schema/>` possono essere rappresentate usando la classe <xref:System.Xml.Schema.XmlSchema>.  Analogamente, gli elementi `<xsd:element>...</xsd:element>` e `<xsd:attribute>...</xsd:attribute>` sono associati rispettivamente alle classi <xref:System.Xml.Schema.XmlSchemaElement?displayProperty=fullName> e <xref:System.Xml.Schema.XmlSchemaAttribute?displayProperty=fullName>.  Questa associazione continua per tutti gli elementi di uno schema XML creando un modello SOM XML nello spazio dei nomi <xref:System.Xml.Schema> mostrato nel diagramma seguente.  
  
 ![Modello a oggetti Xml.Schema](../../../../docs/standard/data/xml/media/xmlschemaobjmodeloverview.png "XMLSchemaObjModelOverview")  
  
 Per altre informazioni su ogni classe nello spazio dei nomi <xref:System.Xml.Schema>, vedere la documentazione di riferimento relativa allo spazio dei nomi <xref:System.Xml.Schema> nella libreria di classi di .NET Framework.  
  
## Vedere anche  
 [Lettura e scrittura di schemi XML](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)   
 [Compilazione di XML Schema](../../../../docs/standard/data/xml/building-xml-schemas.md)   
 [Attraversamento di schemi XML](../../../../docs/standard/data/xml/traversing-xml-schemas.md)   
 [Modifica di schemi XML](../../../../docs/standard/data/xml/editing-xml-schemas.md)   
 [Inclusione o importazione di schemi XML](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)   
 [XmlSchemaSet per la compilazione di schemi](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)   
 [Post\-Schema Compilation Infoset \(PSCI, infoset sulla compilazione post\-schema\)](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)