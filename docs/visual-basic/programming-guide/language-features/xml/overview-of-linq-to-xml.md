---
title: "Overview of LINQ to XML in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "LINQ to XML [Visual Basic], about LINQ to XML"
  - "LINQ [Visual Basic], LINQ to XML"
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Overview of LINQ to XML in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] fornisce supporto per [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] tramite valori letterali XML e proprietà axis XML.  In questo modo, è possibile utilizzare una sintassi comoda e ben conosciuta per l'utilizzo di XML nel codice [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]. I *valori letterali XML* consentono di includere direttamente l'XML nel codice.  Le *proprietà axis XML* consentono di accedere a nodi figlio, a nodi derivati e agli attributi di un valore letterale XML.  Per ulteriori informazioni, vedere [XML Literals Overview](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md) e [Accessing XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md).  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)] è un'API di programmazione XML in memoria progettata appositamente per consentire l'utilizzo di [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext-md.md)].  Sebbene sia possibile chiamare direttamente le API [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)], solo [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consente di dichiarare valori letterali XML e di accedere direttamente alle proprietà axis XML.  
  
> [!NOTE]
>  I valori letterali XML e le proprietà axis XML non sono supportate in codice dichiarativo in una pagina ASP.NET.  Per utilizzare le funzionalità XML di Visual Basic, inserire il codice in una pagina code\-behind nell'applicazione ASP.NET.  
  
 ![Collegamento a video](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") Per dimostrazioni video correlate, vedere [Ricerca per categorie: Introduzione a LINQ to XML](http://go.microsoft.com/fwlink/?LinkId=143034) e [Creazione di fogli di calcolo di Excel tramite LINQ to XML](http://go.microsoft.com/fwlink/?LinkId=143536).  
  
## Creazione XML  
 Le strutture ad albero XML possono essere create in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] in due modi.  È possibile dichiarare un valore letterale XML direttamente nel codice oppure è possibile utilizzare le API [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] per creare la struttura ad albero.  Entrambi i processi consentono al codice di riflettere la struttura finale della struttura ad albero XML.  Nell'esempio di codice riportato di seguito viene creato un elemento XML .  
  
 [!code-vb[VbXmlSamples#5](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_1.vb)]  
  
 Per ulteriori informazioni, vedere [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md).  
  
## Accesso ed esplorazione XML  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] fornisce proprietà axis XML per l'accesso a strutture XML e l'esplorazione di tali strutture.  Queste proprietà consentono di accedere a elementi e attributi XML specificando i nomi dell'elemento figlio XML.  In alternativa, è possibile chiamare in modo esplicito i metodi [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] per esplorare e individuare elementi e attributi.  Nell'esempio di codice riportato di seguito vengono utilizzate le proprietà axis XML per fare riferimento agli attributi e agli elementi figlio di un elemento XML.  Nell'esempio di codice viene utilizzata una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] per recuperare elementi figlio e restituirli come elementi XML, eseguendo in effetti una trasformazione.  
  
 [!code-vb[VbXmlSamples#8](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_2.vb)]  
  
 Per ulteriori informazioni, vedere [Accessing XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md).  
  
## Spazi dei nomi XML  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consente di specificare un alias per uno spazio dei nomi XML globale utilizzando l'istruzione `Imports`.  Nell'esempio riportato di seguito viene illustrato come utilizzare l'istruzione `Imports` per importare uno spazio dei nomi XML.  
  
 [!code-vb[VbXMLSamples#1](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_3.vb)]  
  
 È possibile utilizzare un alias dello spazio dei nomi XML quando si accede alle proprietà axis di XML e si dichiarano valori letterali XML per documenti ed elementi XML.  
  
 È possibile recuperare un oggetto <xref:System.Xml.Linq.XNamespace> per un particolare prefisso dello spazio dei nomi utilizzando [GetXmlNamespace Operator](../../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md).  
  
 Per ulteriori informazioni, vedere [Imports Statement \(XML Namespace\)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
### Utilizzare lo spazio dei nomi XML nei valori letterali XML  
 Nell'esempio riportato di seguito viene illustrato come creare un oggetto <xref:System.Xml.Linq.XElement> che usa lo spazio dei nomi globale `ns`.  
  
 [!code-vb[VbXMLSamples#2](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_4.vb)]  
  
 Il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] converte valori letterali XML che contengono alias dello spazio dei nomi XML in codice equivalente che utilizza la notazione XML per utilizzare gli spazi dei nomi XML, con l'attributo `xmlns`.  Dopo la compilazione, il codice riportato nell'esempio della sezione precedente produce sostanzialmente lo stesso codice eseguibile dell'esempio seguente:  
  
 [!code-vb[VbXMLSamples#3](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_5.vb)]  
  
### Utilizzare gli spazi dei nomi XML in proprietà axis XML.  
 Gli spazi dei nomi XML dichiarati nei valori letterali XML non possono essere utilizzati in proprietà axis XML.  Tuttavia, gli spazi dei nomi globali possono essere utilizzati con le proprietà axis XML.  Utilizzare un segno di due punti per separare il prefisso dello spazio dei nomi XML dal nome dell'elemento locale.  Di seguito è riportato un esempio:  
  
 [!code-vb[VbXMLSamples#4](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/overview-of-linq-to-xml_6.vb)]  
  
## Vedere anche  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Accessing XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [Manipulating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)