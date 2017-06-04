---
title: "Elaborazione di dati XML con il modello di dati XPath | Microsoft Docs"
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
ms.assetid: 536c6fce-1453-4654-9c72-bca54d47e081
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Elaborazione di dati XML con il modello di dati XPath
Lo spazio dei nomi <xref:System.Xml?displayProperty=fullName> fornisce una rappresentazione programmatica in memoria di documenti, frammenti, nodi o set di nodi XML usando la classe <xref:System.Xml.XmlDocument> o la classe <xref:System.Xml.XPath.XPathDocument>.  
  
 La classe <xref:System.Xml.XPath.XPathDocument> fornisce una rappresentazione in memoria rapida e di sola lettura di un documento XML usando il modello di dati XPath.  La classe <xref:System.Xml.XmlDocument> fornisce una rappresentazione in memoria modificabile di un documento XML implementando i componenti di base delle specifiche Document Object Model \(DOM\) Level 1 e Level 2 di W3C.  Entrambe le classi consentono di implementare l'interfaccia <xref:System.Xml.XPath.IXPathNavigable> e di restituire un oggetto <xref:System.Xml.XPath.XPathNavigator> usato per selezionare, valutare, esplorare e, in alcuni casi, modificare i dati XML sottostanti.  
  
 Nelle sezioni riportate seguenti viene descritta la funzionalità della classe <xref:System.Xml.XPath.XPathNavigator> in base alla classe che la restituisce.  
  
## Contenuto della sezione  
 [Lettura di dati XML con XPathDocument e XmlDocument](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md)  
 Viene illustrato come creare un oggetto di sola lettura della classe <xref:System.Xml.XPath.XPathDocument> per leggere un documento XML, nonché come creare un oggetto modificabile della classe <xref:System.Xml.XmlDocument> per leggere e modificare un documento XML.  Nell'argomento viene inoltre illustrato come restituire un oggetto <xref:System.Xml.XPath.XPathNavigator> da ogni classe per esplorare e modificare un documento XML.  
  
 [Selezione, valutazione e corrispondenza di dati XML con XPathNavigator](../../../../docs/standard/data/xml/selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)  
 Vengono illustrati i metodi della classe <xref:System.Xml.XPath.XPathNavigator> usati per selezionare nodi in un oggetto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument> usando una query XPath, valutare ed esaminare i risultati di un'espressione XPath e determinare se un nodo in un documento XML corrisponde a un'espressione XPath specifica.  
  
 [Accesso ai dati XML con XPathNavigator](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)  
 Vengono illustrati i metodi della classe <xref:System.Xml.XPath.XPathNavigator> usati per esplorare i nodi, estrarre dati XML e accedere a dati XML tipizzati in modo sicuro in un oggetto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument>.  
  
 [Modifica di dati XML con XPathNavigator](../../../../docs/standard/data/xml/editing-xml-data-using-xpathnavigator.md)  
 Vengono illustrati i metodi della classe <xref:System.Xml.XPath.XPathNavigator> usati per inserire, modificare e rimuovere nodi e valori da un documento XML contenuto in un oggetto <xref:System.Xml.XmlDocument>.  
  
 [Convalida dello schema con XPathNavigator](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md)  
 Vengono illustrati i metodi di valutazione del contenuto XML in un oggetto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument>.  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello DOM](../../../../docs/standard/data/xml/process-xml-data-using-the-dom-model.md)