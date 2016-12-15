---
title: "XML Value Property (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyExtensionValue"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Value property [Visual Basic]"
  - "Visual Basic code, accessing XML"
  - "XML axis [Visual Basic], Value"
  - "XML Value property [Visual Basic]"
ms.assetid: 7ddd057a-a195-4e9b-ad8b-2ee0e615a20f
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML Value Property (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di accedere al valore del primo elemento di una raccolta di oggetti <xref:System.Xml.Linq.XElement>.  
  
## Sintassi  
  
```  
  
object.Value  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`object`|Obbligatorio.  Raccolta di oggetti <xref:System.Xml.Linq.XElement>.|  
  
## Valore restituito  
 Oggetto `String` che contiene il valore del primo elemento della raccolta, o `Nothing` se la raccolta è vuota.  
  
## Note  
 La proprietà <xref:System.Xml.Linq.XElement.Value%2A> semplifica l'accesso al valore del primo elemento in una raccolta di oggetti <xref:System.Xml.Linq.XElement>.  Questa proprietà dapprima controlla se la raccolta contiene almeno un oggetto.  Se la raccolta è vuota, questa proprietà restituisce `Nothing`.  In caso contrario la proprietà restituisce il valore della proprietà <xref:System.Xml.Linq.XElement.Value%2A> del primo elemento della raccolta.  
  
> [!NOTE]
>  Quando si accede al valore di un attributo XML utilizzando l'identificatore '@', il valore dell'attributo viene restituito come un oggetto `String` e non è necessario specificare in modo esplicito la proprietà <xref:System.Xml.Linq.XAttribute.Value%2A>.  
  
 Per accedere agli altri elementi in una raccolta è possibile utilizzare la proprietà dell'indicizzatore di estensione XML.  Per ulteriori informazioni, vedere [Extension Indexer Property](../../../visual-basic/language-reference/xml-axis/extension-indexer-property.md).  
  
## Ereditarietà  
 La maggior parte degli utenti non dovranno implementare <xref:System.Collections.Generic.IEnumerable%601>e possono pertanto ignorare questa sezione.  
  
 La proprietà <xref:System.Xml.Linq.XElement.Value%2A> è una proprietà di estensione per i tipi che implementano `IEnumerable(Of XElement)`.  L'associazione di questa proprietà di estensione è simile all'associazione di metodi di estensione: se un tipo implementa una delle interfacce e definisce una proprietà che ha il nome "Valore", tale proprietà ha precedenza sulla proprietà di estensione.  In altre parole, si può eseguire l'override di questa proprietà <xref:System.Xml.Linq.XElement.Value%2A> definendo una nuova proprietà in una classe che implementa `IEnumerable(Of XElement)`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare la proprietà <xref:System.Xml.Linq.XElement.Value%2A> per accedere al primo nodo di una raccolta di oggetti <xref:System.Xml.Linq.XElement>.  Nell'esempio viene utilizzata la proprietà axis figlio per ottenere la raccolta di tutti i nodi figlio denominati `phone` inclusi nell'oggetto `contact`.  
  
 [!code-vb[VbXMLSamples#15](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-value-property_1.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `Phone number: 206-555-0144`  
  
## Esempio  
 Nell'esempio seguente viene illustrato come ottenere il valore di un attributo XML da una raccolta di oggetti <xref:System.Xml.Linq.XAttribute>.  In questo esempio viene utilizzato l'attributo della proprietà axis per visualizzare il valore dell'attributo `type` per tutti gli elementi di `phone`.  
  
 [!code-vb[VbXMLSamples#16](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-value-property_2.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `home`  
  
 `work`  
  
## Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 <xref:System.Collections.Generic.IEnumerable%601>   
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML Literals](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creating XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Metodi di estensione](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Extension Indexer Property](../../../visual-basic/language-reference/xml-axis/extension-indexer-property.md)   
 [XML Child Axis Property](../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)   
 [XML Attribute Axis Property](../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)