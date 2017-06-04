---
title: "Dataset ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 82b641bb-6001-4512-bf1a-2830acdd92ab
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Dataset ADO.NET
Il <xref:System.Data.DataSet> oggetto è fondamentale per il supporto disconnessi e distribuiti gli scenari di dati con [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)]. Il **set di dati** è una rappresentazione residente in memoria dei dati che fornisce un modello di programmazione relazionale coerente indipendente dall'origine dati. È possibile usarlo con numerose origini dati diverse, con dati XML o per la gestione di dati locali all'applicazione. Il **set di dati** rappresenta un set completo di dati che include tabelle correlate, vincoli e relazioni tra tabelle. La figura seguente mostra il **set di dati** modello a oggetti.  
  
 ![Rappresentazione grafica di ADO.Net](../../../../docs/framework/data/adonet/media/ado-1-bpuedev11.png "ado_1_bpuedev11")  
Modello a oggetti DataSet  
  
 I metodi e gli oggetti in un **set di dati** siano coerenti con quelle del modello di database relazionale.  
  
 Il **set di dati** possono inoltre mantenere e ricaricare il contenuto come XML e il relativo schema sotto forma di schema XML schema definition language (XSD). Per ulteriori informazioni, vedere [Using XML in un set di dati](../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md).  
  
## <a name="the-datatablecollection"></a>DataTableCollection  
 Un [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] **set di dati** contiene una raccolta di zero o più tabelle rappresentate da <xref:System.Data.DataTable> oggetti. Il <xref:System.Data.DataTableCollection> contiene tutti i **DataTable** gli oggetti in un **set di dati**.  
  
 Oggetto **DataTable** è definito nel <xref:System.Data> dello spazio dei nomi e rappresenta una singola tabella di dati residenti in memoria. Contiene una raccolta di colonne rappresentata da un <xref:System.Data.DataColumnCollection>e dei vincoli rappresentati da un <xref:System.Data.ConstraintCollection>, che definiscono lo schema della tabella. Oggetto **DataTable** contiene inoltre un insieme di righe rappresentato dal <xref:System.Data.DataRowCollection>, che contiene i dati nella tabella. Oltre allo stato corrente, un <xref:System.Data.DataRow> vengono mantenute entrambe le versioni correnti e originali per identificare le modifiche ai valori memorizzati nella riga.  
  
## <a name="the-dataview-class"></a>Classe DataView  
 Oggetto <xref:System.Data.DataView> consente di creare diverse visualizzazioni dei dati archiviati in un <xref:System.Data.DataTable>, una funzione che viene spesso utilizzata nelle applicazioni di associazione dati. Utilizzando un <xref:System.Data.DataView>, è possibile esporre i dati in una tabella con diversi ordinamenti ed è possibile filtrare i dati dello stato o basata su un'espressione di filtro di riga. Per ulteriori informazioni, vedere [DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md).  
  
## <a name="the-datarelationcollection"></a>DataRelationCollection  
 Oggetto **set di dati** contiene le relazioni nel relativo <xref:System.Data.DataRelationCollection> oggetto. Una relazione, rappresentata dal <xref:System.Data.DataRelation> oggetto, associa le righe in una **DataTable** con le righe in un altro **DataTable**. Una relazione è analoga a un eventuale percorso di join esistente tra colonne di chiave primaria e di chiave esterna di un database relazionale. Oggetto **DataRelation** identifica le colonne corrispondenti in due tabelle di un **set di dati**.  
  
 Le relazioni consentono la navigazione da una tabella a altra in un **set di dati**. Gli elementi essenziali di un **DataRelation** sono il nome della relazione, il nome di tabelle correlate e le colonne correlate in ogni tabella. È possibile compilare relazioni con più di una colonna per tabella specificando una matrice di <xref:System.Data.DataColumn> oggetti come colonne chiave. Quando si aggiunge una relazione con il <xref:System.Data.DataRelationCollection>, è possibile aggiungere facoltativamente un **UniqueKeyConstraint** e **ForeignKeyConstraint** per garantire l'integrità dei vincoli quando vengono apportate modifiche ai valori di colonna correlata.  
  
 Per ulteriori informazioni, vedere [aggiunta di oggetti DataRelation](../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md).  
  
## <a name="xml"></a>XML  
 È possibile compilare un **set di dati** da un flusso o documento XML. È possibile utilizzare il flusso o documento XML per fornire al **set di dati** dati, le informazioni sullo schema o entrambi. Le informazioni fornite dal documento o flusso XML possono essere combinate con i dati o informazioni sullo schema già presenti nella **set di dati**. Per ulteriori informazioni, vedere [Using XML in un set di dati](../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md).  
  
## <a name="extendedproperties"></a>ExtendedProperties  
 Il **set di dati**, **DataTable**, e **DataColumn** hanno un **ExtendedProperties** proprietà. **ExtendedProperties** è un **PropertyCollection** in cui è possibile inserire informazioni personalizzate, ad esempio l'istruzione SELECT utilizzata per generare il set di risultati o l'ora di generazione dati. Il **ExtendedProperties** insieme persistente con informazioni sullo schema per il **set di dati**.  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] fornisce funzionalità di esecuzione delle query integrate nel linguaggio per dati disconnessi archiviati in un oggetto DataSet. [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)]utilizza standard [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] sintassi e fornisce la verifica della sintassi in fase di compilazione, la tipizzazione statica e il supporto IntelliSense quando si utilizza il [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] IDE.  
  
 Per ulteriori informazioni, vedere [LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari su ADO.NET](../../../../docs/framework/data/adonet/ado-net-overview.md)   
 [DataSet, DataTable e DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider ADO.NET gestiti e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)