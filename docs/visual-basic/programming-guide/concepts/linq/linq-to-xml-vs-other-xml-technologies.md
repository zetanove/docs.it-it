---
title: LINQ to XML e Altri Technologies2 XML | Documenti di Microsoft
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
ms.assetid: 72ce3a82-ffc6-488c-98e7-b9b40f3591ec
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0254788fb9efa018e735a57990144c6b176d30d6
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-vs-other-xml-technologies"></a>LINQ to XML e altre tecnologie XML
Questo argomento vengono confrontate [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] per le seguenti tecnologie XML: <xref:System.Xml.XmlReader>, XSLT, MSXML e XmlLite.</xref:System.Xml.XmlReader> Queste informazioni possono risultare utili per decidere quale tecnologia usare.  
  
 Per un confronto tra [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] per il modello (DOM), vedere [LINQ to XML e. DOM (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-vs-dom.md).  
  
## <a name="linq-to-xml-vs-xmlreader"></a>LINQ to XML e XmlReader  
 <xref:System.Xml.XmlReader>è un parser rapido, forward-only e non supporta la memorizzazione nella cache.</xref:System.Xml.XmlReader>  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]viene implementato in cima <xref:System.Xml.XmlReader>, e sono strettamente integrate.</xref:System.Xml.XmlReader> Tuttavia, è inoltre possibile utilizzare <xref:System.Xml.XmlReader>da solo.</xref:System.Xml.XmlReader>  
  
 Si supponga ad esempio di compilare un servizio Web per l'analisi di centinaia di documenti XML al secondo e che i documenti abbiano la stessa struttura, per cui è necessario scrivere un'unica implementazione del codice di analisi. In questo caso, è preferibile utilizzare <xref:System.Xml.XmlReader>da solo.</xref:System.Xml.XmlReader>  
  
 Al contrario, se si sta creando un sistema che analizza i vari documenti XML più piccoli, diversi uno da altro, si desidera sfruttare i miglioramenti di produttività che [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] fornisce.  
  
## <a name="linq-to-xml-vs-xslt"></a>LINQ to XML e XSLT  
 Entrambi [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] e XSLT sono disponibili funzionalità complete di trasformazione di documenti XML. XSLT è un approccio dichiarativo, basato su regole. I programmatori XSLT avanzati scrivono codice XSLT in uno stile di programmazione funzionale che enfatizza un approccio senza stato. Le trasformazioni possono essere scritte con funzioni pure implementate senza effetti collaterali. Questo approccio basato su regole o funzionale non è noto a tutti gli sviluppatori e può risultare un processo lungo e difficile da apprendere.  
  
 XSLT può essere un sistema molto produttivo che consente di generare applicazioni a elevate prestazioni. Alcune grandi società Web, ad esempio, usano XSLT per generare HTML dall'XML recuperato da un'ampia varietà di archivi dati. Il motore XSLT gestito compila XSLT in codice CLR e in alcuni scenari offre prestazioni ancora più elevate rispetto al motore XSLT nativo.  
  
 Tuttavia, XSLT non consente di sfruttare le conoscenze di C# e Visual Basic di cui dispongono molti sviluppatori. Richiede la scrittura di codice in un linguaggio di programmazione diverso e complesso. Con l'uso di due sistemi di sviluppo non integrati, quali C# (o Visual Basic) e XSLT, i sistemi software risultanti sono più difficili da sviluppare e mantenere.  
  
 Dopo avere assimilato [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] , espressioni di query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] trasformazioni sono una tecnologia potente che è facile da utilizzare. In pratica, il documento XML utilizzando la costruzione funzionale, recuperando i dati da diverse origini, costruendo <xref:System.Xml.Linq.XElement>gli oggetti in modo dinamico e assemblando l'insieme in un nuovo albero XML.</xref:System.Xml.Linq.XElement> La trasformazione può generare un documento completamente nuovo. Costruzione di trasformazioni in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è relativamente semplice e intuitivo e il codice risultante è leggibile. con una conseguente riduzione dei costi di sviluppo e manutenzione.  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] non è progettato per sostituire XSLT, che rimane lo strumento ideale per trasformazioni XML complicate e basate su documenti, soprattutto se la struttura del documento non è ben definita.  
  
 XSLT presenta il vantaggio di essere uno standard W3C (World Wide Web Consortium). Se è necessario rispettare il requisito di usare solo tecnologie che corrispondono a standard, XSLT può rivelarsi la soluzione più appropriata.  
  
 XSLT equivale a XML, pertanto può essere modificato a livello di codice.  
  
## <a name="linq-to-xml-vs-msxml"></a>LINQ to XML e MSXML  
 MSXML è la tecnologia basata su COM per l'elaborazione di codice XML inclusa in Microsoft Windows. Fornisce un'implementazione nativa di DOM (Document Object Model) con supporto per XPath e XSLT. Contiene inoltre il parser SAX2 basato su eventi che non supporta la memorizzazione nella cache.  
  
 MSXML offre prestazioni soddisfacenti, è sicuro per impostazione predefinita nella maggior parte degli scenari ed è accessibile in Internet Explorer per eseguire l'elaborazione XML lato client nelle applicazioni in stile AJAX. Può essere usato da qualsiasi linguaggio di programmazione che supporta COM, tra cui C++, JavaScript e [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 6.0.  
  
 L'utilizzo di MSXML non è consigliato in codice gestito basato sul CLR (Common Language Runtime).  
  
## <a name="linq-to-xml-vs-xmllite"></a>LINQ to XML e XmlLite  
 XmlLite è un parser di tipo pull e forward-only che non supporta la memorizzazione nella cache. Gli sviluppatori usano XmlLite principalmente con C++. Non è consigliabile usare XmlLite con codice gestito.  
  
 Il vantaggio principale di XmlLite è che si tratta di un parser XML veloce e leggero, sicuro nella maggior parte degli scenari. La superficie di rischio è molto ridotta. Se è necessario analizzare documenti non attendibili e si desidera proteggersi da attacchi di tipo Denial of Service o esposizione di dati, XmlLite rappresenta una buona soluzione.  
  
 XmlLite non è integrato con [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]. Offre ai programmatori miglioramenti per la produttività che sono la principale motivazione alla base [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/getting-started-linq-to-xml.md)
