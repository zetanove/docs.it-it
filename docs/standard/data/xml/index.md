---
title: "Documenti e dati XML | Microsoft Docs"
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
ms.assetid: e695047f-3c0f-4045-8708-5baea91cc380
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Documenti e dati XML
.NET Framework fornisce un set completo e integrato di classi tramite cui è possibile compilare facilmente applicazioni che supportano XML.  Le classi negli spazi dei nomi seguenti supportano l'analisi e la scrittura del codice XML, la modifica dei dati XML in memoria, la convalida dei dati e la trasformazione XSLT.  
  
-   <xref:System.Xml>  
  
-   <xref:System.Xml.XPath>  
  
-   <xref:System.Xml.Xsl>  
  
-   <xref:System.Xml.Schema>  
  
-   <xref:System.Xml.Linq>  
  
 Per un elenco completo, vedere la pagina Web relativa agli [spazi dei nomi System.Xml](http://msdn.microsoft.com/library/gg145036.aspx).  
  
 Le classi in questi spazi dei nomi supportano le raccomandazioni W3C \(World Wide Web Consortium\).  Ad esempio:  
  
-   La classe <xref:System.Xml.XmlDocument?displayProperty=fullName> implementa le raccomandazioni [W3C Document Object Model \(DOM\) Level 1 Core](http://www.w3.org/TR/REC-DOM-Level-1/) e [DOM Level 2 Core](http://www.w3.org/TR/DOM-Level-2-Core/).  
  
-   Le classi <xref:System.Xml.XmlReader?displayProperty=fullName> e <xref:System.Xml.XmlWriter?displayProperty=fullName> supportano le raccomandazioni [W3C XML 1.0](http://www.w3.org/TR/2006/REC-xml-20060816/) e [Namespaces in XML](http://www.w3.org/TR/REC-xml-names/).  
  
-   Gli schemi nella classe <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=fullName> supportano le raccomandazioni [W3C XML Schema Part 1: Structures](http://www.w3.org/TR/xmlschema-1/) e [XML Schema Part 2: Datatypes](http://www.w3.org/TR/xmlschema-2/).  
  
-   Le classi nello spazio dei nomi <xref:System.Xml.Xsl?displayProperty=fullName> supportano le trasformazioni XSLT conformi alla raccomandazione [W3C XSLT 1.0](http://www.w3.org/TR/xslt).  
  
 Le classi XML in .NET Framework offrono i vantaggi seguenti:  
  
-   **Produttività.** Grazie a [LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md) è più semplice programmare con XML. Inoltre, viene garantito un utilizzo delle query simile a SQL.  
  
-   **Estendibilità.** Le classi XML di .NET Framework sono estendibili mediante l'uso di classi di base astratte e metodi virtuali.  Ad esempio, è possibile creare una classe derivata della classe <xref:System.Xml.XmlUrlResolver> tramite cui viene archiviato il flusso della cache nel disco locale.  
  
-   **Architettura modulare.** .NET Framework offre un'architettura in cui è possibile un utilizzo interscambiabile dei componenti e i dati possono essere trasmessi tra i componenti.  Ad esempio, un archivio dati quale un oggetto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument> può essere trasformato con la classe <xref:System.Xml.Xsl.XslCompiledTransform> e l'output potrà quindi essere inserito in un flusso di un altro archivio o restituito come flusso da un servizio Web.  
  
-   **Prestazioni.** Per prestazioni ottimali dell'applicazione, alcune delle classi XML di .NET Framework supportano un modello basato sul flusso con le caratteristiche seguenti:  
  
    -   Minimo utilizzo della memorizzazione nella cache per l'analisi di tipo forward\-only, modello pull \(<xref:System.Xml.XmlReader>\).  
  
    -   Convalida di tipo forward\-only \(<xref:System.Xml.XmlReader>\).  
  
    -   Tipo di navigazione tramite cursore grazie al quale la creazione di nodi è ridotta a un singolo nodo virtuale, fornendo nel contempo l'accesso casuale al documento \(<xref:System.Xml.XPath.XPathNavigator>\).  
  
     Per ottimizzare le prestazioni ogni volta che è necessaria l'elaborazione XSLT, è possibile usare la classe <xref:System.Xml.XPath.XPathDocument>, vale a dire un archivio ottimizzato di sola lettura per query XPath progettate per interagire in modo efficiente con la classe <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
-   **Integrazione con ADO.NET.** Le classi XML e [ADO.NET](../../../../docs/framework/data/adonet/index.md) sono strettamente integrati per raggruppare dati relazionali e XML.  La classe <xref:System.Data.DataSet> è una cache in memoria dei dati recuperati da un database.  Con la classe <xref:System.Data.DataSet> è possibile leggere e scrivere il codice XML usando le classi <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlWriter>, mantenere la struttura interna degli schemi relazionali come XML Schema \(XSD\) e dedurre la struttura dello schema di un documento XML.  
  
## In questa sezione  
 [Opzioni di elaborazione XML](../../../../docs/standard/data/xml/xml-processing-options.md)  
 Vengono illustrate le opzioni per l'elaborazione di dati XML.  
  
 [Elaborazione di dati XML in memoria](../../../../docs/standard/data/xml/processing-xml-data-in-memory.md)  
 Vengono illustrati i tre modelli per l'elaborazione dei dati XML in memoria.  [LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md), la classe <xref:System.Xml.XmlDocument> \(basata sul modello DOM di W3C\) e la classe <xref:System.Xml.XPath.XPathDocument> \(basata sul modello di dati XPath\).  
  
 [Trasformazioni XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)  
 Viene descritto come usare il processore XSLT.  
  
 [SOM \(Schema Object Model\) XML](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)  
 Vengono descritte le classi usate per la compilazione e la modifica di XML Schema \(XSD\) fornendo una classe <xref:System.Xml.Schema.XmlSchema> per il caricamento e la modifica di uno schema.  
  
 [Integrazione di XML con dati relazionali e ADO.NET](../../../../docs/standard/data/xml/xml-integration-with-relational-data-and-adonet.md)  
 Viene descritto come .NET Framework consente l'accesso in tempo reale e in modalità sincrona alle rappresentazioni sia relazionali sia gerarchiche di dati tramite gli oggetti <xref:System.Data.DataSet> e <xref:System.Xml.XmlDataDocument>.  
  
 [Gestione di spazi dei nomi in un documento XML](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)  
 Viene descritto come viene usata la classe <xref:System.Xml.XmlNamespaceManager> per archiviare e gestire le informazioni sugli spazi dei nomi.  
  
 [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)  
 Vengono descritti il mapping dei tipi di dati XML ai tipi CLR, la conversione di tipi di dati XML e altre funzionalità di supporto dei tipi nelle classi <xref:System.Xml>.  
  
## Sezioni correlate  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)  
 Vengono fornite informazioni sulle modalità di accesso ai dati usando ADO.NET.  
  
 [Security](../../../../docs/standard/security/index.md)  
 Viene fornita una panoramica sul sistema di sicurezza di .NET Framework.  
  
 [Centro per sviluppatori XML](http://go.microsoft.com/fwlink/?linkid=42458)  
 Vengono forniti download, newsgroup, informazioni tecniche aggiuntive e altre risorse per gli sviluppatori XML.