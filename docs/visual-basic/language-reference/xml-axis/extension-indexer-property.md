---
title: "Extension Indexer Property (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyExtensionIndexer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, accessing XML"
  - "XML extension indexer [Visual Basic]"
  - "extension indexer [Visual Basic]"
  - "XML [Visual Basic], accessing"
ms.assetid: a16a4b13-54be-432c-82b3-a87091464ada
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Extension Indexer Property (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Fornisce accesso ai singoli elementi di una raccolta.  
  
## Sintassi  
  
```  
  
object(index)  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`object`|Obbligatorio.  Raccolta queryable.  Ovvero, una raccolta che implementa un oggetto <xref:System.Collections.Generic.IEnumerable%601> o un oggetto <xref:System.Linq.IQueryable%601>.|  
|\(|Obbligatorio.  Indica l'inizio della proprietà dell'indicizzatore.|  
|`index`|Obbligatorio.  Una espressione integrale che specifica la posizione in base zero di un elemento della raccolta.|  
|\)|Obbligatorio.  Indica la fine della proprietà dell'indicizzatore.|  
  
## Valore restituito  
 L'oggetto dal percorso specificato nella raccolta, o `Nothing` se l'indice è esterno all'intervallo.  
  
## Note  
 È possibile utilizzare la proprietà dell'indicizzatore di estensione per accedere ai singoli elementi in una raccolta.  Questa proprietà dell'indicizzatore viene utilizzata in genere sull'output delle proprietà axis XML.  L'elemento figlio XML e la proprietà axis descendant XML restituiscono raccolte di oggetti <xref:System.Xml.Linq.XElement> o un valore dell'attributo.  
  
 Tramite il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] le proprietà dell'indicizzatore di estensione vengono convertite in chiamate al metodo`ElementAtOrDefault`. A differenza dell'indicizzatore di matrice, se l'indice è esterno all'intervallo, tramite il metodo `ElementAtOrDefault` viene restituito `Nothing`.  Questo comportamento si rivela utile quando non è possibile determinare facilmente il numero di elementi in una raccolta.  
  
 Questa proprietà dell'indicizzatore è simile a una proprietà di estensione per raccolte che implementa <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>: viene utilizzata solo se la raccolta non ha un indicizzatore o una proprietà predefinita.  
  
 Per accedere al valore del primo elemento di una raccolta di oggetti <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XAttribute>, è possibile utilizzare la proprietà `Value` XML.  Per ulteriori informazioni, vedere [XML Value Property](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'indicizzatore di estensione per accedere al secondo nodo figlio di una raccolta di oggetti <xref:System.Xml.Linq.XElement>.  È possibile accedere alla raccolta utilizzando la proprietà axis dell'elemento figlio che ottiene tutti gli elementi figlio denominati `phone` nell'oggetto `contact`.  
  
 [!code-vb[VbXMLSamples#24](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/extension-indexer-property_1.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `Second phone number: 425-555-0145`  
  
## Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML Value Property](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)