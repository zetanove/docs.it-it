---
title: "Post-Schema Compilation Infoset (PSCI, infoset sulla compilazione post-schema) | Microsoft Docs"
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
ms.assetid: 7f1bc7f4-401b-459f-9078-f099cc711fde
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Post-Schema Compilation Infoset (PSCI, infoset sulla compilazione post-schema)
Nel documento [World Wide Web Consortium \(W3C\) XML Schema Recommendation](http://go.microsoft.com/fwlink/?linkid=45242) viene illustrato il set di informazioni \(infoset\) che deve essere esposto per la convalida pre\-schema e la compilazione post\-schema.  Il modello SOM \(Schema Object Model\) XML visualizza questa esposizione prima e dopo che venga chiamato il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  
  
 L'infoset sulla convalida pre\-schema viene compilato durante la modifica dello schema.  L'infoset sulla compilazione post\-schema viene generato dopo la chiamata al metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>, durante la compilazione dello schema, e viene esposto come proprietà.  
  
 Il modello SOM è il modello a oggetti che rappresenta gli infoset di convalida pre\-schema e di compilazione post\-schema. Include le classi nello spazio dei nomi <xref:System.Xml.Schema?displayProperty=fullName>.  Tutte le proprietà di lettura e scrittura delle classi nello spazio dei nomi <xref:System.Xml.Schema> appartengono all'infoset sulla convalida pre\-schema, mentre tutte le proprietà delle classi nello spazio dei nomi <xref:System.Xml.Schema> appartengono all'infoset sulla compilazione post\-schema.  L'eccezione a questa regola è rappresentata dalle seguenti proprietà, che sono proprietà sia di infoset di convalida pre\-schema sia di infoset di compilazione post\-schema.  
  
|Classe|Proprietà|  
|------------|---------------|  
|<xref:System.Xml.Schema.XmlSchemaObject>|<xref:System.Xml.Schema.XmlSchemaObject.Parent%2A>|  
|<xref:System.Xml.Schema.XmlSchema>|<xref:System.Xml.Schema.XmlSchema.AttributeFormDefault%2A>, <xref:System.Xml.Schema.XmlSchema.BlockDefault%2A>, <xref:System.Xml.Schema.XmlSchema.ElementFormDefault%2A>, <xref:System.Xml.Schema.XmlSchema.FinalDefault%2A>, <xref:System.Xml.Schema.XmlSchema.TargetNamespace%2A>|  
|<xref:System.Xml.Schema.XmlSchemaExternal>|<xref:System.Xml.Schema.XmlSchemaExternal.Schema%2A>|  
|<xref:System.Xml.Schema.XmlSchemaAttributeGroup>|<xref:System.Xml.Schema.XmlSchemaAttributeGroup.AnyAttribute%2A>|  
|<xref:System.Xml.Schema.XmlSchemaParticle>|<xref:System.Xml.Schema.XmlSchemaParticle.MaxOccurs%2A>, <xref:System.Xml.Schema.XmlSchemaParticle.MinOccurs%2A>|  
|<xref:System.Xml.Schema.XmlSchemaComplexType>|<xref:System.Xml.Schema.XmlSchemaComplexType.AnyAttribute%2A>|  
  
 Ad esempio, sia la classe <xref:System.Xml.Schema.XmlSchemaElement> che la classe <xref:System.Xml.Schema.XmlSchemaComplexType> dispongono delle proprietà `BlockResolved` e `FinalResolved`.  Tali proprietà vengono usate per conservare i valori delle proprietà `Block` e `Final` dopo che lo schema è stato compilato e convalidato.  Le proprietà `BlockResolved` e `FinalResolved` sono di sola lettura e fanno parte dell'infoset di compilazione post\-schema.  
  
 Nell'esempio seguente viene illustrata la proprietà <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A> della classe <xref:System.Xml.Schema.XmlSchemaElement> impostata dopo la convalida dello schema.  Prima della convalida la proprietà contiene un riferimento `null` e la proprietà <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> è impostata sul nome del tipo in questione.  Dopo la convalida la proprietà <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> viene risolta in un tipo valido e l'oggetto del tipo è disponibile attraverso la proprietà <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A>.  
  
 [!code-cpp[PsciSample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/PsciSample/CPP/PsciSample.cpp#1)]
 [!code-csharp[PsciSample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/PsciSample/CS/PsciSample.cs#1)]
 [!code-vb[PsciSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/PsciSample/VB/PsciSample.vb#1)]  
  
## Vedere anche  
 [SOM \(Schema Object Model\) XML](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)