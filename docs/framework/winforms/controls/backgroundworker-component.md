---
title: "Componente BackgroundWorker | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Modello asincrono"
  - "operazioni in background"
  - "attività in background"
  - "BackgroundWorker (componente)"
  - "componenti [Windows Form], asincrono"
  - "form, operazioni in background"
  - "form, multithreading"
  - "threading [Windows Form], operazioni in background"
ms.assetid: bef7b0ab-ce57-475a-a2d6-fb8a702a9417
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Componente BackgroundWorker
Il componente `BackgroundWorker` consente a un form o a un controllo di eseguire un'operazione in modo asincrono.  
  
## In questa sezione  
 [Cenni preliminari sul componente BackgroundWorker](../../../../docs/framework/winforms/controls/backgroundworker-component-overview.md)  
 Viene illustrato il componente `BackgroundWorker`, il quale offre la possibilità di eseguire operazioni lunghe ed elaborate in modo asincrono \(in background\) su un thread diverso da quello utilizzato dall'interfaccia utente principale dell'applicazione.  
  
 [Procedura dettagliata: esecuzione di un'operazione in background](../../../../docs/framework/winforms/controls/walkthrough-running-an-operation-in-the-background.md)  
 Viene illustrato come utilizzare il componente `BackgroundWorker` nella finestra di progettazione per eseguire un'operazione lunga ed elaborata su un thread separato.  
  
 [Procedura: eseguire un'operazione in background](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)  
 Viene illustrato come utilizzare il componente `BackgroundWorker` per eseguire un'operazione lunga ed elaborata su un thread separato.  
  
 [Procedura dettagliata: implementazione di un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/walkthrough-implementing-a-form-that-uses-a-background-operation.md)  
 Viene creata un'applicazione mediante la finestra di progettazione che consente di eseguire calcoli matematici in modo asincrono.  
  
 [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)  
 Viene creata un'applicazione che consente di eseguire calcoli matematici in modo asincrono.  
  
 [Procedura: scaricare file in background](../../../../docs/framework/winforms/controls/how-to-download-a-file-in-the-background.md)  
 Viene illustrato come utilizzare il componente `BackgroundWorker` per eseguire il download di un file su un thread separato.  
  
## Riferimenti  
 <xref:System.ComponentModel.BackgroundWorker>  
 Viene descritta la classe e forniti i collegamenti a tutti i relativi membri.  
  
 <xref:System.ComponentModel.RunWorkerCompletedEventArgs>  
 Viene descritto il tipo che contiene i dati per l'evento <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>.  
  
 <xref:System.ComponentModel.ProgressChangedEventArgs>  
 Viene descritto il tipo che contiene i dati per l'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>.  
  
## Sezioni correlate  
 [Event\-based Asynchronous Pattern Overview](../../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)  
 Viene illustrato il modo in cui il modello asincrono consente di usufruire dei vantaggi offerti dalle applicazioni multithreading nascondendo nel contempo gran parte degli aspetti complessi inerenti la progettazione multithreading.