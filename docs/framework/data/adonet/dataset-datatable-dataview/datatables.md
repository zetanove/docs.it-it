---
title: "DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52ff0e32-3e5a-41de-9a3b-7b04ea52b83e
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataTable
Un tipo <xref:System.Data.DataSet> è composto da una raccolta di tabelle, relazioni e vincoli.  In ADO.NET gli oggetti <xref:System.Data.DataTable> vengono usati per rappresentare le tabelle in un **DataSet**.  Una **DataTable** rappresenta una tabella di dati relazionali in memoria. Tali dati sono locali rispetto all'applicazione basata su .NET in cui risiedono, ma possono provenire da un'origine dati quale Microsoft SQL Server tramite **DataAdapter**. Per altre informazioni, vedere [Popolamento di un dataset da un oggetto DataAdapter](../../../../../docs/framework/data/adonet/populating-a-dataset-from-a-dataadapter.md).  
  
 La classe **DataTable** è un membro dello spazio dei nomi **System.Data** all'interno della libreria di classi .NET Framework.  È possibile creare e usare una **DataTable** in modo indipendente o come membro di un **DataSet** e gli oggetti **DataTable** possono essere usati anche insieme ad altri oggetti .NET Framework, incluso l'oggetto <xref:System.Data.DataView>.  È possibile accedere alla raccolta di tabelle di un **DataSet** tramite la proprietà **Tables** dell'oggetto **DataSet**.  
  
 Lo schema o struttura di una tabella è rappresentato da colonne e vincoli.  Per definire lo schema di una **DataTable**, è possibile usare gli oggetti <xref:System.Data.DataColumn> o gli oggetti <xref:System.Data.ForeignKeyConstraint> e <xref:System.Data.UniqueConstraint>.  Le colonne di una tabella possono essere associate a colonne di un'origine dati, contenere valori calcolati da espressioni, incrementare automaticamente i propri valori o contenere valori di chiavi primarie.  
  
 Oltre a uno schema, è necessario che **DataTable** disponga anche di righe per contenere e ordinare i dati.  La classe <xref:System.Data.DataRow> rappresenta i dati effettivi contenuti in una tabella.  La classe **DataRow** e i relativi metodi e proprietà consentono di recuperare, valutare e modificare i dati di una tabella.  Quando si accede ai dati di una riga e li si modifica, l'oggetto **DataRow** conserva sia lo stato corrente che lo stato originale.  
  
 L'utilizzo di una o più colonne correlate delle tabelle consente di creare relazioni padre\-figlio tra tabelle.  È possibile creare una relazione tra oggetti **DataTable** tramite un tipo <xref:System.Data.DataRelation>.  Gli oggetti **DataRelation** possono quindi essere usati per restituire le righe padre o figlio correlate di una particolare riga.  Per altre informazioni, vedere [Aggiunta di DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md).  
  
## In questa sezione  
 [Creazione di una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-datatable.md)  
 Viene spiegato come creare una **DataTable** e aggiungerla a un **DataSet**.  
  
 [Definizione dello schema di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)  
 Vengono fornite informazioni sulla creazione e l'uso di oggetti e vincoli **DataColumn**.  
  
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)  
 Viene spiegato come aggiungere, modificare ed eliminare i dati di una tabella  e come usare gli eventi **DataTable** per esaminare le modifiche apportate ai dati della tabella.  
  
 [Gestione degli eventi di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md)  
 Vengono fornite informazioni relative agli eventi disponibili per l'uso con un oggetto **DataTable**, inclusi gli eventi relativi alla modifica di valori di colonna e all'aggiunta o all'eliminazione di righe.  
  
## Sezioni correlate  
 [ADO.NET](../../../../../docs/framework/data/adonet/index.md)  
 Vengono descritti l'architettura e i componenti di ADO.NET e come usarli per l'accesso alle origini dati esistenti e per la gestione dei dati dell'applicazione.  
  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 Vengono fornite informazioni relative al **DataSet** di ADO.NET, incluse informazioni sulla creazione di relazioni tra tabelle.  
  
 [Classe Constraint](frlrfSystemDataConstraintClassTopic)  
 Vengono fornite informazioni di riferimento relative all'oggetto **Constraint**.  
  
 [Classe DataColumn](frlrfSystemDataDataColumnClassTopic)  
 Vengono fornite informazioni di riferimento relative all'oggetto **DataColumn**.  
  
 [Classe DataSet](frlrfSystemDataDataSetClassTopic)  
 Vengono fornite informazioni di riferimento relative all'oggetto **DataSet**.  
  
 [Classe DataTable](frlrfSystemDataDataTableClassTopic)  
 Vengono fornite informazioni di riferimento relative all'oggetto **DataTable**.  
  
 [Cenni preliminari sulla libreria di classi](../../../../../docs/standard/class-library-overview.md)  
 Viene fornita una panoramica della libreria di classi .NET Framework, incluso lo spazio dei nomi **System** e il relativo spazio dei nomi di secondo livello **System.Data**.  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)