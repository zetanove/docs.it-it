---
title: "Deprecated types in Windows Workflow Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4aebe928-a964-4c1c-abf7-0dbbd3604b13
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Deprecated types in Windows Workflow Foundation
In .NET 4 team del flusso di lavoro ha rilasciato un motore del flusso di lavoro totalmente nuovo nello spazio dei nomi <xref:System.Activities>.  Con la versione di .NET 4.5 Beta la maggior parte dei tipi negli spazi dei nomi di "WF 3" <xref:System.Workflow.Activities>, <xref:System.Workflow.ComponentModel> e <xref:System.Workflow.Runtime> vengono contrassegnati come obsoleti.  
  
## Spazi dei nomi e strumenti obsoleti  
 Gli assembly seguenti includono uno o più tipi pubblici che saranno deprecati:  
  
-   System.Workflow.Activities.dll  
  
-   System.Workflow.ComponentModel.dll  
  
-   System.Workflow.Runtime.dll  
  
-   System.WorkflowServices.dll  
  
-   Microsoft.Workflow.DebugController.dll  
  
-   Microsoft.Workflow.Compiler.exe  
  
-   Wfc.exe  
  
 Di conseguenza, i clienti che usano le API di WF 3 deprecate riceveranno avvisi di compilazione con un messaggio simile al seguente:  
  
  **Avviso BC40000: X è obsoleto. I tipi in WF 3 sono deprecati.  Usare WF 4.**  I tipi verranno rimossi da .NET Framework in una versione futura, ma non è stato ancora determinato l'arco di tempo \(non in 4.5\).  L'attuale passaggio intende comunicare la direttiva ai clienti concedendo loro il tempo sufficiente per passare al nuovo modello WF4.  Naturalmente, i tipi in WF 3 continueranno ad essere supportati secondo i [criteri di supporto per il ciclo di vita Microsoft](http://aka.ms/MicrosoftSupportLifecycle).  Le applicazioni in WF3 esistenti verranno eseguite senza problemi in .NET 4.5 e [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] supporterà le nuove e soluzioni esistenti basate su WF3.  
  
 I tipi relativi alle regole nello spazio dei nomi <xref:System.Workflow.Activities.Rules>, che non hanno una sostituzione in WF 4.5, non sono stati deprecati.  
  
 I clienti che vogliono eseguire la migrazione delle applicazioni a WF 4 possono trovare le informazioni negli articoli [Istruzione di migrazione del flusso di lavoro 4](http://aka.ms/WF4MigrationGuidance) in MSDN e nel [Kit di migrazione di WF 4](http://aka.ms/WF4MigrationKit) disponibile nel sito [WF Codeplex](http://aka.ms/WFCodeplex).