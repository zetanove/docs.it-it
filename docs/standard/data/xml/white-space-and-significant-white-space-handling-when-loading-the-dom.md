---
title: "Gestione degli spazi vuoti e degli spazi vuoti significativi durante il caricamento del DOM | Microsoft Docs"
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
ms.assetid: 1b141a0a-50d8-4ebd-83cd-a84449bb22b2
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Gestione degli spazi vuoti e degli spazi vuoti significativi durante il caricamento del DOM
Quando si carica il documento, è possibile impostare l'opzione che consente di conservare gli spazi vuoti e creare nodi **XmlWhitespace** nell'albero del documento.  Per creare nodi con spazi vuoti, impostare la proprietà **PreserveWhitespace** su true.  Se la proprietà è impostata su **false**, che rappresenta il valore predefinito, i nodi con spazi vuoti non verranno creati.  I nodi con spazi vuoti significativi vengono sempre conservati e i nodi **XmlSignificantWhitespace** vengono sempre creati in memoria per rappresentare tali dati, indipendentemente dall'impostazione del flag **PreserveWhitespace**.  
  
 Se il documento viene caricato da un lettore, l'impostazione della proprietà del flag **PreserveWhitespace** sulla classe **XmlDocument** inciderà sulla creazione dei nodi **XmlWhitespace** solo se la proprietà **WhitespaceHandling** di **XmlTextReader** non è impostata su **WhitespaceHandling.None**.  Il valore della proprietà **WhitespaceHandling** ha la precedenza sull'impostazione del flag nella classe **XmlDocument**.  Per altre informazioni su **XmlSignificantWhitespace**, vedere [Classe XmlSignificantWhitespace](frlrfSystemXmlXmlSignificantWhitespaceClassTopic).  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)