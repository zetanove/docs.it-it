---
title: "Rimozione di nodi dal DOM | Microsoft Docs"
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
ms.assetid: 0a98e0ca-0555-45c1-ab69-0d8d20ca1abd
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Rimozione di nodi dal DOM
Per rimuovere un nodo specifico dal DOM \(Document Object Model\) XML, usare il metodo <xref:System.Xml.XmlNode.RemoveChild%2A>.  Quando si rimuove un nodo, il metodo rimuove il sottoalbero appartenente al nodo che viene rimosso, purché tale nodo non sia un nodo foglia.  
  
 Per rimuovere più nodi dal DOM, usare il metodo <xref:System.Xml.XmlNode.RemoveAll%2A> che consente di rimuovere tutti gli eventuali elementi figlio e attributi del nodo corrente.  
  
 Se si usa una mappa di nodi <xref:System.Xml.XmlNamedNodeMap>, è possibile rimuovere un nodo usando il metodo <xref:System.Xml.XmlNamedNodeMap.RemoveNamedItem%2A>.  
  
 Per rimuovere gli attributi, vedere [Rimozione di attributi da un nodo di tipo element nel DOM](../../../../docs/standard/data/xml/removing-attributes-from-an-element-node-in-the-dom.md).  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)