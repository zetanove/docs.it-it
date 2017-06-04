---
title: "Inferenza della struttura relazionale del DataSet da XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd2f41c6-6785-420e-aa43-3ceb0bdccdce
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Inferenza della struttura relazionale del DataSet da XML
La struttura relazionale, o schema, di un tipo <xref:System.Data.DataSet> è costituita da tabelle, colonne, vincoli e relazioni.  Quando si carica un tipo <xref:System.Data.DataSet> dall'XML, lo schema può essere predefinito oppure creato, implicitamente o tramite inferenza, dall'XML caricato.  Per altre informazioni sul caricamento dello schema e sul contenuto di un tipo <xref:System.Data.DataSet> dall'XML, vedere [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md) e [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md).  
  
 Per creare lo schema di un tipo <xref:System.Data.DataSet> dall'XML, si consiglia di specificare esplicitamente lo schema tramite il linguaggio XSD \(XML Schema Definition Language\), come descritto in [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md), oppure tramite il linguaggio XDR \(XML\-Data Reduced\).  Se nell'XML non è disponibile un XML Schema o uno schema XDR, è possibile inferire lo schema del tipo <xref:System.Data.DataSet> dalla struttura degli elementi e degli attributi XML.  
  
 Contenuto della sezione vengono descritte le regole relative all'inferenza dello schema del tipo <xref:System.Data.DataSet> mediante l'illustrazione degli elementi e degli attributi XML, delle relative strutture e dello schema inferito del tipo <xref:System.Data.DataSet> risultante.  
  
 Non è necessario includere in un processo di inferenza tutti gli attributi presenti in un documento XML.  È possibile che negli attributi qualificati dallo spazio dei nomi siano inclusi metadati importanti per il documento XML ma non per lo schema del tipo <xref:System.Data.DataSet>.  Il metodo <xref:System.Data.DataSet.InferXmlSchema%2A> consente di specificare degli spazi dei nomi da ignorare durante il processo di inferenza.  Per altre informazioni, vedere [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md).  
  
## In questa sezione  
 [Riepilogo del processo di inferenza dello schema di un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/summary-of-the-dataset-schema-inference-process.md)  
 Viene fornito un riepilogo estremamente dettagliato delle regole per l'inferenza dello schema di un tipo <xref:System.Data.DataSet> dall'XML.  
  
 [Inferenza di tabelle](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-tables.md)  
 Vengono descritti gli elementi XML inferiti come tabelle in un tipo <xref:System.Data.DataSet>.  
  
 [Inferenza di colonne](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-columns.md)  
 Vengono descritti gli elementi e gli attributi XML inferiti come colonne di tabelle.  
  
 [Inferenza delle relazioni](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-relationships.md)  
 Vengono descritti gli oggetti <xref:System.Data.DataRelation> e <xref:System.Data.ForeignKeyConstraint> creati per le tabelle annidate inferite.  
  
 [Inferenza del testo degli elementi](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-element-text.md)  
 Vengono descritte le colonne create per il testo negli elementi XML e vengono illustrati i casi in cui tale testo viene ignorato.  
  
 [Limitazioni delle inferenze](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inference-limitations.md)  
 Vengono illustrate le limitazioni dell'inferenza dello schema.  
  
## Sezioni correlate  
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 Viene descritta l'interazione dell'oggetto <xref:System.Data.DataSet> con i dati XML.  
  
 [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 Viene descritta la struttura relazionale, o schema, di un tipo <xref:System.Data.DataSet> creato da uno schema XSD \(XML Schema Definition Language\).  
  
 [Cenni preliminari su ADO.NET](../../../../../docs/framework/data/adonet/ado-net-overview.md)  
 Vengono descritti l'architettura e i componenti di ADO.NET, nonché il relativo uso per accedere alle origini dati esistenti e per gestire i dati dell'applicazione.  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)