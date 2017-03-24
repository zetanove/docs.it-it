---
title: "Proprietà dell&quot;indicizzatore di estensione (Visual Basic) | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlPropertyExtensionIndexer
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML extension indexer [Visual Basic]
- extension indexer [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: a16a4b13-54be-432c-82b3-a87091464ada
caps.latest.revision: 22
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
ms.openlocfilehash: 25f434a5b5f8caf013ad5f778897e4e98e3d825d
ms.lasthandoff: 03/13/2017

---
# <a name="extension-indexer-property-visual-basic"></a>Proprietà dell'indicizzatore di estensione (Visual Basic)
Fornisce l'accesso ai singoli elementi di una raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object(index)  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`object`|Obbligatorio. Raccolta queryable. Vale a dire, una raccolta che implementa <xref:System.Collections.Generic.IEnumerable%601>o <xref:System.Linq.IQueryable%601>.</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601>|  
|(|Obbligatorio. Indica l'inizio della proprietà dell'indicizzatore.|  
|`index`|Obbligatorio. Espressione integer che specifica la posizione in base zero di un elemento della raccolta.|  
|)|Obbligatorio. Indica la fine della proprietà dell'indicizzatore.|  
  
## <a name="return-value"></a>Valore restituito  
 L'oggetto dal percorso specificato nella raccolta, o `Nothing` se l'indice è compreso nell'intervallo.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare la proprietà dell'indicizzatore di estensione per accedere ai singoli elementi in una raccolta. Questa proprietà dell'indicizzatore è in genere utilizzata nell'output di proprietà axis XML. L'elemento figlio XML e proprietà axis descendant XML restituiscono raccolte di <xref:System.Xml.Linq.XElement>oggetti o un valore di attributo.</xref:System.Xml.Linq.XElement>  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte le proprietà dell'indicizzatore di estensione per le chiamate al`ElementAtOrDefault` metodo. A differenza di un indicizzatore di matrice, il`ElementAtOrDefault` restituisce `Nothing` se l'indice è compreso nell'intervallo. Questo comportamento risulta utile quando non è facile determinare il numero di elementi in una raccolta.  
  
 Questa proprietà dell'indicizzatore è simile a una proprietà di estensione per le raccolte che implementano <xref:System.Collections.Generic.IEnumerable%601>o <xref:System.Linq.IQueryable%601>: viene utilizzata solo se la raccolta non dispone di un indicizzatore o una proprietà predefinita.</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601>  
  
 Per accedere al valore del primo elemento in una raccolta di <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XAttribute>oggetti, è possibile utilizzare il codice XML `Value` proprietà.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> Per ulteriori informazioni, vedere [proprietà Value XML](../../../visual-basic/language-reference/xml-axis/xml-value-property.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare l'indicizzatore di estensione per accedere al secondo nodo figlio in una raccolta di <xref:System.Xml.Linq.XElement>oggetti.</xref:System.Xml.Linq.XElement> La raccolta è accessibile tramite la proprietà di asse figlio, che ottiene tutti gli elementi figlio denominati `phone` nel `contact` oggetto.  
  
 [!code-vb[VbXMLSamples&#24;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/extension-indexer-property_1.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Second phone number: 425-555-0145`  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [Proprietà Axis XML](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [Valori letterali XML](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creazione di XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Proprietà Value XML](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)
