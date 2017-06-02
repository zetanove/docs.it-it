---
title: "Procedura: effettuare chiamate thread-safe a controlli di Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "EHInvalidOperation.WinForms.IllegalCrossThreadCall"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "thread safety, chiamata di controlli [Windows Form]"
  - "chiamata di controlli, thread safety [Windows Form]"
  - "CheckForIllegalCrossThreadCalls (proprietà) [Windows Form]"
  - "Controlli Windows Form, multithreading"
  - "Classe BackgroundWorker, esempi"
  - "threading [Windows Form], chiamata tra thread"
  - "controlli [Windows Form], multithreading"
ms.assetid: 138f38b6-1099-4fd5-910c-390b41cbad35
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: effettuare chiamate thread-safe a controlli di Windows Form
Se si usa il multithreading per migliorare le prestazioni delle applicazioni Windows Forms, è necessario assicurarsi che sia possibile effettuare chiamate ai controlli in modo thread\-safe.  
  
 L'accesso ai controlli Windows Form non è intrinsecamente thread\-safe. Se si hanno due o più thread che gestiscono lo stato di un controllo, è possibile forzare il controllo in uno stato incoerente. Altri bug relativi ai thread sono possibili, ad esempio race condition e deadlock. È importante assicurarsi che l'accesso ai controlli venga eseguito in modo thread\-safe.  
  
 Non è sicuro chiamare un controllo da un thread diverso da quello che ha creato il controllo senza usare il metodo <xref:System.Windows.Forms.Control.Invoke%2A>. Di seguito è riportato un esempio di una chiamata non thread\-safe.  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#6)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#6)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#6)]  
  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] consente di rilevare l'accesso ai controlli in modo non thread\-safe. Quando si esegue l'applicazione nel debugger e un thread diverso da quello che ha creato un controllo prova a chiamare il controllo, il debugger genera un' eccezione <xref:System.InvalidOperationException> con il messaggio "È stato eseguito l'accesso al controllo *nome controllo* da un thread diverso da quello da cui è stata eseguita la creazione".  
  
 Questa eccezione si verifica in modo affidabile durante il debug e, in alcune circostanze, in fase di esecuzione. Questa eccezione potrebbe verificarsi quando si esegue il debug di applicazioni scritte con [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] prima di [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]. È consigliabile risolvere questo problema non appena si presenta, ma è possibile prevenirlo impostando la proprietà <xref:System.Windows.Forms.Control.CheckForIllegalCrossThreadCalls%2A> su `false`. In questo modo il controllo viene eseguito come in Visual Studio .NET 2003 e [!INCLUDE[net_v11_short](../../../../includes/net-v11-short-md.md)].  
  
> [!NOTE]
>  Se si usano controlli ActiveX in un form, è possibile che venga visualizzato il <xref:System.InvalidOperationException> cross\-thread quando si esegue il debugger. In questo caso, il controllo ActiveX non supporta operazioni multithread. Per altre informazioni sull'uso dei controlli ActiveX con Windows Form, vedere [Windows Forms and Unmanaged Applications](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md). Se si usa Visual Studio, è possibile impedire questa eccezione disattivando il processo di hosting di Visual Studio. A tale scopo, vedere [Procedura: disabilitare il processo di hosting](../Topic/How%20to:%20Disable%20the%20Hosting%20Process.md).  
  
## Effettuare chiamate thread\-safe a controlli di Windows Form  
  
#### Per effettuare chiamate thread\-safe a un controllo di Windows Form  
  
1.  Eseguire una query sulla proprietà <xref:System.Windows.Forms.Control.InvokeRequired%2A> del controllo.  
  
2.  Se <xref:System.Windows.Forms.Control.InvokeRequired%2A> restituisce `true`, chiamare <xref:System.Windows.Forms.Control.Invoke%2A> con un delegato che effettui la chiamata effettiva al controllo.  
  
3.  Se <xref:System.Windows.Forms.Control.InvokeRequired%2A> restituisce `false`, chiamare direttamente il controllo.  
  
 Nell'esempio di codice seguente, una chiamata thread\-safe è implementata nel metodo `ThreadProcSafe`, che viene eseguito dal thread in background. Se la proprietà <xref:System.Windows.Forms.TextBox> del controllo <xref:System.Windows.Forms.Control.InvokeRequired%2A> restituisce `true`, il metodo `ThreadProcSafe` crea un'istanza di `SetTextCallback` e la passa al metodo <xref:System.Windows.Forms.Control.Invoke%2A> del form. In questo modo la chiamata al metodo `SetText` viene eseguita sul thread che ha creato il controllo <xref:System.Windows.Forms.TextBox> e la proprietà <xref:System.Windows.Forms.Control.Text%2A> viene impostata direttamente in questo contesto di thread.  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#7](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#7)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#7)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#7)]  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#3](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#3)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#3)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#3)]  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#8](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#8)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#8](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#8)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#8](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#8)]  
  
## Chiamate Thread\-Safe con BackgroundWorker  
 Il metodo migliore per implementare il multithreading nell'applicazione è usare il componente <xref:System.ComponentModel.BackgroundWorker>, Il componente <xref:System.ComponentModel.BackgroundWorker> usa un modello basato sugli eventi per il multithreading. Il thread in background esegue il gestore dell'evento <xref:System.ComponentModel.BackgroundWorker.DoWork> e il thread che crea i controlli esegue i gestori degli eventi <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> e <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>. È possibile chiamare i controlli dai gestore degli eventi <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> e <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>.  
  
#### Per effettuare chiamate thread\-safe con BackgroundWorker  
  
1.  Creare un metodo che esegua le operazioni desiderate nel thread in background. Non chiamare controlli creati dal thread principale in questo metodo.  
  
2.  Creare un metodo che riporti i risultati delle operazioni in background dopo il loro completamento. È possibile chiamare controlli creati dal thread principale in questo metodo.  
  
3.  Associare il metodo creato nel passaggio 1 all'evento <xref:System.ComponentModel.BackgroundWorker.DoWork> di un'istanza di <xref:System.ComponentModel.BackgroundWorker> e associare il metodo creato nel passaggio 2 all'evento <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> della stessa istanza.  
  
4.  Per avviare il thread in background, chiamare il metodo <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> dell'istanza <xref:System.ComponentModel.BackgroundWorker>.  
  
 Nell'esempio di codice seguente, il gestore eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> usa <xref:System.Threading.Thread.Sleep%2A> per simulare operazioni che richiedono un certo tempo. Non chiama il controllo <xref:System.Windows.Forms.TextBox> del form. La proprietà <xref:System.Windows.Forms.TextBox> del controllo <xref:System.Windows.Forms.Control.Text%2A> viene impostata direttamente nel gestore dell'evento <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>.  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#5)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#5)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#5)]  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#9](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#9)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#9)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#9)]  
  
 È possibile segnalare anche lo stato di avanzamento di un'attività in background con l'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>. Per un esempio che incorpori questo evento, vedere <xref:System.ComponentModel.BackgroundWorker>.  
  
## Esempio  
 L'esempio di codice seguente è un'applicazione Windows Form completa, costituita da un form con tre pulsanti e una casella di testo. Il primo pulsante dimostra un accesso cross\-thread non sicuro, il secondo pulsante dimostra un accesso sicuro con <xref:System.Windows.Forms.Control.Invoke%2A> e il terzo pulsante dimostra un accesso sicuro con <xref:System.ComponentModel.BackgroundWorker>.  
  
> [!NOTE]
>  Per istruzioni su come eseguire l'esempio, vedere [How to: Compile and Run a Complete Windows Forms Code Example Using Visual Studio](http://msdn.microsoft.com/it-it/cc447f7e-4c3b-4397-9d05-aeba3ca49416). Questo esempio richiede riferimenti agli assembly System.Drawing e System.Windows.Forms.  
  
 [!code-cpp[System.Windows.Forms.CrossThreadCalls#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/cpp/Form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.CrossThreadCalls#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.CrossThreadCalls#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CrossThreadCalls/VB/Form1.vb#1)]  
  
 Quando si esegue l'applicazione e si fa clic sul pulsante **Unsafe Call**, viene immediatamente visualizzato "Written by the main thread" nella casella di testo. Due secondi dopo, quando viene tentata la chiamata non sicura, il debugger di Visual Studio indica che si è verificata un'eccezione. Il debugger si arresta alla riga nel thread in background che ha provato a scrivere direttamente nella casella di testo. Sarà necessario riavviare l'applicazione per testare gli altri due pulsanti. Quando si fa clic sul pulsante **Safe Call**, viene visualizzato "Written by the main thread" nella casella di testo. Due secondi dopo, la casella di testo viene impostata su "Written by the background thread \(Invoke\)", che indica che è stato chiamato il metodo <xref:System.Windows.Forms.Control.Invoke%2A>. Quando si fa clic sul pulsante **Safe BW Call**, viene visualizzato "Written by the main thread" nella casella di testo. Due secondi dopo, la casella di testo viene impostata su "Written by the main thread after the background thread completed", a indicare che è stato chiamato il gestore per l'evento <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> di <xref:System.ComponentModel.BackgroundWorker>.  
  
## Programmazione efficiente  
  
> [!CAUTION]
>  Quando si usa qualsiasi tipo di multithreading, è possibile che il codice venga esposto al rischio di bug gravi e complessi. Per altre informazioni, vedere [Managed Threading Best Practices](../../../../docs/standard/threading/managed-threading-best-practices.md) prima di implementare soluzioni che usano il multithreading.  
  
## Vedere anche  
 <xref:System.ComponentModel.BackgroundWorker>   
 [Procedura: eseguire un'operazione in background](../../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Procedura: implementare un form che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [Sviluppo di controlli Windows Form personalizzati con .NET Framework](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [Windows Forms and Unmanaged Applications](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)