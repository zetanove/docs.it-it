---
title: Cenni preliminari sui valori letterali XML (Visual Basic) | Documenti di Microsoft
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
helpviewer_keywords:
- XML literals [Visual Basic], about XML literals
- declaring XML literals [Visual Basic]
- LINQ to XML [Visual Basic], XML literals
- literals [Visual Basic], XML
ms.assetid: 37987c15-4ab8-471b-bd45-399816bfb57f
caps.latest.revision: 27
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
ms.openlocfilehash: 57d036910ba9e49385caca28de222a8a8e28ec56
ms.lasthandoff: 03/13/2017

---
# <a name="xml-literals-overview-visual-basic"></a>Cenni preliminari sui valori letterali XML (Visual Basic)
Un *valore letterale XML* consente di incorporare direttamente XML di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] codice. Sintassi del valore letterale XML rappresenta [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetti ed è simile alla sintassi XML 1.0. Questo rende più facile creare elementi e documenti XML a livello di programmazione perché il codice ha la stessa struttura del XML finale.  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Compila i valori letterali XML in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetti. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]fornisce un modello a oggetti semplice per la creazione e modifica di XML e questo modello si integra bene con [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]. Per ulteriori informazioni, vedere <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>  
  
 È possibile incorporare un [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] espressione in un valore letterale XML. In fase di esecuzione, l'applicazione crea un [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetto per ogni valore letterale, includendo i valori delle espressioni incorporate. Consente di specificare contenuto dinamico all'interno di un valore letterale XML. Per ulteriori informazioni, vedere [espressioni incorporate in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
 Per ulteriori informazioni sulle differenze tra la sintassi del valore letterale XML e la sintassi XML 1.0, vedere [valori letterali XML e specifica XML 1.0](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md).  
  
## <a name="simple-literals"></a>Valori letterali semplici  
 È possibile creare un [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetto di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] codice digitando o incollando XML valido. Restituisce un valore letterale elemento XML un <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement> Per ulteriori informazioni, vedere [letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md) e [valori letterali XML e specifica XML 1.0](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md). Nell'esempio seguente viene creato un elemento XML che contiene diversi elementi figlio.  
  
 [!code-vb[VbXMLSamples n.&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_1.vb)]  
  
 È possibile creare un documento XML iniziando un valore letterale XML con `<?xml version="1.0"?>`, come illustrato nell'esempio seguente. Restituisce un valore letterale documento XML un <xref:System.Xml.Linq.XDocument>oggetto.</xref:System.Xml.Linq.XDocument> Per ulteriori informazioni, vedere [XML Document Literal](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md).  
  
 [!code-vb[6 VbXMLSamples](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_2.vb)]  
  
> [!NOTE]
>  Sintassi del valore letterale XML in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non è identica alla sintassi nella specifica XML 1.0. Per ulteriori informazioni, vedere [valori letterali XML e specifica XML 1.0](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md).  
  
## <a name="line-continuation"></a>Continuazione di riga  
 Un valore letterale XML può occupare più righe senza utilizzare caratteri di continuazione di riga (sequenza spazio-carattere di sottolineatura-invio). Questo rende più facile confrontare i valori letterali XML in codice con documenti XML.  
  
 Il compilatore considera i caratteri di continuazione di riga come parte di un valore letterale XML. Pertanto, è necessario utilizzare la sequenza spazio-carattere di sottolineatura-invio solo quando fa parte di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetto.  
  
 Caratteri di continuazione di riga, tuttavia, è necessaria se si dispone di un'espressione su più righe in un'espressione incorporata. Per ulteriori informazioni, vedere [espressioni incorporate in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
## <a name="embedding-queries-in-xml-literals"></a>Incorporare le query nei valori letterali XML  
 È possibile utilizzare una query in un'espressione incorporata. Quando si esegue questa operazione, gli elementi restituiti dalla query vengono aggiunti all'elemento XML. Ciò consente di aggiungere contenuto dinamico, ad esempio il risultato di query dell'utente, a un valore letterale XML.  
  
 Ad esempio, il codice seguente viene utilizzata una query incorporata per creare elementi XML dai membri di `phoneNumbers2` di matrice e quindi aggiungere tali elementi come elementi figlio di `contact2`.  
  
 [!code-vb[VbXMLSamples&#7;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_3.vb)]  
  
## <a name="how-the-compiler-creates-objects-from-xml-literals"></a>Come il compilatore crea oggetti da valori letterali XML  
 Il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte i valori letterali XML in chiamate equivalente [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] costruttori per creare il [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] oggetto. Ad esempio, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore convertirà il codice seguente in una chiamata al <xref:System.Xml.Linq.XProcessingInstruction>costruttore per l'istruzione in versione XML, le chiamate al <xref:System.Xml.Linq.XElement>costruttore per la `<contact>`, `<name>`, e `<phone>` elementi e le chiamate al <xref:System.Xml.Linq.XAttribute>costruttore per il `type` attributo.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XProcessingInstruction> Fornito in particolare, gli attributi nell'esempio seguente, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore chiamerà il <xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29>costruttore due volte.</xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29> Il primo passerà il valore `type` per il `name` parametro e il valore `home` per il `value` parametro. Il secondo passerà anche il valore `type` per il `name` parametro, ma il valore `work` per il `value` parametro.  
  
 [!code-vb[6 VbXMLSamples](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [Creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Espressioni incorporate in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [Valore letterale documento XML](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [Valore letterale elemento XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Valori letterali XML](../../../../visual-basic/language-reference/xml-literals/index.md)
