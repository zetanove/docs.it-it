---
title: "Archivio di istanze del flusso di lavoro SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8cd2f8a5-4bf8-46ea-8909-c7fdb314fabc
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Archivio di istanze del flusso di lavoro SQL
[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] viene fornito con l'archivio di istanze del flusso di lavoro SQL che consente ai flussi di lavoro di rendere persistenti le informazioni sullo stato delle istanze del flusso di lavoro in un database di SQL Server 2005 o di SQL Server 2008.Questa funzionalità viene implementata principalmente nel formato della classe <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> che deriva dalla classe <xref:System.Runtime.Persistence.InstanceStore> astratta del framework di persistenza.La funzionalità di archivio di istanze del flusso di lavoro SQL costituisce un provider di persistenza SQL, ovvero un'implementazione concreta dell'API di persistenza utilizzata da un host per inviare i comandi di persistenza all'archivio.  
  
 L'archivio di istanze del flusso di lavoro SQL supporta sia flussi di lavoro indipendenti o i servizi dei flussi di lavoro che utilizzano l'oggetto <xref:System.Activities.WorkflowApplication> o <xref:System.ServiceModel.WorkflowServiceHost> sia i servizi ospitati in WAS tramite l'oggetto <xref:System.ServiceModel.WorkflowServiceHost>.La funzionalità di archivio di istanze del flusso di lavoro SQL può essere configurata a livello di codice per i servizi indipendenti tramite il modello a oggetti esposto dalla funzionalità.Questa funzionalità può essere configurata per i servizi ospitati dall'oggetto <xref:System.ServiceModel.WorkflowServiceHost> sia a livello di codice tramite il modello a oggetti sia tramite un file di configurazione XML.  
  
 La funzionalità di archivio di istanze del flusso di lavoro SQL \(classe **SqlWorkflowInstanceStore**\) non implementa l'oggetto <xref:System.ServiceModel.Persistence.PersistenceProviderFactory>, pertanto non offre il supporto della persistenza per i servizi WCF durevoli non del flusso di lavoro.Inoltre, non implementando l'oggetto <xref:System.Workflow.Runtime.Hosting.WorkflowPersistenceService>, non offre il supporto della persistenza per i flussi di lavoro 3.x.La funzionalità supporta la persistenza solo per i flussi di lavoro e i relativi servizi di WF 4.0 \(e versione successiva\).La funzionalità non supporta inoltre alcun database diverso da SQL Server 2005 e SQL Server 2008.  
  
 Negli argomenti di questa sezione vengono descritte le proprietà e le funzionalità dell'archivio di istanze del flusso di lavoro SQL e forniti i dettagli sulla configurazione dell'archivio.  
  
 Windows Server AppFabric è dotato di un proprio archivio di istanze e di strumenti per semplificare la configurazione e l'utilizzo dell'archivio.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] vedere [Archivio di istanze di Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=201201).[!INCLUDE[crabout](../../../includes/crabout-md.md)] sul database di persistenza di SQL Server AppFabric vedere [Database di persistenza SQL Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=201202)  
  
## In questa sezione  
  
-   [Proprietà dell'archivio di istanze del flusso di lavoro SQL](../../../docs/framework/windows-workflow-foundation//properties-of-sql-workflow-instance-store.md)  
  
-   [Procedura: abilitare la persistenza SQL per i flussi di lavoro e i relativi servizi](../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)  
  
-   [Attivazione di istanze](../../../docs/framework/windows-workflow-foundation//instance-activation.md)  
  
-   [Supporto per le query](../../../docs/framework/windows-workflow-foundation//support-for-queries.md)  
  
-   [Estensibilità dell'archivio](../../../docs/framework/windows-workflow-foundation//store-extensibility.md)  
  
-   [Sicurezza](../../../docs/framework/windows-workflow-foundation//security.md)  
  
-   [Database di persistenza SQL Server](../../../docs/framework/windows-workflow-foundation//sql-server-persistence-database.md)  
  
## Vedere anche  
 [Esempi di persistenza](http://go.microsoft.com/fwlink/?LinkID=177735)