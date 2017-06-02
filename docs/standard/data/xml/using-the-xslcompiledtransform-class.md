---
title: "Utilizzo della classe XslCompiledTransform | Microsoft Docs"
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
ms.assetid: f9b074f6-d6f4-49dd-a093-df510bf0cf7b
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Utilizzo della classe XslCompiledTransform
La classe <xref:System.Xml.Xsl.XslCompiledTransform> è il processore XSLT di Microsoft .NET Framework.  Questa classe consente di compilare fogli di stile e di eseguire trasformazioni XSLT.  
  
> [!NOTE]
>  Sebbene le prestazioni complessive della classe <xref:System.Xml.Xsl.XslCompiledTransform> siano migliori rispetto alla classe <xref:System.Xml.Xsl.XslTransform>, l'esecuzione del metodo <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> della classe <xref:System.Xml.Xsl.XslCompiledTransform> potrebbe risultare più lenta di quella del metodo <xref:System.Xml.Xsl.XslTransform.Load%2A> della classe <xref:System.Xml.Xsl.XslTransform> la prima volta che tale metodo viene chiamato su una trasformazione.  Questa situazione si verifica perché il file XSLT deve essere compilato prima del caricamento.  Per altre informazioni, vedere il post di blog seguente: [XslCompiledTransform Slower che XslTransform?](http://go.microsoft.com/fwlink/?LinkId=130590)  
  
## In questa sezione  
 [Input alla classe XslCompiledTransform](../../../../docs/standard/data/xml/inputs-to-the-xslcompiledtransform-class.md)  
 Vengono descritte le opzioni di input XSLT disponibili.  
  
 [Opzioni di output nella classe XslCompiledTransform](../../../../docs/standard/data/xml/output-options-on-the-xslcompiledtransform-class.md)  
 Vengono descritte le opzioni di output XSLT disponibili.  
  
 [Risoluzione delle risorse esterne durante l'elaborazione XSLT](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md)  
 Viene descritto come usare la classe <xref:System.Xml.XmlResolver> per risolvere risorse esterne.  
  
 [Estensione di fogli di stile XSLT](../../../../docs/standard/data/xml/extending-xslt-style-sheets.md)  
 Viene descritto il supporto delle estensioni XSLT.  
  
|||  
|-|-|  
|[Errori XSLT risolvibili](../../../../docs/standard/data/xml/recoverable-xslt-errors.md)|Vengono elencati i comportamenti discretionary consentiti dalla raccomandazione W3C \(World Wide Web Consortium\) XSLT 1.0 e viene descritto il modo in cui tali comportamenti vengono gestiti dalla classe <xref:System.Xml.Xsl.XslCompiledTransform>.|  
|[Procedura: trasformare un frammento di nodo](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md)|Viene descritto come trasformare un frammento di nodo.|  
  
## Sezioni correlate  
 [Migrazione dalla classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)  
 Viene descritto come migrare il codice dalla classe <xref:System.Xml.Xsl.XslTransform>.  
  
## Vedere anche  
 <xref:System.Xml.Xsl.XsltSettings>   
 <xref:System.Xml.Xsl.XsltMessageEncounteredEventArgs>