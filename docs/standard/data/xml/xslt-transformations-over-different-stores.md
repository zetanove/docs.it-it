---
title: "Trasformazioni XSLT su diversi archivi | Microsoft Docs"
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
ms.assetid: 369850e9-004a-45d2-b5c3-5060d9135adb
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Trasformazioni XSLT su diversi archivi
> [!NOTE]
>  La classe <xref:System.Xml.Xsl.XslTransform> è obsoleta in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)].  È possibile eseguire le trasformazioni XSLT \(Extensible Stylesheet Language for Transformations\) usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>.  Per altre informazioni, vedere [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) e [Migrazione dalla classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md).  
  
 ADO.NET e le classi XML in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] costituiscono un modello di programmazione unificato per accedere ai dati.  Tali dati sono rappresentati come dati XML, vale a dire testo delimitato da tag e dati relazionali, ovvero tabelle composte da righe e colonne.  I dati XML in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] vengono letti dall'XML da qualsiasi flusso di dati in alberi di nodi DOM, dove è possibile accedere ai dati a livello di programmazione, mentre ADO.NET fornisce il mezzo per accedere e modificare i dati relazionali all'interno di un oggetto <xref:System.Data.DataSet>.  
  
 Il DOM XML fornisce l'accesso ai dati nei documenti XML e nelle classi aggiuntive per scrivere, leggere e spostarsi all'interno dei documenti XML.  Queste classi sono supportate nello spazio dei nomi <xref:System.Xml>, che unifica inoltre il DOM XML con i servizi di accesso ai dati forniti da ADO.NET.  L'oggetto <xref:System.Xml.XmlDataDocument> fornisce l'accesso relazionale ai dati.  Il tipo <xref:System.Xml.XmlDataDocument> associa il codice XML ai dati relazionali in un <xref:System.Data.DataSet> di ADO.NET.  In qualsiasi applicazione basata su [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] vengono usate le classi nello spazio dei nomi <xref:System.Xml> per accedere e modificare i documenti XML e i dati relazionali nel tipo <xref:System.Xml.XmlDataDocument>.  Questa implementazione supporta le architetture a più livelli per la raccolta e la distribuzione dei dati.  Per altre informazioni, vedere [Integrazione di XML con dati relazionali e ADO.NET](../../../../docs/standard/data/xml/xml-integration-with-relational-data-and-adonet.md).  
  
## Vedere anche  
 [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)