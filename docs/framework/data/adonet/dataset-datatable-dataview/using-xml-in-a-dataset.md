---
title: "Utilizzo di XML in un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 35138159-e199-49ec-baf7-1ec6777e171e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Utilizzo di XML in un DataSet
ADO.NET consente di compilare un tipo <xref:System.Data.DataSet> con i dati contenuti in un flusso o documento XML.  È possibile usare il flusso o il documento XML per fornire al tipo <xref:System.Data.DataSet> dati o informazioni relative allo schema oppure entrambi.  Le informazioni fornite dal flusso o documento XML possono essere combinate con i dati o le informazioni relative allo schema già presenti nel tipo <xref:System.Data.DataSet>.  
  
 ADO.NET consente inoltre di creare una rappresentazione XML di un tipo <xref:System.Data.DataSet>, con o senza il relativo schema, in modo da trasportare il <xref:System.Data.DataSet> tramite HTTP e renderlo disponibile per l'uso da parte di un'altra applicazione o piattaforma abilitata per XML.  In una rappresentazione XML di un tipo <xref:System.Data.DataSet> i dati vengono scritti in XML e lo schema, se incluso inline nella rappresentazione, viene scritto usando il linguaggio XSD \(XML Schema Definition Language\).  Il formato ottenuto tramite XML e XSD risulta ottimale per il trasferimento del contenuto di un tipo <xref:System.Data.DataSet> da e verso client remoti.  
  
## In questa sezione  
 [DiffGram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)  
 Vengono fornite informazioni dettagliate su DiffGram, un formato XML usato per la lettura e la scrittura del contenuto di un tipo <xref:System.Data.DataSet>.  
  
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)  
 Vengono illustrate le diverse opzioni disponibili per il caricamento del contenuto di un tipo <xref:System.Data.DataSet> da un documento XML.  
  
 [Scrittura del contenuto di DataSet come dati XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)  
 Viene illustrata la generazione del contenuto di un tipo <xref:System.Data.DataSet> sotto forma di dati XML e vengono descritte le diverse opzioni disponibili relative al formato XML.  
  
 [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)  
 Vengono illustrati i metodi del tipo <xref:System.Data.DataSet> usati per caricare lo schema di un <xref:System.Data.DataSet> da XML.  
  
 [Scrittura delle informazioni relative allo schema di un DataSet come XSD](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-schema-information-as-xsd.md)  
 Vengono illustrate le modalità di utilizzo di un XML Schema e il modo in cui generarne uno da un oggetto <xref:System.Data.DataSet>.  
  
 [Sincronizzazione di DataSet e XmlDataDocument](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)  
 Vengono illustrate le funzionalità disponibili in .NET Framework per l'accesso sincrono alle visualizzazioni relazionale e gerarchica di un singolo set di dati e viene descritto come creare una relazione sincrona tra un tipo <xref:System.Data.DataSet> e un tipo <xref:System.Xml.XmlDataDocument>.  
  
 [DataRelation annidati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)  
 Viene illustrata l'importanza degli oggetti <xref:System.Data.DataRelation> annidati per la rappresentazione del contenuto di un tipo <xref:System.Data.DataSet> sotto forma di dati XML e ne viene descritta la creazione.  
  
 [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 Viene descritta la struttura relazionale, o schema, di un oggetto <xref:System.Data.DataSet> creato da un XML Schema.  
  
 [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)  
 Viene descritta la struttura relazionale risultante, o schema, di un tipo <xref:System.Data.DataSet> creato tramite inferenza da elementi XML.  
  
## Sezioni correlate  
 [Cenni preliminari su ADO.NET](../../../../../docs/framework/data/adonet/ado-net-overview.md)  
 Vengono descritti l'architettura e i componenti di ADO.NET e come usare ADO.NET per l'accesso alle origini dati esistenti e per la gestione dei dati dell'applicazione.  
  
## Vedere anche  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)