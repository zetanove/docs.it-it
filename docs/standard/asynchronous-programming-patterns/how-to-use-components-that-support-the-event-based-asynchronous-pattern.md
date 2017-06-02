---
title: "How to: Use Components That Support the Event-based Asynchronous Pattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Event-based Asynchronous Pattern"
  - "ProgressChangedEventArgs class"
  - "BackgroundWorker component"
  - "events [.NET Framework], asynchronous"
  - "Asynchronous Pattern"
  - "AsyncOperationManager class"
  - "threading [.NET Framework], asynchronous features"
  - "components [.NET Framework], asynchronous"
  - "AsyncOperation class"
  - "threading [Windows Forms], asynchronous features"
  - "AsyncCompletedEventArgs class"
ms.assetid: 35e9549c-1568-4768-ad07-17cc6dff11e1
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# How to: Use Components That Support the Event-based Asynchronous Pattern
Diversi componenti consentono di eseguire le attività a essi associate in modo asincrono.  I componenti <xref:System.Media.SoundPlayer> e <xref:System.Windows.Forms.PictureBox>, ad esempio, consentono di caricare suoni e immagini in background mentre l'esecuzione del thread principale procede senza interruzioni.  
  
 Per utilizzare metodi asincroni su una classe che supporta [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md), operazione che può risultare semplice quanto il collegamento del gestore eventi all'evento *MethodName*`Completed` del componente, seguire la procedura utilizzata per qualsiasi altro evento.  Quando si chiama il metodo *MethodName*`Async`, l'esecuzione dell'applicazione continua senza interruzioni fino alla generazione dell'evento *MethodName*`Completed`.  Nel gestore eventi specifico è possibile esaminare il parametro <xref:System.ComponentModel.AsyncCompletedEventArgs> per determinare se l'operazione asincrona è stata completata o annullata.  
  
 Per ulteriori informazioni sull'utilizzo di gestori eventi, vedere [Event Handlers Overview](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md).  
  
 Nella procedura riportata di seguito viene illustrata la funzionalità asincrona di caricamento dell'immagine di un controllo <xref:System.Windows.Forms.PictureBox>.  
  
### Per consentire il caricamento asincrono di un'immagine a un controllo PictureBox  
  
1.  Creare un'istanza del componente <xref:System.Windows.Forms.PictureBox> nel form.  
  
2.  Assegnare un gestore eventi all'evento <xref:System.Windows.Forms.PictureBox.LoadCompleted>.  
  
     Verificare in questa posizione la presenza di errori che si potrebbero verificare nel corso del download asincrono.  In questa posizione viene eseguita anche la verifica dell'annullamento dell'operazione.  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#2)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#5)]  
  
3.  Aggiungere al form due pulsanti, denominati `loadButton` e `cancelLoadButton`.  Aggiungere i gestori eventi <xref:System.Windows.Forms.Control.Click> per avviare e annullare il download.  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.PictureBox.LoadAsync#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.PictureBox.LoadAsync#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.PictureBox.LoadAsync/VB/Form1.vb#4)]  
  
4.  Eseguire l'applicazione.  
  
     Durante il download dell'immagine è possibile spostare liberamente il form, ridurlo a icona e ingrandirlo.  
  
## Vedere anche  
 [Procedura: eseguire un'operazione in background](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)   
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/it-it/c731a50c-09c1-4468-9646-54c86b75d269)