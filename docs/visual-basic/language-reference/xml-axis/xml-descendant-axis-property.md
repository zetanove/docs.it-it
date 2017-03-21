---
title: "Proprietà Axis Descendant XML (Visual Basic) | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlPropertyDescendantsAxis
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML descendant axis property [Visual Basic]
- descendant axis property [Visual Baisc]
- XML axis [Visual Basic], descendant
- XML [Visual Basic], accessing
ms.assetid: a178f85b-5d54-438f-8479-40b62af6fe76
caps.latest.revision: 14
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 434dc90c643381bdc27b2da54a7418e39bf15e98
ms.lasthandoff: 03/13/2017

---
# <a name="xml-descendant-axis-property-visual-basic"></a>Proprietà axis descendant XML (Visual Basic)
Fornisce l'accesso ai discendenti di uno dei seguenti: un <xref:System.Xml.Linq.XElement>oggetto, un <xref:System.Xml.Linq.XDocument>oggetto, una raccolta di <xref:System.Xml.Linq.XElement>oggetti o una raccolta di <xref:System.Xml.Linq.XDocument>oggetti.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object...<descendant>  
```  
  
## <a name="parts"></a>Parti  
 `object`  
 Obbligatorio. Un <xref:System.Xml.Linq.XElement>oggetto, un <xref:System.Xml.Linq.XDocument>oggetto, una raccolta di <xref:System.Xml.Linq.XElement>oggetti o una raccolta di <xref:System.Xml.Linq.XDocument>oggetti.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
 ...<  
 Obbligatorio. Indica l'inizio di una proprietà axis descendant.  
  
 `descendant`  
 Obbligatorio. Nome dei nodi discendente per accedere, nel formato [`prefix``:`]`name`.  
  
|Parte|Descrizione|  
|----------|-----------------|  
|`prefix`|Facoltativo. Prefisso dello spazio dei nomi XML per il nodo discendente. Deve essere uno spazio dei nomi XML globale viene definito mediante un `Imports` istruzione.|  
|`name`|Obbligatorio. Nome locale del nodo discendente. Vedere [i nomi di elementi e attributi XML dichiarati](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).|  
  
 \>  
 Obbligatorio. Indica la fine di una proprietà axis descendant.  
  
## <a name="return-value"></a>Valore restituito  
 Una raccolta di <xref:System.Xml.Linq.XElement>oggetti.</xref:System.Xml.Linq.XElement>  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare una proprietà axis descendant XML per accedere a nodi discendenti in base al nome da un <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>oggetto, o da una raccolta di <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>oggetti.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> Utilizzare il codice XML `Value` proprietà per accedere al valore del primo nodo discendente nella raccolta restituita. Per ulteriori informazioni, vedere [proprietà Value XML](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte le proprietà axis descendant in chiamate per il <xref:System.Xml.Linq.XContainer.Descendants%2A>(metodo).</xref:System.Xml.Linq.XContainer.Descendants%2A>  
  
## <a name="xml-namespaces"></a>Spazi dei nomi XML  
 Il nome di una proprietà axis descendant può utilizzare solo spazi dei nomi XML dichiarati globalmente con il `Imports` istruzione. È possibile utilizzare gli spazi dei nomi XML dichiarati localmente all'interno di valori letterali dell'elemento XML. Per ulteriori informazioni, vedere [istruzione Imports (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come accedere al valore del primo nodo discendente denominato `name` e i valori di tutti i nodi discendenti denominati `phone` dal `contacts` oggetto.  
  
 [!code-vb[VbXMLSamples&#25;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-descendant-axis-property_1.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Name: Patrick Hines`  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene dichiarato `ns` come un prefisso dello spazio dei nomi XML. Viene quindi utilizzato il prefisso dello spazio dei nomi per creare valori letterali XML e accedere al valore del primo nodo figlio con il nome completo `ns:name`.  
  
 [!code-vb[&#26; VbXMLSamples](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-descendant-axis-property_2.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Name: Patrick Hines`  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [Proprietà Axis XML](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [Valori letterali XML](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creazione di XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Nomi di elementi e attributi XML dichiarati](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
