---
title: "Opzioni di elaborazione XML | Microsoft Docs"
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
ms.assetid: 33ced8ee-1745-4e71-8dee-ebe70ec067c7
caps.latest.revision: 5
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 5
---
# Opzioni di elaborazione XML
Per un elenco di tecnologie Microsoft usabili per l'elaborazione dei dati XML, vedere le tabelle riportate di seguito.  
  
## Opzioni di .NET Framework  
  
|**Opzione**|**Tipo di elaborazione**|**Descrizione**|  
|-----------------|------------------------------|---------------------|  
|[LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md) <br /> \(spazio dei nomi <xref:System.Xml.Linq>\)|In memoria|-   Basata sulla tecnologia LINQ \(Language Integrated Query\) di .NET Framework.<br />-   Garantisce un utilizzo delle query simile a SQL per oggetti, dati relazionali e dati XML.<br />-   Fornisce funzionalità intuitive per la creazione e la trasformazione di documenti.<br />-   Usare questa opzione se si scrive del nuovo codice.|  
|<xref:System.Xml.XmlReader?displayProperty=fullName>|Basata sul flusso|-   Fornisce un accesso rapido, non memorizzato nella cache, di tipo forward\-only ai dati XML.<br />-   È possibile creare oggetti usando il metodo <xref:System.Xml.XmlReader.Create%2A?displayProperty=fullName>, nonché specificare il set di funzionalità da abilitare nell'oggetto tramite la classe <xref:System.Xml.XmlReaderSettings>.|  
|<xref:System.Xml.XmlWriter?displayProperty=fullName>|Basata sul flusso|-   Fornisce una generazione rapida, non memorizzata nella cache, di tipo forward\-only dei dati XML.<br />-   È possibile creare oggetti usando il metodo <xref:System.Xml.XmlWriter.Create%2A?displayProperty=fullName>, nonché specificare il set di funzionalità da abilitare nell'oggetto tramite la classe <xref:System.Xml.XmlWriterSettings>.|  
|<xref:System.Xml.XmlDocument?displayProperty=fullName>|In memoria|-   Implementa le raccomandazioni [W3C Document Object Model \(DOM\) Level 1 Core](http://www.w3.org/TR/REC-DOM-Level-1/level-one-core.html) e [DOM Level 2 Core](http://www.w3.org/TR/DOM-Level-2-Core/).<br />-   È possibile creare, inserire, rimuovere e modificare nodi usando metodi e proprietà basati sul modello DOM noto.<br />-   Usare questa opzione se si modifica il codice esistente tramite cui viene usato DOM di W3C.|  
|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|In memoria|-   Offre diverse opzioni di modifica e funzionalità di navigazione usando un modello di cursore.<br />-   I documenti XML possono essere contenuti in un oggetto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument>.<br />-   Fornisce prestazioni eccellenti per l'elaborazione di sola lettura di XML.<br />-   Usare questa opzione se si modifica il codice esistente con query XPath o trasformazioni XSLT.|  
|<xref:System.Xml.Xsl.XslCompiledTransform>|In memoria|-   Fornisce opzioni per la trasformazione di dati XML tramite trasformazioni XSL.<br />-   Tramite [Compilatore XSLT \(xsltc.exe\)](../../../../docs/standard/data/xml/xslt-compiler-xsltc-exe.md) è possibile fare riferimento a trasformazioni precompilate nell'applicazione in utilizzo.|  
  
## Opzioni basate su Win32 e COM  
  
|**Opzione**|**Descrizione**|  
|-----------------|---------------------|  
|[XmlLite](http://go.microsoft.com/fwlink/?LinkId=93723)|-   Parser XML rapido, sicuro, che non supporta la memorizzazione nella cache, di tipo forward\-only con cui è possibile compilare applicazioni XML a elevate prestazioni.<br />-   È compatibile con qualsiasi linguaggio che usa DLL. Se ne consiglia l'uso con C\+\+.|  
|[MSXML](http://go.microsoft.com/fwlink/?LinkId=93722)|-   Tecnologia basata su COM per l'elaborazione di codice XML inclusa nel sistema operativo Windows.<br />-   Fornisce un'implementazione nativa di DOM con supporto per XPath e XSLT.<br />-   Contiene il parser SAX2 basato su eventi.|  
  
## Vedere anche  
 [Elaborazione di dati XML con il modello DOM](../../../../docs/standard/data/xml/process-xml-data-using-the-dom-model.md)   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Compilatore XSLT \(xsltc.exe\)](../../../../docs/standard/data/xml/xslt-compiler-xsltc-exe.md)