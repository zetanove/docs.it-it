---
title: "XML Attribute Axis Property (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyAttributeAxis"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "attribute axis property [Visual Basic]"
  - "Visual Basic code, accessing XML"
  - "XML attribute axis property [Visual Basic]"
  - "XML axis [Visual Basic], attribute"
  - "XML [Visual Basic], accessing"
ms.assetid: 7a4777e1-0618-4de9-9510-fb9ace2bf4db
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# XML Attribute Axis Property (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Fornisce accesso al valore di un attributo per un oggetto <xref:System.Xml.Linq.XElement> o al primo elemento in una raccolta di oggetti <xref:System.Xml.Linq.XElement>.  
  
## Sintassi  
  
```  
  
      object.@attribute  
-or-  
object.@<attribute>  
```  
  
## Parti  
 `object`  
 Obbligatorio.  Un oggetto <xref:System.Xml.Linq.XElement> o una raccolta di oggetti <xref:System.Xml.Linq.XElement>.  
  
 .@  
 Obbligatorio.  Indica l'inizio di una proprietà axis attributo.  
  
 \<  
 Parametro facoltativo.  Indica l'inizio del nome dell'attributo quando `attribute` non è un identificatore valido in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 `attribute`  
 Obbligatorio.  Nome dell'attributo a cui accedere, nel formato \[`prefix`\]`name`.  
  
|Parte|Descrizione|  
|-----------|-----------------|  
|`prefix`|Parametro facoltativo.  Prefisso dello spazio dei nomi XML per l'attributo.  Deve essere uno spazio dei nomi XML globale definito utilizzando un'istruzione `Imports`.|  
|`name`|Obbligatorio.  Nome di attributo locale  Vedere [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).|  
  
 \>  
 Parametro facoltativo.  Indica la fine del nome di attributo quando `attribute` non è un identificatore valido in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
## Valore restituito  
 Stringa contenente il valore di `attribute`.  Se il nome dell'attributo non esiste, viene restituito `Nothing`.  
  
## Note  
 È possibile utilizzare una proprietà axis di un attributo XML per accedere al valore di un attributo in base al nome da un oggetto <xref:System.Xml.Linq.XElement> o dal primo elemento in una raccolta di oggetti <xref:System.Xml.Linq.XElement>.  È possibile recuperare un valore dell'attributo in base al nome o aggiungere un nuovo attributo a un elemento specificando un nuovo nome preceduto dall'identificatore @.  
  
 Quando viene fatto riferimento a un attributo XML utilizzando l'identificatore @, il valore dell'attributo viene restituito come una stringa e non è necessario specificare in modo esplicito la proprietà <xref:System.Xml.Linq.XAttribute.Value%2A>.  
  
 Le regole di denominazione per gli attributi XML differiscono dalle regole di denominazione per gli identificatori di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]. Per accedere a un attributo XML con un nome che non è un identificatore di Visual Basic valido, racchiudere il nome tra parentesi acute \(\< e \>\).  
  
## Spazi dei nomi XML  
 Il nome in una proprietà axis attributo può utilizzare solo prefisso degli spazi dei nomi XML dichiarati globalmente con l'istruzione `Imports`.  Non può utilizzare prefissi degli spazi dei nomi XML dichiarati localmente all'interno di valori letterali dell'elemento XML.  Per ulteriori informazioni, vedere [Imports Statement \(XML Namespace\)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
## Esempio  
 Nell'esempio seguente viene mostrato come ottenere i valori degli attributi XML denominati `type` da una raccolta di elementi XML denominati `phone`.  
  
 [!code-vb[VbXMLSamples#12](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-attribute-axis-prope_1.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `<phoneTypes>`  
  
 `<type>home</type>`  
  
 `<type>work</type>`  
  
 `</phoneTypes>`  
  
## Esempio  
 Nell'esempio seguente viene illustrato come creare attributi per un elemento XML, sia in modo dichiarativo come parte dell'XML che dinamicamente aggiungendo un attributo a un'istanza di un oggetto <xref:System.Xml.Linq.XElement>.  L'attributo di `type` viene creato in modo dichiarativo e l'attributo `owne` viene creato dinamicamente.  
  
 [!code-vb[VbXMLSamples#44](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-attribute-axis-prope_2.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
```  
<phone type="home" owner="Harris, Phyllis">206-555-0144</phone>  
```  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la sintassi della parentesi angolari per ottenere il valore dell'attributo XML denominato `number-type`, che non è un identificatore valido in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 [!code-vb[VbXMLSamples#13](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-attribute-axis-prope_3.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `Phone type: work`  
  
## Esempio  
 Nell'esempio riportato di seguito viene dichiarato `ns` come un prefisso dello spazio dei nomi XML.  Viene quindi utilizzato il prefisso dello spazio dei nomi per creare un valore letterale XML e accedere al primo nodo figlio con il nome completo "`ns:name`".  
  
 [!code-vb[VbXMLSamples#14](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xml-attribute-axis-prope_4.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `Phone type: home`  
  
## Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)