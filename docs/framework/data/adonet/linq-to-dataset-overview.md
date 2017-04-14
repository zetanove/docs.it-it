---
title: "Cenni preliminari su LINQ to DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dc20a8fb-03f6-4b68-9c2b-7f7299e3070b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Cenni preliminari su LINQ to DataSet
<xref:System.Data.DataSet> è uno dei componenti più utilizzati di [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)]. Rappresenta un elemento chiave del modello di programmazione disconnesso su cui si basa [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] e consente di memorizzare in modo esplicito nella cache dati di origini dati diverse. Per il livello della presentazione <xref:System.Data.DataSet> è strettamente integrato nei controlli GUI per l'associazione dati. Per il livello intermedio fornisce una cache che mantiene la forma relazionale dei dati e include servizi di navigazione all'interno della gerarchia e di query semplici e rapidi.  Una tecnica comune usata per ridurre il numero di richieste su un database consiste nell'usare <xref:System.Data.DataSet> per la memorizzazione nella cache di livello intermedio.  Si consideri ad esempio un'applicazione Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] basata sui dati.  Spesso, una parte significativa dei dati dell'applicazione non viene modificata frequentemente ed è comune a più sessioni o utenti.  Tali dati possono essere mantenuti in memoria sul server Web, in modo da ridurre il numero di richieste al database e velocizzare le interazioni utente.  Un altro aspetto utile di <xref:System.Data.DataSet> è che consente a un'applicazione di portare nello spazio dell'applicazione subset di dati da una o più origini dati.  L'applicazione può quindi modificare i dati in memoria, mantenendo comunque la propria forma relazionale.  
  
 Nonostante l'importanza che lo contraddistingue, <xref:System.Data.DataSet> dispone di funzionalità limitate di query.  È possibile usare il metodo <xref:System.Data.DataTable.Select%2A> per il filtro e l'ordinamento e i metodi <xref:System.Data.DataRow.GetChildRows%2A> e <xref:System.Data.DataRow.GetParentRow%2A> per la navigazione all'interno della gerarchia.  Per operazioni più complesse, tuttavia, lo sviluppatore deve scrivere una query personalizzata.  Le applicazioni risultanti possono quindi essere difficilmente gestibili e caratterizzate da prestazioni inadeguate.  
  
 Con [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] è più facile e veloce eseguire una query su dati memorizzati nella cache di un oggetto <xref:System.Data.DataSet>.  Queste query sono espresse nel linguaggio di programmazione stesso, anziché come valori letterali stringa incorporati nel codice dell'applicazione.  Gli sviluppatori non devono pertanto imparare un diverso linguaggio di query.  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] consente inoltre di incrementare la produttività degli sviluppatori di [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], poiché l'IDE di [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] fornisce il controllo della sintassi in fase di compilazione, la tipizzazione statica e il supporto IntelliSense per [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)].  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] può inoltre essere usato per eseguire query su dati che sono stati consolidati da una o più origini dati.  In tal modo sono possibili molti scenari in cui è necessario poter rappresentare e gestire i dati con flessibilità.  In particolare, questo tipo di modifiche sono richieste nelle applicazioni generiche per la creazione di rapporti, di analisi e di Business Intelligence.  
  
## Esecuzione di query su DataSet con LINQ to DataSet  
 Prima di poter eseguire query su un oggetto <xref:System.Data.DataSet> con [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], è necessario popolare <xref:System.Data.DataSet>. È possibile caricare dati in un oggetto <xref:System.Data.DataSet> in diversi modi, ad esempio usando la classe <xref:System.Data.Common.DataAdapter> o [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md).  È possibile iniziare a eseguire query su un oggetto <xref:System.Data.DataSet> dopo avervi caricato i dati.  La formulazione di query con [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] è simile all'utilizzo di [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] su altre origini dati con supporto [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)].  È possibile eseguire query [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] su singole tabelle di un oggetto <xref:System.Data.DataSet> o su più di una tabella usando gli operatori di query standard <xref:System.Linq.Enumerable.Join%2A> e <xref:System.Linq.Enumerable.GroupJoin%2A>.  
  
 Sono supportate query [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] su oggetti <xref:System.Data.DataSet> tipizzati e non tipizzati.  Se si conosce lo schema di <xref:System.Data.DataSet> in fase di progettazione dell'applicazione, è consigliabile usare <xref:System.Data.DataSet> tipizzati. In un <xref:System.Data.DataSet> tipizzato, per ciascuna colonna delle tabelle e delle righe sono disponibili membri tipizzati, pertanto le query risultano più semplici e più leggibili.  
  
 Oltre agli operatori di query standard implementati in  System.Core.dll, [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] aggiunge diverse estensioni specifiche di <xref:System.Data.DataSet> che semplificano l'esecuzione di query su un set di oggetti <xref:System.Data.DataRow>.  Le estensioni specifiche di <xref:System.Data.DataSet> includono operatori per il confronto di sequenze di righe, nonché metodi che forniscono accesso ai valori di colonna di un oggetto <xref:System.Data.DataRow>.  
  
## Applicazioni a più livelli e LINQ to DataSet  
 Le applicazioni dati a più livelli sono applicazioni mirate ai dati separate in più livelli logici.  Una tipica applicazione a più livelli include un livello di presentazione, un livello intermedio e un livello dati.  La separazione dei componenti dell'applicazione in livelli aumenta la gestibilità e la manutenibilità dell'applicazione,  Per altre informazioni sulle applicazioni a più livelli, vedere [Utilizzo dei dataset nelle applicazioni a più livelli](../Topic/Work%20with%20datasets%20in%20n-tier%20applications.md).  
  
 Nelle applicazioni a più livelli <xref:System.Data.DataSet> viene spesso usato nel livello intermedio per memorizzare nella cache le informazioni per un'applicazione Web.  La funzionalità di query di [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] viene implementata tramite metodi di estensione e consente di estendere l'oggetto <xref:System.Data.DataSet> esistente di ADO.NET 2.0 .  
  
## Vedere anche  
 [Esecuzione di query su DataSet](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)