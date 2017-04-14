---
title: "Inferenza degli schemi da documenti XML | Microsoft Docs"
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
ms.assetid: f3d97d53-614d-4a04-a174-87965b7405f6
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Inferenza degli schemi da documenti XML
In questo argomento viene descritto come usare la classe <xref:System.Xml.Schema.XmlSchemaInference> per inferire uno schema XSD \(XML Schema Definition Language\) dalla struttura di un documento XML.  
  
## Processo di inferenza dello schema  
 La classe <xref:System.Xml.Schema.XmlSchemaInference> dello spazio dei nomi <xref:System.Xml.Schema?displayProperty=fullName> è usata per generare uno o più schemi XSD \(XML Schema definition language\) dalla struttura di un documento XML.  È possibile usare gli schemi generati per convalidare il documento XML originale.  
  
 Quando un documento XML viene elaborato dalla classe <xref:System.Xml.Schema.XmlSchemaInference>, la classe <xref:System.Xml.Schema.XmlSchemaInference> ipotizza i componenti dello schema che descrivono gli elementi e gli attributi nel documento XML.  La classe <xref:System.Xml.Schema.XmlSchemaInference> inferisce inoltre i componenti dello schema in modo vincolante inferendo il tipo più restrittivo per un determinato elemento o attributo.  Una volta raccolta una quantità maggiore di informazioni sul documento XML, tali vincoli vengono sciolti inferendo tipi meno restrittivi.  Il tipo meno restrittivo che è possibile inferire è `xs:string`.  
  
 Si consideri, ad esempio, la seguente parte di un documento XML.  
  
```  
<parent attribute1="6">  
    <child>One</child>  
    <child>Two</child>  
</parent>  
<parent attribute1="A">  
```  
  
 Nell'esempio precedente, quando viene rilevato l'attributo `attribute1` con un valore uguale a `6` dal processo <xref:System.Xml.Schema.XmlSchemaInference>, si presuppone che sia del tipo `xs:unsignedByte`.  Quando viene rilevato il secondo elemento `parent` dal processo <xref:System.Xml.Schema.XmlSchemaInference>, il vincolo viene allentato modificando il tipo in `xs:string`, in quanto il valore dell'attributo `attribute1` è ora uguale a `A`.  Analogamente, l'attributo `minOccurs` per tutti gli elementi `child` inferiti nello schema viene allentato impostandolo su `minOccurs="0"`, in quanto il secondo elemento padre non contiene elementi figlio.  
  
## Inferenza degli schemi da documenti XML  
 La classe <xref:System.Xml.Schema.XmlSchemaInference> usa due metodi <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> di overload per inferire uno schema da un documento XML.  
  
 Il primo metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=fullName> viene usato per creare uno schema basato su un documento XML.  Il secondo metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=fullName> viene usato per inferire uno schema che descrive più documenti XML.  Ad esempio, è possibile aggiungere uno alla volta più documenti XML nel metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=fullName> per ottenere uno schema che descrive l'intero set di documenti XML.  
  
 Il primo metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=fullName> inferisce lo schema da un documento XML contenuto in un oggetto <xref:System.Xml.XmlReader> e restituisce un oggetto <xref:System.Xml.Schema.XmlSchemaSet> contenente lo schema inferito.  Il secondo metodo <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=fullName> cerca un oggetto <xref:System.Xml.Schema.XmlSchemaSet> per uno schema con lo stesso spazio dei nomi di destinazione del documento XML contenuto nell'oggetto <xref:System.Xml.XmlReader>, ottimizza lo schema esistente e restituisce un oggetto <xref:System.Xml.Schema.XmlSchemaSet> contenente lo schema inferito.  
  
 Le modifiche apportate allo schema ottimizzato sono basate sulla nuova struttura rilevata nel documento XML.  Ad esempio, quando si scorre un documento XML, si ipotizzano i tipi di dati rilevati e lo schema viene creato in base a tali ipotesi.  Tuttavia, se i dati vengono rilevati in un secondo passaggio del processo di inferenza che differisce dall'ipotesi iniziale, lo schema viene ridefinito.  Nell'esempio seguente viene illustrato questo processo.  
  
 [!code-cpp[XmlSchemaInferenceExamples#4](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaInferenceExamples/CPP/XmlSchemaInferenceExamples.cpp#4)]
 [!code-csharp[XmlSchemaInferenceExamples#4](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaInferenceExamples/CS/XmlSchemaInferenceExamples.cs#4)]
 [!code-vb[XmlSchemaInferenceExamples#4](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaInferenceExamples/VB/XmlSchemaInferenceExamples.vb#4)]  
  
 Nell'esempio il file `item1.xml` viene considerato come primo input.  
  
 [!code-xml[XmlSchemaInferenceExamples#13](../../../../samples/snippets/xml/VS_Snippets_Data/XmlSchemaInferenceExamples/XML/item1.xml#13)]  
  
 Il file `item2.xml` viene quindi considerato come secondo input:  
  
 [!code-xml[XmlSchemaInferenceExamples#14](../../../../samples/snippets/xml/VS_Snippets_Data/XmlSchemaInferenceExamples/XML/item2.xml#14)]  
  
 Quando viene rilevato l'attributo `productID` nel primo documento XML, si presuppone che il valore `123456789` sia del tipo `xs:unsignedInt`.  Tuttavia, quando viene letto il secondo documento XML e viene rilevato un valore uguale a `A53-246`, non è più possibile presupporre il tipo `xs:unsignedInt`.  Lo schema viene ridefinito e il tipo `productID` viene modificato in `xs:string`.  Inoltre, l'attributo `minOccurs` per l'elemento `supplierID` è impostato su `0`, in quanto il secondo documento XML non contiene alcun elemento `supplierID`.  
  
 Lo schema seguente è lo schema inferito dal primo documento XML.  
  
 [!code-xml[XmlSchemaInferenceExamples#15](../../../../samples/snippets/xml/VS_Snippets_Data/XmlSchemaInferenceExamples/XML/InferSchema1.xml#15)]  
  
 Lo schema seguente è lo schema inferito dal primo documento XML, ridefinito dal secondo documento XML.  
  
 [!code-xml[XmlSchemaInferenceExamples#16](../../../../samples/snippets/xml/VS_Snippets_Data/XmlSchemaInferenceExamples/XML/InferSchema2.xml#16)]  
  
## Schemi inline  
 Se viene rilevato uno schema XSD inline durante il processo <xref:System.Xml.Schema.XmlSchemaInference>, viene generata l'eccezione <xref:System.Xml.Schema.XmlSchemaInferenceException>.  Ad esempio, nel seguente schema inline viene generata un'eccezione <xref:System.Xml.Schema.XmlSchemaInferenceException>.  
  
```  
<root xmlns:ex="http://www.contoso.com" xmlns="http://www.tempuri.org">  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="http://www.contoso.com">  
        <xs:element name="Contoso" type="xs:normalizedString" />  
    </xs:schema>  
    <ex:Contoso>Test</ex:Contoso>  
</root>  
```  
  
## Schemi che non possono essere ridefiniti  
 Esistono costrutti di schemi W3C XML che il processo XSD \(XML Schema definition language\) <xref:System.Xml.Schema.XmlSchemaInference> non è in grado di gestire se si tratta di ridefinire un tipo e viene quindi generata un'eccezione.  Un esempio è un tipo particolarmente complesso il cui compositor di livello principale è diverso da una sequenza.  Nel SOM \(Schema Object Model\), ciò corrisponde a un tipo <xref:System.Xml.Schema.XmlSchemaComplexType> la cui proprietà <xref:System.Xml.Schema.XmlSchemaComplexType.Particle%2A> non è un'istanza del tipo <xref:System.Xml.Schema.XmlSchemaSequence>.  
  
## Vedere anche  
 <xref:System.Xml.Schema.XmlSchemaInference>   
 [SOM \(Schema Object Model\) XML](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)   
 [Inferenza di uno schema XML](../../../../docs/standard/data/xml/inferring-an-xml-schema.md)   
 [Regole per l'inferenza dello schema per tipi di nodo e struttura](../../../../docs/standard/data/xml/rules-for-inferring-schema-node-types-and-structure.md)   
 [Regole per l'inferenza di tipi semplici](../../../../docs/standard/data/xml/rules-for-inferring-simple-types.md)