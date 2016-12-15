---
title: "XML Literals Overview (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML literals [Visual Basic], about XML literals"
  - "declaring XML literals [Visual Basic]"
  - "LINQ to XML [Visual Basic], XML literals"
  - "literals [Visual Basic], XML"
ms.assetid: 37987c15-4ab8-471b-bd45-399816bfb57f
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML Literals Overview (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Un *valore letterale XML* consente di incorporare direttamente XML nel codice [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. La sintassi del valore letterale XML rappresenta gli oggetti [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] ed è simile alla sintassi XML 1.0. In questo modo viene semplificata la creazione a livello di codice di elementi e documenti XML perché il codice ha la stessa struttura dell'XML finale.  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compila valori letterali XML in oggetti [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] fornisce un semplice modello a oggetti per creare e modificare l'XML e questo modello si integra bene con [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)].  Per ulteriori informazioni, vedere <xref:System.Xml.Linq.XElement>.  
  
 È possibile incorporare un'espressione [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] in un valore letterale XML.  In fase di esecuzione, l'applicazione crea un oggetto [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] per ogni valore letterale, includendo i valori delle espressioni incorporate.  Questo consente di specificare contenuto dinamico in un valore letterale XML.  Per ulteriori informazioni, vedere [Embedded Expressions in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
 Per ulteriori informazioni sulle differenze tra la sintassi dei valori letterali XML e la sintassi XML 1.0, vedere [XML Literals and the XML 1.0 Specification](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md).  
  
## Valori letterali semplici  
 È possibile creare un oggetto [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] nel codice di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] digitando o incollando XML valido.  Un valore letterale di un elemento XML restituisce un oggetto <xref:System.Xml.Linq.XElement>.  Per ulteriori informazioni, vedere [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md) e [XML Literals and the XML 1.0 Specification](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md).  Nell'esempio riportato di seguito viene creato un elemento XML con vari elementi figlio.  
  
 [!code-vb[VbXMLSamples#5](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_1.vb)]  
  
 È possibile creare un documento XML iniziando un valore letterale XML con `<?xml version="1.0"?>`, come illustrato nell'esempio seguente.  Un valore letterale del documento XML restituisce un oggetto <xref:System.Xml.Linq.XDocument>.  Per ulteriori informazioni, vedere [XML Document Literal](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md).  
  
 [!code-vb[VbXMLSamples#6](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_2.vb)]  
  
> [!NOTE]
>  La sintassi del valore letterale XML in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non è identica alla sintassi della specifica XML 1.0.  Per ulteriori informazioni, vedere [XML Literals and the XML 1.0 Specification](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-and-the-xml-1-0-specification.md).  
  
## Continuazione di riga  
 Un valore letterale XML può occupare più righe senza utilizzare caratteri di continuazione di riga.\(la sequenza di tasti spazio\-carattere di sottolineatura\-invio\).  Questo semplifica il confronto tra i valori letterali XML nel codice e i documenti XML.  
  
 Il compilatore tratta i di caratteri di continuazione di riga come parte di un valore letterale XML.  Pertanto, è necessario utilizzare la sequenza spazio\-carattere di sottolineatura\-invio solo quando questa fa parte dell'oggetto [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
 Tuttavia, i caratteri di continuazione di riga sono necessari se si crea un'espressione su più righe in un'espressione incorporata.  Per ulteriori informazioni, vedere [Embedded Expressions in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
## Incorporare Query nei valori letterali XML  
 È possibile utilizzare una query in un'espressione incorporata.  In questo caso, gli elementi restituiti dalla query vengono aggiunti all'elemento XML.  In tal modo è possibile aggiungere contenuto dinamico, ad esempio il risultato di una query di un utente, a un valore letterale XML.  
  
 Ad esempio, nel codice seguente viene utilizzata una query incorporata per creare elementi XML dai membri della matrice `phoneNumbers2` e quindi aggiungere tali elementi come elementi figli di `contact2`.  
  
 [!code-vb[VbXMLSamples#7](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_3.vb)]  
  
## Come il compilatore crea oggetti dai valori letterali XML  
 Il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] traduce i valori letterali XML in chiamate ai costruttori [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] equivalenti per compilare l'oggetto [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  Ad esempio, il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tradurrà l'esempio di codice seguente in una chiamata al costruttore <xref:System.Xml.Linq.XProcessingInstruction> per l'istruzione in versione XML, effettua la chiamata al costruttore <xref:System.Xml.Linq.XElement> per gli elementi `<contact>`, `<name>` e `<phone>` e la chiamata al costruttore <xref:System.Xml.Linq.XAttribute> per l'attributo `type`.  In particolare, in base agli attributi dell'esempio seguente, il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] chiamerà due volte il costruttore <xref:System.Xml.Linq.XAttribute.%23ctor%28System.Xml.Linq.XName%2CSystem.Object%29>.  Il primo passerà il valore `type` per il parametro `name` e il valore `home` per il parametro `value`.  Il secondo passerà ancora il valore `type` per il parametro `name` ma il valore `work` per il parametro `value`.  
  
 [!code-vb[VbXMLSamples#6](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-literals-overview_2.vb)]  
  
## Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Embedded Expressions in XML](../../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [XML Document Literal](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML Literals](../../../../visual-basic/language-reference/xml-literals/index.md)