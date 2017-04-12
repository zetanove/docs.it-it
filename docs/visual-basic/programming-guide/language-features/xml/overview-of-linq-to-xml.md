---
title: Panoramica di LINQ to XML in Visual Basic | Documenti di Microsoft
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
- LINQ to XML [Visual Basic], about LINQ to XML
- LINQ [Visual Basic], LINQ to XML
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
caps.latest.revision: 17
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
ms.openlocfilehash: 508d4a97b0636f10607326eb35c4c5d8c7860873
ms.lasthandoff: 03/13/2017

---
# <a name="overview-of-linq-to-xml-in-visual-basic"></a>Cenni preliminari su LINQ to XML in Visual Basic
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce il supporto per [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] tramite valori letterali XML e le proprietà axis XML. In questo modo è possibile utilizzare una sintassi pratica e familiare per l'utilizzo di XML nel [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] codice. *Valori letterali XML* consentono di includere dati XML direttamente nel codice. *Proprietà axis XML* consentono di accedere a nodi figlio, i relativi nodi discendenti e gli attributi di un valore letterale XML. Per ulteriori informazioni, vedere [Cenni preliminari sui valori letterali XML](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md) e [l'accesso a XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md).  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]è progettato specificamente per sfruttare i vantaggi di API di programmazione XML in memoria [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]. Sebbene sia possibile chiamare il [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] direttamente le API solo [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente di dichiarare valori letterali XML e accedere direttamente le proprietà axis XML.  
  
> [!NOTE]
>  Valori letterali XML e le proprietà axis XML non sono supportate nel codice dichiarativo in una pagina ASP.NET. Per utilizzare le funzionalità XML di Visual Basic, inserire il codice in una pagina code-behind nell'applicazione ASP.NET.  
  
 ![collegamento a video](../../../../visual-basic/programming-guide/language-features/xml/media/playvideo.gif "PlayVideo") per dimostrazioni video correlate, vedere [How Do prendetevi con LINQ to XML?](http://go.microsoft.com/fwlink/?LinkId=143034) e [come posso creare fogli di calcolo Excel con LINQ to XML?](http://go.microsoft.com/fwlink/?LinkId=143536).  
  
## <a name="creating-xml"></a>Creazione di XML  
 Esistono due modi per creare strutture ad albero XML in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. È possibile dichiarare un XML letterale direttamente nel codice oppure è possibile utilizzare il [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] API per creare la struttura ad albero. Entrambi i processi consentono al codice in modo da riflettere la struttura finale della struttura ad albero XML. Ad esempio, il codice seguente crea un elemento XML:  
  
 [!code-vb[VbXmlSamples n.&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_1.vb)]  
  
 Per ulteriori informazioni, vedere [la creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md).  
  
## <a name="accessing-and-navigating-xml"></a>Accesso e l'esplorazione XML  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce le proprietà axis XML per l'accesso e l'esplorazione di strutture XML. Queste proprietà consentono di accedere a elementi e attributi XML specificando i nomi degli elementi figlio XML. In alternativa, è possibile chiamare in modo esplicito il [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] metodi per esplorare e individuare elementi e attributi. Ad esempio, il codice seguente utilizza le proprietà axis XML per fare riferimento agli attributi e gli elementi figlio di un elemento XML. Nell'esempio di codice viene utilizzato un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query per recuperare gli elementi figlio e restituirli come elementi XML, in modo efficace eseguendo una trasformazione.  
  
 [!code-vb[VbXmlSamples n.&8;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_2.vb)]  
  
 Per ulteriori informazioni, vedere [l'accesso a XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md).  
  
## <a name="xml-namespaces"></a>Spazi dei nomi XML  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Consente di specificare un alias per uno spazio dei nomi XML globale utilizzando il `Imports` istruzione. Nell'esempio seguente viene illustrato come utilizzare il `Imports` per importare uno spazio dei nomi XML:  
  
 [!code-vb[VbXMLSamples n.&1;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_3.vb)]  
  
 Quando si accede alle proprietà axis XML e dichiarano i valori letterali XML per elementi e documenti XML, è possibile utilizzare un alias dello spazio dei nomi XML.  
  
 È possibile recuperare un <xref:System.Xml.Linq.XNamespace>oggetto per un prefisso dello spazio dei nomi specifico utilizzando il [operatore GetXmlNamespace](../../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md).</xref:System.Xml.Linq.XNamespace>  
  
 Per ulteriori informazioni, vedere [istruzione Imports (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
### <a name="using-xml-namespaces-in-xml-literals"></a>Utilizzo di spazi dei nomi XML in valori letterali XML  
 Nell'esempio seguente viene illustrato come creare un <xref:System.Xml.Linq.XElement>oggetto che utilizza lo spazio dei nomi globale `ns`:</xref:System.Xml.Linq.XElement>  
  
 [!code-vb[VbXMLSamples n.&2;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_4.vb)]  
  
 Il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore converte i valori letterali XML che contengono alias dello spazio dei nomi XML in codice equivalente che utilizza la notazione XML per l'utilizzo di spazi dei nomi XML, con la `xmlns` attributo. Quando viene compilato, il codice di esempio della sezione precedente produce essenzialmente lo stesso codice eseguibile dell'esempio seguente:  
  
 [!code-vb[VbXMLSamples n.&3;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_5.vb)]  
  
### <a name="using-xml-namespaces-in-xml-axis-properties"></a>Utilizzo di spazi dei nomi XML in proprietà Axis XML  
 Spazi dei nomi XML dichiarati in valori letterali XML non sono disponibili per l'utilizzo in proprietà axis XML. Tuttavia, è possibile utilizzare gli spazi dei nomi globale con le proprietà axis XML. Utilizzare un virgola per separare il prefisso dello spazio dei nomi XML dal nome dell'elemento locale. Di seguito è riportato un esempio:  
  
 [!code-vb[VbXMLSamples n.&4;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_6.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [Creazione di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Accesso a XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [Modifica di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)
