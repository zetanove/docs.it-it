---
title: Assi LINQ to XML (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: ecd3bd00-28e5-4517-a59f-53bff39fd478
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4d6466a78c3a8e9d21e30f2d3cf8a49ed89dafbf
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-axes-visual-basic"></a>Assi LINQ to XML (Visual Basic)
Dopo aver creato un albero XML o aver caricato un documento XML in un albero XML, è possibile eseguire query su di essa per cercare elementi e attributi e recuperarne i valori.  
  
 Prima di scrivere eventuali query, è necessario conoscere gli assi [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]. Esistono due tipi di metodi dell'asse: innanzitutto, sono disponibili i metodi vengono chiamati su un unico <xref:System.Xml.Linq.XElement>oggetto <xref:System.Xml.Linq.XDocument>oggetto, o <xref:System.Xml.Linq.XNode>oggetto.</xref:System.Xml.Linq.XNode> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> Questi metodi operano su un singolo oggetto e restituiscono una raccolta di <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XAttribute>, o <xref:System.Xml.Linq.XNode>oggetti.</xref:System.Xml.Linq.XNode> </xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> Il secondo tipo include i metodi di estensione che operano su raccolte e restituiscono raccolte. I metodi di estensione enumerano la raccolta di origine, chiamano il metodo dell'asse appropriato su ogni elemento della raccolta e concatenano i risultati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[LINQ to panoramica degli assi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes-overview.md)|Viene fornita una definizione degli assi e ne viene illustrato l'uso nel contesto di query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].|  
|[Procedura: recuperare una raccolta di elementi (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-elements-linq-to-xml.md)|Introduce il <xref:System.Xml.Linq.XContainer.Elements%2A>(metodo).</xref:System.Xml.Linq.XContainer.Elements%2A> che consente di recuperare una raccolta degli elementi figlio di un elemento.|  
|[Procedura: recuperare il valore di un elemento (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md)|Viene spiegato come ottenere i valori di elementi.|  
|[Procedura: filtrare i nomi degli elementi (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-filter-on-element-names-linq-to-xml.md)|Viene illustrato come filtrare in base a nomi di elemento quando si usano gli assi.|  
|[Procedura: concatenare chiamate al metodo Axis (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-chain-axis-method-calls-linq-to-xml.md)|Viene illustrato come concatenare chiamate ai metodi degli assi.|  
|[Procedura: recuperare un singolo elemento figlio (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md)|Viene illustrato come recuperare un singolo elemento figlio di un elemento, dato il relativo nome di tag.|  
|[Procedura: recuperare una raccolta di attributi (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-attributes-linq-to-xml.md)|Introduce il <xref:System.Xml.Linq.XElement.Attributes%2A>(metodo).</xref:System.Xml.Linq.XElement.Attributes%2A> che consente di recuperare gli attributi di un elemento.|  
|[Procedura: recuperare un singolo attributo (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-attribute-linq-to-xml.md)|Viene illustrato come recuperare un singolo attributo di un elemento, dato il relativo nome.|  
|[Procedura: recuperare il valore di un attributo (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-attribute-linq-to-xml.md)|Viene spiegato come ottenere i valori di attributi.|  
|[Procedura: recuperare il valore superficiale di un elemento (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-shallow-value-of-an-element.md)|Viene illustrato come recuperare il valore superficiale di un elemento|  
|[Assi integrati nel linguaggio in Visual Basic (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/language-integrated-axes.md)|Vengono riepilogate le [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] assi integrati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
