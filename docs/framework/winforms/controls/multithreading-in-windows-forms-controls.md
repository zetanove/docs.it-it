---
title: "Multithreading nei controlli Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "BackgroundWorker (componente)"
  - "BeginInvoke (metodo)"
  - "threading [Windows Form], controlli"
ms.assetid: c311d652-0f26-45fa-bdcc-b1615d73ce4e
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Multithreading nei controlli Windows Form
In molte applicazioni è possibile migliorare i tempi di risposta dell'interfaccia utente eseguendo operazioni lunghe ed elaborate su un altro thread.  Per il multithreading dei controlli Windows Form sono disponibili diversi strumenti, tra cui lo spazio dei nomi <xref:System.Threading>, il metodo <xref:System.Windows.Forms.Control.BeginInvoke%2A?displayProperty=fullName> e il componente `BackgroundWorker`.  
  
> [!NOTE]
>  Benché il componente `BackgroundWorker` sostituisca lo spazio dei nomi <xref:System.Threading> e il metodo <xref:System.Windows.Forms.Control.BeginInvoke%2A?displayProperty=fullName> aggiungendo funzionalità, questi ultimi vengono mantenuti per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  Per ulteriori informazioni, vedere [Cenni preliminari sul componente BackgroundWorker](../../../../docs/framework/winforms/controls/backgroundworker-component-overview.md).  
  
## In questa sezione  
 [Procedura: effettuare chiamate thread\-safe a controlli di Windows Form](../../../../docs/framework/winforms/controls/how-to-make-thread-safe-calls-to-windows-forms-controls.md)  
 Viene illustrato come effettuare chiamate thread\-safe a controlli Windows Form.  
  
 [Procedura: utilizzare un thread in background per la ricerca di file](../../../../docs/framework/winforms/controls/how-to-use-a-background-thread-to-search-for-files.md)  
 Viene illustrato come utilizzare lo spazio dei nomi <xref:System.Threading> e il metodo <xref:System.Windows.Forms.Control.BeginInvoke%2A> per ricercare file in modo asincrono.  
  
## Riferimenti  
 <xref:System.ComponentModel.BackgroundWorker>  
 Vengono fornite informazioni su un componente che incapsula un thread di lavoro per operazioni asincrone.  
  
 <xref:System.Media.SoundPlayer.LoadAsync%2A>  
 Viene illustrato come caricare un suono in modo asincrono.  
  
 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A>  
 Viene illustrato come caricare un'immagine in modo asincrono.  
  
## Sezioni correlate  
 [Procedura: eseguire un'operazione in background](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)  
 Viene illustrato come eseguire un'operazione lunga ed elaborata con il componente <xref:System.ComponentModel.BackgroundWorker>.  
  
 [Cenni preliminari sul componente BackgroundWorker](../../../../docs/framework/winforms/controls/backgroundworker-component-overview.md)  
 Vengono forniti argomenti in cui è illustrato come utilizzare il componente <xref:System.ComponentModel.BackgroundWorker> per operazioni asincrone.