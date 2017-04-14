---
title: "Elaborazione di dati XML in memoria | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 1bbb4d05-ead7-4bda-8ece-f86d35c57ad4
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Elaborazione di dati XML in memoria
Microsoft .NET Framework include tre modelli per l'elaborazione dei dati XML: la classe <xref:System.Xml.XmlDocument>, la classe <xref:System.Xml.XPath.XPathDocument> e [LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md).  
  
 La classe <xref:System.Xml.XmlDocument> consente l'implementazione delle raccomandazioni di base di livello 1 e 2 del modello DOM W3C.  Il modello DOM è una rappresentazione in memoria \(cache\) dell'albero di un documento XML.  Usando la classe <xref:System.Xml.XmlDocument> e le classi correlate è possibile costruire documenti XML, caricare e accedere ai dati, modificare i dati e salvare le modifiche.  
  
 La classe <xref:System.Xml.XPath.XPathDocument> è un archivio dati in memoria, di sola lettura, basato sul modello dati XPath.  La classe <xref:System.Xml.XPath.XPathNavigator> offre diverse opzioni di modifica e funzionalità di navigazione usando un modello di cursore sui documenti XML contenuti nella classe <xref:System.Xml.XPath.XPathDocument> di sola lettura, nonché nella classe <xref:System.Xml.XmlDocument>.  
  
 [LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md) rappresenta il nuovo modello di elaborazione dei dati XML incluso in .NET Framework versione 3.5.  È un modello in memoria che sfrutta [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md).  LINQ estende la sintassi dei linguaggi C\# e Visual Basic offrendo nuove funzionalità di query.  
  
## In questa sezione  
 [Elaborazione di dati XML con il modello DOM](../../../../docs/standard/data/xml/process-xml-data-using-the-dom-model.md)  
 Viene illustrato l'uso della classe <xref:System.Xml.XmlDocument> e delle classi correlate per l'elaborazione dei dati XML.  
  
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
 Viene illustrato l'uso delle classi <xref:System.Xml.XPath.XPathDocument>, <xref:System.Xml.XmlDocument> e <xref:System.Xml.XPath.XPathNavigator> e delle classi correlate per l'elaborazione dei dati XML.  
  
 [Elaborazione di dati XML utilizzando LINQ to XML](../../../../docs/standard/data/xml/process-xml-data-using-linq-to-xml.md)  
 Viene fornita una breve panoramica di LINQ to XML e sono elencati i collegamenti alla relativa documentazione.  
  
## Sezioni correlate  
 [Documenti e dati XML](../../../../docs/standard/data/xml/index.md)