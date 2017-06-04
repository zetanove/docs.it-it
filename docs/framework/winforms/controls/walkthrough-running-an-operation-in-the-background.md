---
title: "Procedura dettagliata: esecuzione di un&#39;operazione in background | Microsoft Docs"
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
  - "operazioni in background"
  - "attività in background"
  - "thread in background"
  - "BackgroundWorker (classe), esempi"
  - "form, operazioni in background"
  - "form, multithreading"
  - "threading [Windows Form], operazioni in background"
ms.assetid: 1b9a4e0a-f134-48ff-a1be-c461446a31ba
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura dettagliata: esecuzione di un&#39;operazione in background
Se l'esecuzione di un'operazione richiede molto tempo e si desidera evitare ritardi nella risposta dell'interfaccia utente, è possibile utilizzare la classe <xref:System.ComponentModel.BackgroundWorker> per eseguire l'operazione in un altro thread.  
  
 Per il listato completo del codice utilizzato in questo esempio, vedere [Procedura: eseguire un'operazione in background](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per eseguire un'operazione in background  
  
1.  Trascinare due controlli <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** al form attivo in Progettazione Windows Form, quindi impostare le proprietà `Name` e <xref:System.Windows.Forms.Control.Text%2A> dei pulsanti secondo i valori indicati nella tabella seguente.  
  
    |Button|Nome|Text|  
    |------------|----------|----------|  
    |`button1`|`startBtn`|Start|  
    |`button2`|`cancelBtn`|Cancel|  
  
2.  Aprire la **Casella degli strumenti**, fare clic sulla scheda **Componenti** e trascinare il componente <xref:System.ComponentModel.BackgroundWorker> nel form.  
  
     Il componente `backgroundWorker1` verrà visualizzato nella **Barra dei componenti**.  
  
3.  Nella finestra **Proprietà** impostare la proprietà <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> su `true`.  
  
4.  Fare clic sul pulsante **Eventi** nella finestra **Proprietà**, quindi fare doppio clic sugli eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> e <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> per creare i gestori eventi.  
  
5.  Inserire codice particolarmente complesso nel gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork>.  
  
6.  Estrarre tutti i parametri richiesti per l'operazione dalla proprietà <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A> del parametro <xref:System.ComponentModel.DoWorkEventArgs>.  
  
7.  Assegnare il risultato del calcolo alla proprietà <xref:System.ComponentModel.DoWorkEventArgs.Result%2A> della classe <xref:System.ComponentModel.DoWorkEventArgs>.  
  
     Il risultato sarà disponibile al gestore eventi <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>.  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#2)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#2)]  
  
8.  Inserire il codice per recuperare il risultato dell'operazione nel gestore eventi <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>.  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#3)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#3)]  
  
9. Implementare il metodo `TimeConsumingOperation`.  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#4)]  
  
10. In Progettazione Windows Form fare doppio clic su `startButton` per creare il gestore eventi <xref:System.Windows.Forms.Control.Click>.  
  
11. Chiamare il metodo <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> nel gestore eventi <xref:System.Windows.Forms.Control.Click> per `startButton`.  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#5)]  
  
12. In Progettazione Windows Form fare doppio clic su `cancelButton` per creare il gestore eventi <xref:System.Windows.Forms.Control.Click>.  
  
13. Chiamare il metodo <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> nel gestore eventi <xref:System.Windows.Forms.Control.Click> per `cancelButton`.  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#6)]  
  
14. All'inizio del file, importare gli spazi dei nomi System.ComponentModel e System.Threading.  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#7)]  
  
15. Premere F6 per compilare la soluzione, quindi premere CTRL\-F5 per eseguire l'applicazione al di fuori del debugger.  
  
> [!NOTE]
>  Se si preme F5 per eseguire l'applicazione all'interno del debugger, l'eccezione generata nel metodo `TimeConsumingOperation` verrà rilevata e visualizzata dal debugger.  Quando si esegue l'applicazione al di fuori del debugger, <xref:System.ComponentModel.BackgroundWorker> gestisce l'eccezione e la memorizza in cache nella proprietà <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A> della classe <xref:System.ComponentModel.RunWorkerCompletedEventArgs>.  
  
1.  Fare clic sul pulsante **Start** per eseguire un'operazione asincrona, quindi fare clic sul pulsante **Annulla** per interrompere l'esecuzione.  
  
     Il risultato di ciascuna operazione viene visualizzato in una finestra di messaggio <xref:System.Windows.Forms.MessageBox>.  
  
## Passaggi successivi  
  
-   Implementare un form in cui venga indicato lo stato di avanzamento di un'operazione asincrona.  Per ulteriori informazioni, vedere [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md).  
  
-   Implementare una classe che supporta il modello asincrono per componenti.  Per ulteriori informazioni, vedere [Implementing the Event\-based Asynchronous Pattern](../../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md).  
  
## Vedere anche  
 <xref:System.ComponentModel.BackgroundWorker>   
 <xref:System.ComponentModel.DoWorkEventArgs>   
 [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [Procedura: eseguire un'operazione in background](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Componente BackgroundWorker](../../../../docs/framework/winforms/controls/backgroundworker-component.md)