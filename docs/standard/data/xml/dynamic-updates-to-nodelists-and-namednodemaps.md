---
title: "Aggiornamenti dinamici di NodeLists e NamedNodeMaps | Microsoft Docs"
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
ms.assetid: 76c511fd-6704-4ca4-8078-860a68d898ad
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Aggiornamenti dinamici di NodeLists e NamedNodeMaps
Poiché in **XmlNodeList** e **XmlNamedNodeMap** è contenuto un set di nodi e il documento XML è già stato caricato in memoria e sottoposto a modifiche, il W3C \(World Wide Web Consortium\) stabilisce che questi oggetti contenenti set di nodi debbano essere dinamici.  Vale a dire che, se il documento sottostante cambia, anche i dati di questi due oggetti cambiano di conseguenza.  Pertanto, se si dispone di un oggetto **XmlNodeList** contenente tutti gli elementi figlio di un particolare elemento, ad esempio l'elemento X, e si aggiunge quindi un ulteriore elemento, l'elemento Q, al documento sotto l'elemento X,  anche l'oggetto **XmlNodeList** conterrà il nuovo elemento Q aggiunto alla relativa raccolta.  Lo stesso vale per il contrario.  Se si aggiunge un nodo a **XmlNodeList**, il documento sottostante viene anch'esso aggiornato.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)