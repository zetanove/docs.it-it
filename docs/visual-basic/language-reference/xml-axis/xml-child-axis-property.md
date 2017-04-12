---
title: "Proprietà di asse figlio XML (Visual Basic) | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlPropertyChildAxis
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML axis [Visual Basic], child
- child axis property [Visual Basic]
- XML child axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: 89a59d00-985e-4f5c-b59f-29b47bad11cb
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 97b92f9e94ad709c4d8ce944577eb23edc84b328
ms.lasthandoff: 03/13/2017

---
# <a name="xml-child-axis-property-visual-basic"></a>Proprietà Child Axis XML (Visual Basic)
Fornisce l'accesso agli elementi figlio di uno dei seguenti: un <xref:System.Xml.Linq.XElement>oggetto, un <xref:System.Xml.Linq.XDocument>oggetto, una raccolta di <xref:System.Xml.Linq.XElement>oggetti o una raccolta di <xref:System.Xml.Linq.XDocument>oggetti.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.<child>  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`object`|Obbligatorio. Un <xref:System.Xml.Linq.XElement>oggetto, un <xref:System.Xml.Linq.XDocument>oggetto, una raccolta di <xref:System.Xml.Linq.XElement>oggetti o una raccolta di <xref:System.Xml.Linq.XDocument>oggetti.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>|  
|.<|Obbligatorio. Indica l'inizio di una proprietà axis dell'elemento figlio.|  
|`child`|Obbligatorio. Nome dei nodi figlio a cui accedere, nel formato [`prefix``:`]`name`.<br /><br /> -   `Prefix`-Facoltativo. Prefisso dello spazio dei nomi XML per il nodo figlio. Deve essere uno spazio dei nomi XML globale definito usando un'istruzione `Imports`.<br />-   `Name`-Obbligatorio. Nome del nodo figlio locale. Vedere [i nomi di elementi e attributi XML dichiarati](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).|  
|>|Obbligatorio. Indica la fine di una proprietà axis dell'elemento figlio.|  
  
## <a name="return-value"></a>Valore restituito  
 Una raccolta di <xref:System.Xml.Linq.XElement>oggetti.</xref:System.Xml.Linq.XElement>  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare una proprietà child axis XML per accedere a nodi figlio in base al nome da un <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>oggetto, o da una raccolta di <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>oggetti.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> Usare la proprietà `Value` XML per accedere al valore del primo nodo figlio nella raccolta restituita. Per ulteriori informazioni, vedere [proprietà Value XML](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte le proprietà axis figlio per le chiamate al <xref:System.Xml.Linq.XContainer.Elements%2A>(metodo).</xref:System.Xml.Linq.XContainer.Elements%2A>  
  
## <a name="xml-namespaces"></a>Spazi dei nomi XML  
 Il nome in una proprietà axis dell'elemento figlio può usare solo prefissi degli spazi dei nomi XML dichiarati globalmente con l'istruzione `Imports`. Non può usare prefissi degli spazi dei nomi XML dichiarati localmente all'interno di valori letterali dell'elemento XML. Per ulteriori informazioni, vedere [istruzione Imports (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come accedere ai nodi figlio denominati `phone` dall'oggetto `contact`.  
  
 [!code-vb[VbXMLSamples n.&17;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_1.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come accedere ai nodi figlio denominati `phone` dalla raccolta restituita dalla proprietà axis dell'elemento figlio `contact` dell'oggetto `contacts`.  
  
 [!code-vb[VbXMLSamples&#18;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_2.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene dichiarato `ns` come un prefisso dello spazio dei nomi XML. Il prefisso dello spazio dei nomi viene quindi usato per creare un valore letterale XML e accedere al primo nodo figlio con il nome completo `ns:name`.  
  
 [!code-vb[&#19; VbXMLSamples](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-child-axis-property_3.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Patrick Hines`  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [Proprietà Axis XML](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [Valori letterali XML](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creazione di XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Nomi di elementi e attributi XML dichiarati](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
