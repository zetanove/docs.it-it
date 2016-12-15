---
title: "XML Descendant Axis Property (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyDescendantsAxis"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, accessing XML"
  - "XML descendant axis property [Visual Basic]"
  - "descendant axis property [Visual Baisc]"
  - "XML axis [Visual Basic], descendant"
  - "XML [Visual Basic], accessing"
ms.assetid: a178f85b-5d54-438f-8479-40b62af6fe76
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML Descendant Axis Property (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Fornisce l'accesso ai discendenti di uno dei seguenti oggetti: oggetto <xref:System.Xml.Linq.XElement>, oggetto <xref:System.Xml.Linq.XDocument>, raccolta di oggetti <xref:System.Xml.Linq.XElement>, raccolta di oggetti <xref:System.Xml.Linq.XDocument>.  
  
## Sintassi  
  
```  
  
object...<descendant>  
```  
  
## Parti  
 `object`  
 Obbligatorio.  Un oggetto <xref:System.Xml.Linq.XElement>, un oggetto <xref:System.Xml.Linq.XDocument>, una raccolta di oggetti <xref:System.Xml.Linq.XElement> o una raccolta di oggetti <xref:System.Xml.Linq.XDocument>  
  
 ...\<  
 Obbligatorio.  Indica l'inizio di una proprietà axis descendant.  
  
 `descendant`  
 Obbligatorio.  Nome dei nodi discendenti a cui accedere, nel formato \[`prefix``:`\]`name`.  
  
|Parte|Descrizione|  
|-----------|-----------------|  
|`prefix`|Parametro facoltativo.  Prefisso dello spazio dei nomi XML per il nodo discendente.  Deve essere un spazio dei nomi XML globale definito utilizzando un'istruzione `Imports`.|  
|`name`|Obbligatorio.  Nome locale del nodo discendente.  Vedere [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).|  
  
 \>  
 Obbligatorio.  Indica la fine di una proprietà axis descendant.  
  
## Valore restituito  
 Raccolta di oggetti <xref:System.Xml.Linq.XElement>.  
  
## Note  
 È possibile utilizzare una proprietà axis descendant XML per accedere a nodi discendenti in base al nome, da un oggetto <xref:System.Xml.Linq.XElement> o da un oggetto <xref:System.Xml.Linq.XDocument> o da raccolte di oggetti <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument>.  Utilizzare la proprietà `Value` per accedere al valore del primo nodo discendente nella raccolta restituito.  Per ulteriori informazioni, vedere [XML Value Property](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
 Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte le proprietà axis discendenti in chiamate al metodo <xref:System.Xml.Linq.XContainer.Descendants%2A>.  
  
## Spazi dei nomi XML  
 Il nome in una proprietà axis descendant può utilizzare solo spazi dei nomi XML dichiarati globalmente con l'istruzione `Imports`.  Non può utilizzare spazi dei nomi XML dichiarati localmente all'interno di valori letterali dell'elemento XML.  Per ulteriori informazioni, vedere [Imports Statement \(XML Namespace\)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
## Esempio  
 Nell'esempio seguente viene mostrato come accedere al valore del primo nodo discendente denominato `name` e ai valori di tutti i nodi discendenti denominati `phone` dall'oggetto `contacts`.  
  
 [!code-vb[VbXMLSamples#25](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-descendant-axis-property_1.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `Name: Patrick Hines`  
  
 `Home Phone = 206-555-0144`  
  
## Esempio  
 Nell'esempio riportato di seguito viene dichiarato `ns` come un prefisso dello spazio dei nomi XML.  Viene utilizzato quindi il prefisso dello spazio dei nomi per creare un valore letterale XML e accedere al valore del primo nodo figlio con il nome completo `ns:name`.  
  
 [!code-vb[VbXMLSamples#26](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-descendant-axis-property_2.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `Name: Patrick Hines`  
  
## Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)