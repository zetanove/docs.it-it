---
title: "Procedura dettagliata: implementazione di un form che utilizza un&#39;operazione in background | Microsoft Docs"
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
  - "BackgroundWorker (componente)"
  - "form, operazioni in background"
  - "form, multithreading"
  - "threading [Windows Form], operazioni in background"
  - "threading [Windows Form], form"
  - "threading [Windows Form], procedure dettagliate"
ms.assetid: 4691b796-9200-471a-89c3-ba4c7cc78c03
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# Procedura dettagliata: implementazione di un form che utilizza un&#39;operazione in background
Per evitare che l'interfaccia utente \(UI, User Interface\) si blocchi o risponda in ritardo a causa di un'operazione che impiega molto tempo per essere completata, è possibile utilizzare la classe <xref:System.ComponentModel.BackgroundWorker> per eseguire l'operazione in un altro thread.  
  
 In questa procedura dettagliata viene descritto come usare la classe <xref:System.ComponentModel.BackgroundWorker> per eseguire "in background" i calcoli dispendiosi in termini di tempo lasciando inalterata la capacità di risposta dell'interfaccia utente.  Nel corso della procedura, un'applicazione calcola i numeri Fibonacci in modo asincrono.  Sebbene il calcolo di un numero Fibonacci a molte cifre possa impiegare una notevole quantità di tempo, il thread principale della UI non verrà interrotto da questa operazione e la capacità di risposta del form resterà inalterata durante il calcolo.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione di un'applicazione basata su Windows  
  
-   Creazione di <xref:System.ComponentModel.BackgroundWorker> nel form  
  
-   Aggiunta dei gestori eventi asincroni  
  
-   Aggiunta dei report sullo stato di avanzamento e supporto per l'annullamento  
  
 Per il listato completo del codice utilizzato in questo esempio, vedere [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Il primo passaggio indica come creare il progetto e impostare il form.  
  
#### Per creare un form che utilizza un'operazione in background  
  
1.  Creare un progetto di applicazione basata su Windows chiamato `BackgroundWorkerExample`.  Per informazioni dettagliate, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Form1** e scegliere **Rinomina** dal menu di scelta rapida.  Modificare il nome file in `FibonacciCalculator`.  Scegliere il pulsante **Sì** quando richiesto per rinominare tutti i riferimenti all'elemento di codice '`Form1`'.  
  
3.  Trascinare un controllo <xref:System.Windows.Forms.NumericUpDown> dalla **Casella degli strumenti** nel form.  Impostare la proprietà <xref:System.Windows.Forms.NumericUpDown.Minimum%2A> su `1` e la proprietà <xref:System.Windows.Forms.NumericUpDown.Maximum%2A> su `91`.  
  
4.  Aggiungere due controlli <xref:System.Windows.Forms.Button> nel form.  
  
5.  Rinominare il primo controllo <xref:System.Windows.Forms.Button> in `startAsyncButton` e impostare la proprietà <xref:System.Windows.Forms.Control.Text%2A> su `Start Async`.  Rinominare il secondo controllo <xref:System.Windows.Forms.Button> in `cancelAsyncButton` e impostare la proprietà <xref:System.Windows.Forms.Control.Text%2A> su `Cancel Async`.  Impostarne la proprietà <xref:System.Windows.Forms.Control.Enabled%2A> su `false`.  
  
6.  Creare un gestore per entrambi gli eventi <xref:System.Windows.Forms.Control.Click> del controllo <xref:System.Windows.Forms.Button>.  Per informazioni dettagliate, vedere [How to: Create Event Handlers Using the Designer](http://msdn.microsoft.com/it-it/8461e9b8-14e8-406f-936e-3726732b23d2).  
  
7.  Trascinare un controllo <xref:System.Windows.Forms.Label> dalla **Casella degli strumenti** nel form e rinominarlo `resultLabel`.  
  
8.  Trascinare un controllo <xref:System.Windows.Forms.ProgressBar> dalla **Casella degli strumenti** nel form.  
  
## Creazione di un BackgroundWorker nel form  
 È possibile creare il <xref:System.ComponentModel.BackgroundWorker> per l'operazione asincrona utilizzando **Progettazione** **Windows Form**.  
  
#### Per creare un BackgroundWorker con la finestra di progettazione  
  
-   Dalla scheda **Componenti** della **Casella degli strumenti** trascinare un componente <xref:System.ComponentModel.BackgroundWorker> nel form.  
  
## Aggiunta dei gestori eventi asincroni  
 A questo punto è possibile aggiungere i gestori per gli eventi asincroni del componente <xref:System.ComponentModel.BackgroundWorker>.  L'operazione dispendiosa in termini di tempo che verrà eseguita in background, ossia quella che calcola i numeri Fibonacci, viene chiamata da uno di questi gestori eventi.  
  
#### Per implementare i gestori eventi asincroni  
  
1.  Nella finestra **Proprietà**, con il componente <xref:System.ComponentModel.BackgroundWorker> ancora selezionato, fare clic sul pulsante **Eventi**.  Per creare i gestori eventi, fare doppio clic sugli eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> e <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>.  Per ulteriori informazioni sulle modalità di utilizzo dei gestori dell’evento, vedere [How to: Create Event Handlers Using the Designer](http://msdn.microsoft.com/it-it/8461e9b8-14e8-406f-936e-3726732b23d2).  
  
2.  Creare nel form un nuovo metodo denominato `ComputeFibonacci`.  L'operazione verrà effettivamente svolta da questo metodo che verrà eseguito in background.  Il codice dimostra l'implementazione ricorsiva dell'algoritmo Fibonacci che è decisamente inefficiente e esponenzialmente impiega più tempo per completare i numeri a molte cifre.  Viene impiegato per dimostrare come un'operazione possa provocare lunghi ritardi nell'applicazione.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#10)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#10)]
     [!code-vb[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#10)]  
  
3.  Nel gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> aggiungere una chiamata al metodo `ComputeFibonacci`.  Richiamare il primo parametro per `ComputeFibonacci` dalla proprietà <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A> di <xref:System.ComponentModel.DoWorkEventArgs>.  I parametri <xref:System.ComponentModel.BackgroundWorker> e <xref:System.ComponentModel.DoWorkEventArgs> verranno utilizzati in seguito per i report sullo stato di avanzamento e il supporto per l'annullamento.  Assegnare il valore restituito da `ComputeFibonacci` alla proprietà <xref:System.ComponentModel.DoWorkEventArgs.Result%2A> di <xref:System.ComponentModel.DoWorkEventArgs>.  Il risultato sarà disponibile al gestore dell'evento <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>.  
  
    > [!NOTE]
    >  È importante che il gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> non faccia direttamente riferimento alla variabile dell'istanza `backgroundWorker1`. In caso contrario il gestore eventi verrebbe associato a un'istanza specifica di <xref:System.ComponentModel.BackgroundWorker>.  Il riferimento al <xref:System.ComponentModel.BackgroundWorker> che ha generato l'evento viene invece recuperato dal parametro `sender`.  Ciò è importante quando il form include più di un <xref:System.ComponentModel.BackgroundWorker>.  È altrettanto importante evitare di modificare oggetti dell'interfaccia utente nel gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork>.  Comunicare invece con l'interfaccia utente tramite gli eventi <xref:System.ComponentModel.BackgroundWorker>.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#5)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#5)]  
  
4.  Nel gestore eventi <xref:System.Windows.Forms.Control.Click> del controllo `startAsyncButton`, aggiungere il codice che avvia l'operazione asincrona.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#13)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#13)]
     [!code-vb[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#13)]  
  
5.  Nel gestore eventi <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>, assegnare il risultato del calcolo al controllo `resultLabel`.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#6)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#6)]  
  
## Aggiunta dei report sullo stato di avanzamento e supporto per l'annullamento  
 Per le operazioni asincrone che impiegano molto tempo è spesso opportuno notificare all'utente lo stato di avanzamento e permettegli di annullare eventualmente l'operazione.  La classe <xref:System.ComponentModel.BackgroundWorker> fornisce un evento che consente di inviare lo stato mentre l'operazione procede in background.  Fornisce inoltre un flag che consente al codice di rilevare una chiamata a <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> e interrompersi.  
  
#### Per implementare i report sullo stato di avanzamento  
  
1.  Nella finestra **Proprietà** selezionare `backgroundWorker1`.  Impostare le proprietà <xref:System.ComponentModel.BackgroundWorker.WorkerReportsProgress%2A> e <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> su `true`.  
  
2.  Nel form `FibonacciCalculator` dichiarare due variabili  che verranno utilizzate per tenere traccia dello stato di avanzamento.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#14)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#14)]
     [!code-vb[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#14)]  
  
3.  Aggiunge un gestore eventi per l'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>.  Nel gestore dell'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> aggiornare <xref:System.Windows.Forms.ProgressBar> con la proprietà <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> del parametro <xref:System.ComponentModel.ProgressChangedEventArgs>.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#7)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#7)]  
  
#### Per implementare il supporto per l'annullamento  
  
1.  Nel gestore dell'evento <xref:System.Windows.Forms.Control.Click> del controllo `cancelAsyncButton`, aggiungere il codice per annullare l'operazione asincrona.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#4)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#4)]  
  
2.  I seguenti frammenti di codice nel metodo `ComputeFibonacci` restituiscono lo stato di avanzamento e supportano l'annullamento.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#11)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#11)]
     [!code-vb[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#11)]  
    [!code-cpp[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#12)]
    [!code-csharp[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#12)]
    [!code-vb[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#12)]  
  
## Verifica  
 A questo punto è possibile compilare ed eseguire l'applicazione Fibonacci Calculator.  
  
#### Per verificare il progetto  
  
-   Premere F5 per compilare ed eseguire l'applicazione.  
  
     Durante l'esecuzione del calcolo in background, la <xref:System.Windows.Forms.ProgressBar> visualizzerà lo stato di avanzamento del calcolo in relazione alla completamento.  È anche possibile annullare l'operazione in sospeso.  
  
     Per i numeri con poche cifre, il calcolo dovrebbe essere molto rapido, ma per i numeri con tante cifre, si potrebbe notare un considerevole ritardo.  Se si immette il valore 30 o superiore, il ritardo sarà di diversi secondi, a seconda della velocità del computer.  Per i valori maggiori di 40, potrebbero essere necessari diversi minuti o ore per terminare il calcolo.  Mentre il calcolatore è impegnato a calcolare un numero Fibonacci con tante cifre, il form può essere spostato liberamente, ridotto a icona, ingrandito e persino chiuso  in quanto il thread principale della UI non è in attesa della fine del calcolo.  
  
## Passaggi successivi  
 Una volta implementato un form che utilizza un componente <xref:System.ComponentModel.BackgroundWorker> per eseguire un calcolo in background, si possono sperimentare altre possibilità per le operazioni asincrone.  
  
-   Utilizzare più oggetti <xref:System.ComponentModel.BackgroundWorker> per diverse operazioni simultanee.  
  
-   Per eseguire il debug dell'applicazione con multithreading, vedere [Procedura: utilizzare la finestra Thread](../Topic/How%20to:%20Use%20the%20Threads%20Window.md).  
  
-   Implementare il componente che supporta il modello di programmazione asincrona.  Per ulteriori informazioni, vedere [Event\-based Asynchronous Pattern Overview](../../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md).  
  
    > [!CAUTION]
    >  Quando si utilizza il multithreading, si è potenzialmente esposti al rischio di bug molto seri e complicati.  Consultare [Managed Threading Best Practices](../../../../docs/standard/threading/managed-threading-best-practices.md) prima di implementare soluzioni che utilizzano il multithreading.  
  
## Vedere anche  
 <xref:System.ComponentModel.BackgroundWorker>   
 [Managed Threading Best Practices](../../../../docs/standard/threading/managed-threading-best-practices.md)   
 [Multithreading in Components](../Topic/Multithreading%20in%20Components.md)   
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/it-it/c731a50c-09c1-4468-9646-54c86b75d269)   
 [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [Procedura dettagliata: esecuzione di un'operazione in background](../../../../docs/framework/winforms/controls/walkthrough-running-an-operation-in-the-background.md)   
 [Componente BackgroundWorker](../../../../docs/framework/winforms/controls/backgroundworker-component.md)