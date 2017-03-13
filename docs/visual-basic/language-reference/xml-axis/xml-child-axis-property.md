---
title: "XML Child Axis Property (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyChildAxis"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, accessing XML"
  - "XML axis [Visual Basic], child"
  - "child axis property [Visual Basic]"
  - "XML child axis property [Visual Basic]"
  - "XML [Visual Basic], accessing"
ms.assetid: 89a59d00-985e-4f5c-b59f-29b47bad11cb
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# XML Child Axis Property (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Fornisce l'accesso agli elementi figlio di uno dei seguenti oggetti: <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XDocument>, raccolta di <xref:System.Xml.Linq.XElement> o raccolta di <xref:System.Xml.Linq.XDocument>.  
  
## Sintassi  
  
```  
  
object.<child>  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`object`|Necessario.  Un oggetto <xref:System.Xml.Linq.XElement>, un oggetto <xref:System.Xml.Linq.XDocument>, una raccolta di oggetti <xref:System.Xml.Linq.XElement> o una raccolta di oggetti <xref:System.Xml.Linq.XDocument>.|  
|.\<|Obbligatorio.  Indica l'inizio di una proprietà axis dell'elemento figlio.|  
|`child`|Necessario.  Nome dei nodi figlio a cui accedere, nel formato \[`prefix``:`\]`name`.<br /><br /> -   `Prefix` \- Facoltativo.  Prefisso dello spazio dei nomi XML per il nodo figlio.  Deve essere uno spazio dei nomi XML globale definito usando un'istruzione `Imports`.<br />-   `Name` \- Obbligatorio.  Nome del nodo figlio locale.  Vedere [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).|  
|\>|Obbligatorio.  Indica la fine di una proprietà axis dell'elemento figlio.|  
  
## Valore restituito  
 Raccolta di oggetti <xref:System.Xml.Linq.XElement>.  
  
## Note  
 È possibile usare una proprietà axis dell'elemento figlio XML per accedere a nodi figlio in base al nome, da un oggetto <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument> o da raccolte di oggetti <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument>.  Usare la proprietà `Value` XML per accedere al valore del primo nodo figlio nella raccolta restituita.  Per altre informazioni, vedere [XML Value Property](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
 Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] converte le proprietà axis dell'elemento figlio in chiamate al metodo <xref:System.Xml.Linq.XContainer.Elements%2A>.  
  
## Spazi dei nomi XML  
 Il nome in una proprietà axis dell'elemento figlio può usare solo prefissi degli spazi dei nomi XML dichiarati globalmente con l'istruzione `Imports`.  Non può usare prefissi degli spazi dei nomi XML dichiarati localmente all'interno di valori letterali dell'elemento XML.  Per altre informazioni, vedere [Imports Statement \(XML Namespace\)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
## Esempio  
 L'esempio seguente illustra come accedere ai nodi figlio denominati `phone` dall'oggetto `contact`.  
  
 [!code-vb[VbXMLSamples#17](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_1.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Home Phone = 206-555-0144`  
  
## Esempio  
 L'esempio seguente illustra come accedere ai nodi figlio denominati `phone` dalla raccolta restituita dalla proprietà axis dell'elemento figlio `contact` dell'oggetto `contacts`.  
  
 [!code-vb[VbXMLSamples#18](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_2.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Home Phone = 206-555-0144`  
  
## Esempio  
 Nell'esempio seguente viene dichiarato `ns` come un prefisso dello spazio dei nomi XML.  Il prefisso dello spazio dei nomi viene quindi usato per creare un valore letterale XML e accedere al primo nodo figlio con il nome completo `ns:name`.  
  
 [!code-vb[VbXMLSamples#19](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_3.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Patrick Hines`  
  
## Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)