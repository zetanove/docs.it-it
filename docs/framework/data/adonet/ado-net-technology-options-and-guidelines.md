---
title: "Linee guida e opzioni della tecnologia ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8577281-38e6-4ce5-b036-572039a4c3d8
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Linee guida e opzioni della tecnologia ADO.NET
ADO.NET Data Platform è una strategia multi\-versione concepita per ridurre la quantità di codice e di interventi di manutenzione richiesti per gli sviluppatori consentendo loro di eseguire la programmazione per modelli di dati di entità concettuali.  Questa piattaforma include ADO.NET Entity Framework e le tecnologie correlate.  
  
## Entity Framework  
 ADO.NET Entity Framework è progettato per consentire agli sviluppatori di creare applicazioni di accesso ai dati tramite programmazione in base a un modello di applicazione concettuale anziché direttamente in base a uno schema di archiviazione relazionale.  L'obiettivo è quello di ridurre la quantità di codice e le operazioni di manutenzione necessarie per le applicazioni orientate ai dati.  Per altre informazioni, vedere [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md).  
  
### Entity Data Model \(EDM\)  
 Entity Data Model \(EDM\) è una specifica di progettazione che definisce i dati dell'applicazione come set di entità e relazioni.  I dati in questo modello supportano il mapping relazionale oggetti e la programmabilità dei dati tra diverse applicazioni.  
  
### Object Services  
 Object Services consente ai programmatori di interagire con il modello concettuale tramite un set di classi CLR \(Common Language Runtime\).  Tali classi possono essere generate automaticamente dal modello concettuale o sviluppate in modo indipendente per riflettere la struttura del modello.  Object Services offre inoltre supporto per l'infrastruttura per Entity Framework, inclusi servizi quali la gestione dello stato, il rilevamento delle modifiche, la risoluzione di identità, il caricamento e la navigazione di relazioni, la propagazione di modifiche degli oggetti in modifiche del database e il supporto per la compilazione di query per Entity SQL.  Per altre informazioni, vedere [Object Services Overview \(Entity Framework\)](http://msdn.microsoft.com/it-it/43014cf9-c9cb-4538-bfbb-197820b60038).  
  
### LINQ to Entities  
 LINQ to Entities è un'implementazione di LINQ \(Language Integrated Query\) che consente agli sviluppatori di creare query fortemente tipizzate sul contesto dell'oggetto di Entity Framework usando espressioni LINQ e operatori di query standard LINQ.  LINQ to Entities consente agli sviluppatori di lavorare con un modello concettuale con un mapping relazionale oggetti estremamente flessibile in database di Microsoft SQL Server e di terze parti.  Per altre informazioni, vedere [LINQ to Entities](../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md).  
  
### Entity SQL  
 Entity SQL è un linguaggio di query basato su testo progettato per interagire con Entity Data Model.  Entity SQL è un dialetto SQL che contiene costrutti per l'esecuzione di query in termini di concetti di modellazione di livello superiore, ad esempio ereditarietà, tipi complessi e relazioni esplicite.  Gli sviluppatori possono anche usare Entity SQL direttamente con Object Services.  Per altre informazioni, vedere [Linguaggio Entity SQL](../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md).  
  
### EntityClient  
 EntityClient è un nuovo provider di dati .NET Framework usato per l'interazione con Entity Data Model.  Come gli altri provider di dati .NET Framework, EntityClient espone oggetti <xref:System.Data.EntityClient.EntityConnection> e <xref:System.Data.EntityClient.EntityCommand> che restituiscono un oggetto <xref:System.Data.EntityClient.EntityDataReader>.  EntityClient usa il linguaggio Entity SQL, fornendo mapping flessibile ai provider di dati specifici dell'archiviazione.  Per altre informazioni, vedere [EntityClient and Entity SQL](http://msdn.microsoft.com/it-it/49202ab9-ac98-4b4b-a05c-140e422bf527).  
  
### Strumenti di Entity Data Model  
 Entity Framework fornisce finestre di progettazione, procedure guidate e strumenti da riga di comando per semplificare la compilazione di applicazioni EDM.  Il controllo EntityDataSource supporta scenari di associazione dati basati su EDM.  La superficie di programmazione del controllo EntityDataSource è simile agli altri controlli origine dati in Visual Studio.  Per altre informazioni, vedere [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/it-it/91076853-0881-421b-837a-f582f36be527).  
  
## LINQ to SQL  
 LINQ to SQL è un'implementazione del mapping relazionale a oggetti che consente di modellare un database SQL Server tramite le classi di .NET Framework.  LINQ to SQL consente di eseguire una query sul database tramite LINQ nonché di aggiornare, inserire ed eliminare dati da esso.  LINQ to SQL supporta transazioni, visualizzazioni e stored procedure consentendo di integrare facilmente le regole relative alla convalida dei dati e alla logica di business nel modello dati.  È possibile usare Progettazione relazionale oggetti per modellare le classi di entità e le associazioni basate sugli oggetti in un database.  Per altre informazioni, vedere [LINQ to SQL Tools in Visual Studio](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio2.md).  
  
## WCF Data Services  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] distribuisce servizi dati nel Web o in una rete Intranet.  I dati sono strutturati come entità e relazioni in base alle specifiche di Entity Data Model.  I dati distribuiti in questo modello sono indirizzabili tramite il protocollo HTTP standard.  Per altre informazioni, vedere [WCF Data Services 4.5](../../../../docs/framework/data/wcf/index.md).  
  
## Vedere anche  
 [Cenni preliminari su ADO.NET](../../../../docs/framework/data/adonet/ado-net-overview.md)   
 [Novità di ADO.NET](../../../../docs/framework/data/adonet/whats-new.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)