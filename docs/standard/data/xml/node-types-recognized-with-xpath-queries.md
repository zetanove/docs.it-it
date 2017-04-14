---
title: "Tipi di nodo riconosciuti con le query XPath | Microsoft Docs"
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
ms.assetid: 1d33e22d-18e5-43f8-a466-2e3d0a8dd094
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Tipi di nodo riconosciuti con le query XPath
I tipi di nodi riconosciuti in una query XPath non corrispondono a quelli del DOM \(Document Object Model\).  
  
## Tipi di nodo XPath W3C  
 I tipi di nodo riconosciuti in una query XPath non corrispondono a quelli del DOM \(Document Object Model\).  Di seguito sono riportati i tipi di nodo XPath rappresentati dall'enumerazione <xref:System.Xml.XPath.XPathNodeType>.  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
 Questi tipi di nodo sono basati sul modello dati XPath, dove i nodi derivano dal set di informazioni XML.  I tipi di nodo <xref:System.Xml.XPath.XPathNodeType> e <xref:System.Xml.XPath.XPathNodeType> sono estensioni Microsoft .NET Framework dei tipi di nodi di base descritti nel modello dati XPath.  
  
 Il tipo di nodo Attribute viene usato in modo diverso nel modello dati XPath rispetto al DOM.  Nel modello dati XPath il nodo di tipo element è composto da un set di nodi Attribute a esso correlati e il nodo di tipo element è il padre di ogni nodo Attribute.  Nel DOM, tuttavia, il nodo di tipo element è il proprietario e non il padre.  In entrambi i modelli, i nodi Attribute e Namespace non sono considerati nodi figlio del nodo di tipo element.  
  
 Il tipo di nodo Namespace è un'aggiunta al modello dati XPath e non è un tipo di nodo DOM riconosciuto.  
  
 Per altre informazioni sull'esplorazione dei nodi Attribute, Namespace e di tipo element, vedere gli argomenti [Navigazione del set di nodi con XPathNavigator](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md) e [Navigazione dei nodi di attributi e dello spazio dei nomi con XPathNavigator](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md).  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Selezione di dati XML con XPathNavigator](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)   
 [Valutazione di espressioni XPath con XPathNavigator](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)   
 [Corrispondenza di nodi utilizzando XPathNavigator](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)   
 [Query e spazi dei nomi XPath](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)   
 [Espressioni XPath compilate](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)