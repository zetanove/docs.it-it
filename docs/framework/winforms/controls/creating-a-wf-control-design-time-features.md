---
title: "Procedura dettagliata: creazione di un controllo di Windows Form che usufruisca delle funzionalit&#224; offerte da Visual Studio in fase di progettazione | Microsoft Docs"
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
  - "funzionalità in fase di progettazione, Windows Form"
  - "DocumentDesigner (classe) [Windows Form]"
  - "procedure dettagliate [Windows Form], controlli"
  - "controlli Windows Form, creazione"
ms.assetid: 6f487c59-cb38-4afa-ad2e-95edacb1d626
caps.latest.revision: 46
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 46
---
# Procedura dettagliata: creazione di un controllo di Windows Form che usufruisca delle funzionalit&#224; offerte da Visual Studio in fase di progettazione
La fase di progettazione di un controllo personalizzato può essere migliorata mediante la creazione di una finestra di progettazione personalizzata associata.  
  
 In questa procedura dettagliata viene illustrato come creare una finestra di progettazione personalizzata per un controllo personalizzato.  Verrà implementato il tipo `MarqueeControl` e la classe di una finestra di progettazione associata denominata `MarqueeControlRootDesigner`.  
  
 Il tipo `MarqueeControl` implementa una visualizzazione simile all'insegna di un teatro con luci animate e testo intermittente.  
  
 La finestra di progettazione per questo controllo interagisce con l'ambiente di progettazione per consentire di personalizzare la fase di progettazione.  Grazie alla finestra di progettazione personalizzata è possibile assemblare un'implementazione di `MarqueeControl` personalizzata con luci animate e testo intermittente in varie combinazioni.  È possibile utilizzare il controllo assemblato in un form come qualsiasi altro controllo di Windows Form.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione del progetto  
  
-   Creazione di un progetto di libreria di controlli  
  
-   Aggiunta di un riferimento al progetto del controllo personalizzato  
  
-   Definizione di un controllo personalizzato e della relativa finestra di progettazione personalizzata  
  
-   Creazione di un'istanza del controllo personalizzato  
  
-   Impostazione del progetto per il debug in fase di progettazione  
  
-   Implementazione del controllo personalizzato  
  
-   Creazione di un controllo figlio per il controllo personalizzato  
  
-   Creazione del controllo figlio di MarqueeBorder  
  
-   Creazione di una finestra di progettazione personalizzata per eseguire lo shadowing e filtrare le proprietà  
  
-   Gestione delle modifiche ai componenti  
  
-   Aggiunta di verbi di progettazione alla finestra di progettazione personalizzata  
  
-   Creazione di un UITypeEditor personalizzato  
  
-   Test del controllo personalizzato nella finestra di progettazione  
  
 Al termine, il controllo personalizzato risulterà simile al seguente:  
  
 ![Possibile disposizione di MarqueeControl](../../../../docs/framework/winforms/controls/media/demomarqueecontrol.gif "DemoMarqueeControl")  
  
 Per l'elenco di codice completo, vedere [How to: Create a Windows Forms Control That Takes Advantage of Design\-Time Features](../Topic/How%20to:%20Create%20a%20Windows%20Forms%20Control%20That%20Takes%20Advantage%20of%20Design-Time%20Features.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Disporre di autorizzazioni sufficienti per creare ed eseguire progetti di applicazioni Windows Form nel computer dove è installato Visual Studio.  
  
## Creazione del progetto  
 Il primo passaggio consiste nella creazione del progetto di applicazione,  che verrà utilizzato per compilare l'applicazione che contiene il controllo personalizzato.  
  
#### Per creare il progetto  
  
-   Creare un progetto di applicazione Windows Form denominato "MarqueeControlTest". Per ulteriori informazioni, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
## Creazione di un progetto di libreria di controlli  
 Il passaggio successivo consiste nella creazione di un progetto di libreria di controlli.  Verrà creato un nuovo controllo personalizzato insieme alla finestra di progettazione personalizzata corrispondente.  
  
#### Per creare il progetto di libreria di controlli  
  
1.  Aggiungere alla soluzione un progetto Libreria di controlli Windows Form.  Denominare il progetto "MarqueeControlLibrary".  
  
2.  In **Esplora soluzioni** eliminare il controllo predefinito del progetto rimuovendo il file di origine "UserControl1.cs" o "UserControl1.vb", a seconda del linguaggio scelto.  Per ulteriori informazioni, vedere [NIB:How to: Remove, Delete, and Exclude Items](http://msdn.microsoft.com/it-it/6dffdc86-29c8-4eff-bcd8-e3a0dd9e9a73).  
  
3.  Aggiungere un nuovo elemento <xref:System.Windows.Forms.UserControl> al progetto `MarqueeControlLibrary`.  Assegnare al nuovo file di origine il nome di base "MarqueeControl".  
  
4.  In **Esplora soluzioni** creare una nuova cartella nel progetto `MarqueeControlLibrary`.  Per ulteriori informazioni, vedere [NIB:How to: Add New Project Items](http://msdn.microsoft.com/it-it/63d3e16b-de6e-4bb5-a0e3-ecec762201ce).  Assegnare il nome "Design" alla nuova cartella.  
  
5.  Fare clic con il pulsante destro del mouse sulla cartella **Design**, quindi aggiungere una nuova classe.  Assegnare al file di origine il nome di base "MarqueeControlRootDesigner".  
  
6.  Sarà necessario utilizzare i tipi dell'assembly System.Design e quindi aggiungere il riferimento al progetto `MarqueeControlLibrary`.  
  
    > [!NOTE]
    >  Per utilizzare l'assembly System.Design, è necessario che per il progetto venga scelta la versione completa di .NET Framework, non .NET Framework Client Profile.  Per modificare il framework di destinazione, vedere [Procedura: destinare una versione di .NET Framework](../Topic/How%20to:%20Target%20a%20Version%20of%20the%20.NET%20Framework.md).  
  
## Aggiunta di un riferimento al progetto del controllo personalizzato  
 Per eseguire il test del controllo personalizzato si utilizzerà il progetto `MarqueeControlTest`.  Il progetto di test riconoscerà il controllo personalizzato quando viene aggiunto un riferimento al progetto nell'assembly `MarqueeControlLibrary`.  
  
#### Per aggiungere un riferimento al progetto del controllo personalizzato  
  
-   Nel progetto `MarqueeControlTest` aggiungere all'assembly `MarqueeControlLibrary` un riferimento al progetto.  Utilizzare la scheda **Progetti** della finestra di dialogo **Aggiungi riferimento** invece di inserire il riferimento direttamente nell'assembly `MarqueeControlLibrary`.  
  
## Definizione di un controllo personalizzato e della relativa finestra di progettazione personalizzata  
 Il controllo personalizzato verrà derivato dalla classe <xref:System.Windows.Forms.UserControl> e potrà quindi contenere altri controlli e utilizzare molte funzionalità predefinite.  
  
 Il controllo personalizzato disporrà di una finestra di progettazione personalizzata associata  che consente di definire il proprio ambiente di progettazione, personalizzandolo appositamente per il controllo personalizzato.  
  
 È possibile associare il controllo alla rispettiva finestra di progettazione utilizzando la classe <xref:System.ComponentModel.DesignerAttribute>.  Poiché si sta sviluppando l'intero comportamento in fase di progettazione del controllo personalizzato, la finestra di progettazione personalizzata implementerà l'interfaccia <xref:System.ComponentModel.Design.IRootDesigner>.  
  
#### Per definire un controllo personalizzato e la relativa finestra di progettazione personalizzata  
  
1.  Aprire il file di origine `MarqueeControl` nell'**editor di codice**.  Importare all'inizio del file i seguenti spazi dei nomi:  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#220](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#220)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#220](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#220)]  
  
2.  Aggiungere <xref:System.ComponentModel.DesignerAttribute> alla dichiarazione della classe `MarqueeControl`,  in modo da associare il controllo personalizzato alla relativa finestra di progettazione.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#240](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#240)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#240](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#240)]  
  
3.  Aprire il file di origine `MarqueeControlRootDesigner` nell'**editor di codice**.  Importare all'inizio del file i seguenti spazi dei nomi:  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#520](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#520)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#520](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#520)]  
  
4.  Modificare la dichiarazione di `MarqueeControlRootDesigner` in modo che erediti dalla classe <xref:System.Windows.Forms.Design.DocumentDesigner>.  Applicare <xref:System.ComponentModel.ToolboxItemFilterAttribute> per specificare l'interazione della finestra di progettazione con la **Casella degli strumenti**.  
  
     **Nota** La definizione per la classe `MarqueeControlRootDesigner` è stata inclusa in uno spazio dei nomi denominato "MarqueeControlLibrary.Design." Questa dichiarazione posiziona la finestra di progettazione in uno spazio dei nomi speciale, riservato ai tipi correlati alla progettazione.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#530](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#530)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#530](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#530)]  
  
5.  Definire il costruttore per la classe `MarqueeControlRootDesigner`.  Inserire nel corpo del costruttore un'istruzione <xref:System.Diagnostics.Trace.WriteLine%2A> che sarà utile ai fini del debug.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#540](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#540)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#540](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#540)]  
  
## Creazione di un'istanza del controllo personalizzato  
 Per osservare il comportamento personalizzato del controllo in fase di progettazione, si inserirà un'istanza del controllo nel form del progetto `MarqueeControlTest`.  
  
#### Per creare un'istanza del controllo personalizzato  
  
1.  Aggiungere un nuovo elemento <xref:System.Windows.Forms.UserControl> al progetto `MarqueeControlTest`.  Assegnare al nuovo file di origine il nome di base "DemoMarqueeControl".  
  
2.  Aprire il file `DemoMarqueeControl` nell'**editor di codice**.  Importare all'inizio del file lo spazio dei nomi `MarqueeControlLibrary`:  
  
```vb  
Imports MarqueeControlLibrary  
```  
  
```csharp  
using MarqueeControlLibrary;  
```  
  
1.  Modificare la dichiarazione di `DemoMarqueeControl` in modo che erediti dalla classe `MarqueeControl`.  
  
2.  Compilare il progetto.  
  
3.  Aprire `Form1` in Progettazione Windows Form.  
  
4.  Trovare la scheda **Componenti MarqueeControlTest** nella **Casella degli strumenti** e quindi aprirla.  Trascinare un `DemoMarqueeControl` dalla **Casella degli strumenti** nel form.  
  
5.  Compilare il progetto.  
  
## Impostazione del progetto per il debug in fase di progettazione  
 Quando si sviluppa una fase di progettazione personalizzata, è necessario eseguire il debug dei controlli e dei componenti.  Esiste un modo semplice per impostare il progetto in modo da consentire il debug in fase di progettazione.  Per ulteriori informazioni, vedere [Procedura dettagliata: debug di controlli di Windows Form personalizzati in fase di progettazione](../../../../docs/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time.md).  
  
#### Per impostare il progetto per il debug in fase di progettazione  
  
1.  Fare clic con il pulsante destro del mouse sul progetto `MarqueeControlLibrary` e scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo "Pagine delle proprietà di MarqueeControlLibrary" selezionare la pagina **Debug**.  
  
3.  Nella sezione **Azione di avvio** selezionare **Avvia programma esterno**.  Verrà eseguito il debug di un'istanza distinta di Visual Studio. A questo scopo fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) per individuare l'IDE di Visual Studio.  Il nome del file eseguibile è devenv.exe e, se è stato installato nel percorso predefinito, il relativo percorso %programfiles%\\Microsoft Visual Studio 9.0\\Common7\\IDE\\devenv.exe.  
  
4.  Scegliere OK per chiudere la finestra di dialogo.  
  
5.  Fare clic con il pulsante destro del mouse sul progetto `MarqueeControlLibrary` e scegliere "Imposta come progetto di avvio" per attivare la configurazione di debug.  
  
## Verifica  
 A questo punto è possibile eseguire il debug del comportamento in fase di progettazione del controllo personalizzato.  Una volta verificato che l'ambiente di debug è stato configurato correttamente, si eseguirà il test dell'associazione tra il controllo personalizzato e la finestra di progettazione personalizzata.  
  
#### Per eseguire il test dell'ambiente di debug e dell'associazione della finestra di progettazione  
  
1.  Aprire il file di origine `MarqueeControlRootDesigner` nell'**editor di codice** e inserire un punto di interruzione nell'istruzione <xref:System.Diagnostics.Trace.WriteLine%2A>.  
  
2.  Premere F5 per avviare la sessione di debug.  Si noti che verrà creata una nuova istanza di Visual Studio.  
  
3.  Aprire la soluzione "MarqueeControlTest" nella nuova istanza di Visual Studio.  È possibile trovare facilmente la soluzione selezionando **Progetti recenti** dal menu **File**.  Il file della soluzione "MarqueeControlTest.sln" corrisponderà al file utilizzato più di recente nell'elenco.  
  
4.  Aprire `DemoMarqueeControl` nella finestra di progettazione.  Si noti che l'istanza di debug di Visual Studio acquisisce lo stato attivo e l'esecuzione si interrompe in corrispondenza del punto di interruzione.  Premere F5 per continuare la sessione di debug.  
  
 A questo punto è possibile sviluppare ed eseguire il debug del controllo personalizzato e della finestra di progettazione personalizzata associata.  Nella parte restante della presente procedura verranno descritti i dettagli per l'implementazione delle funzioni del controllo e della finestra di progettazione.  
  
## Implementazione del controllo personalizzato  
 `MarqueeControl` è un controllo <xref:System.Windows.Forms.UserControl> leggermente personalizzato  che espone due metodi: il metodo `Start` avvia l'animazione e il metodo `Stop` la interrompe.  Poiché `MarqueeControl` contiene controlli figlio che implementano l'interfaccia `IMarqueeWidget`, i metodi `Start` e `Stop` enumerano i controlli figlio e chiamano rispettivamente i metodi `StartMarquee` e `StopMarquee` per ogni controllo figlio che implementa `IMarqueeWidget`.  
  
 L'aspetto dei controlli `MarqueeBorder` e `MarqueeText` dipende dal layout, quindi `MarqueeControl` esegue l'override del metodo <xref:System.Windows.Forms.Control.OnLayout%2A> e chiama <xref:System.Windows.Forms.Control.PerformLayout%2A> per i controlli figlio di questo tipo.  
  
 Quelle descritte sono le possibili personalizzazioni offerte dal controllo `MarqueeControl`.  Le funzioni della fase di esecuzione vengono implementate dai controlli `MarqueeBorder` e `MarqueeText` e le funzioni della fase di progettazione vengono implementate dalle classi `MarqueeBorderDesigner` e `MarqueeControlRootDesigner`.  
  
#### Per implementare il controllo personalizzato  
  
1.  Aprire il file di origine `MarqueeControl` nell'**editor di codice**.  Implementare i metodi `Start` e `Stop`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#260](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#260)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#260](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#260)]  
  
2.  Eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnLayout%2A>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#270](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#270)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#270](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#270)]  
  
## Creazione di un controllo figlio per il controllo personalizzato  
 Il controllo `MarqueeControl` conterrà due tipi di controlli figlio, `MarqueeBorder` e `MarqueeText`.  
  
-   `MarqueeBorder`: questo controllo disegna lungo i bordi una cornice di luci  che lampeggiano in sequenza in modo da creare un effetto di spostamento lungo i bordi.  La frequenza di intermittenza è controllata dalla proprietà `UpdatePeriod`.  Diverse altre proprietà personalizzate determinano ulteriori fattori dell'aspetto del controllo.  L'avvio e l'arresto dell'animazione sono controllati mediante i due metodi `StartMarquee` e `StopMarquee`.  
  
-   `MarqueeText`: questo controllo disegna una stringa lampeggiante.  Come per il controllo `MarqueeBorder`, la frequenza di intermittenza del testo è determinata dalla proprietà `UpdatePeriod`.  Inoltre il controllo `MarqueeText` dispone dei due metodi `StartMarquee` e `StopMarquee` in comune con il controllo `MarqueeBorder`.  
  
 In fase di progettazione, `MarqueeControlRootDesigner` consente di aggiungere questi due tipi di controllo a un `MarqueeControl` in qualsiasi combinazione.  
  
 Poiché le funzioni comuni ai due controlli sono inserite nell'interfaccia `IMarqueeWidget`,  `MarqueeControl` può individuare i controlli figlio correlati al controllo Marquee e comportarsi di conseguenza.  
  
 Per implementare la funzione di animazione periodica, si utilizzeranno gli oggetti <xref:System.ComponentModel.BackgroundWorker> appartenenti allo spazio dei nomi <xref:System.ComponentModel?displayProperty=fullName>.  Sebbene sia possibile utilizzare gli oggetti <xref:System.Windows.Forms.Timer>, in presenza di molti oggetti `IMarqueeWidget`, il singolo thread dell'interfaccia utente potrebbe non essere in grado di gestire l'animazione.  
  
#### Per creare un controllo figlio per il controllo personalizzato  
  
1.  Aggiungere un nuovo elemento class al progetto `MarqueeControlLibrary`.  Assegnare al nuovo file di origine il nome di base "IMarqueeWidget".  
  
2.  Aprire il file di origine `IMarqueeWidget` nell'**editor di codice** e modificare la dichiarazione da `class` a `interface`:  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/imarqueewidget.cs#2)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/imarqueewidget.vb#2)]  
  
3.  Aggiungere il seguente codice all'interfaccia `IMarqueeWidget` per esporre due metodi e una proprietà che gestiscono l'animazione:  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/imarqueewidget.cs#3)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/imarqueewidget.vb#3)]  
  
4.  Aggiungere un nuovo elemento **Controllo personalizzato** al progetto `MarqueeControlLibrary`.  Assegnare al nuovo file di origine il nome di base "MarqueeText".  
  
5.  Trascinare un componente <xref:System.ComponentModel.BackgroundWorker> dalla **Casella degli strumenti** nel controllo `MarqueeText`.  Tale componente consentirà al controllo `MarqueeText` di aggiornarsi in modo asincrono.  
  
6.  Nella finestra Proprietà impostare le proprietà `WorkerReportsProgess` e <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> del componente <xref:System.ComponentModel.BackgroundWorker> su `true`.  Queste impostazioni consentono al componente <xref:System.ComponentModel.BackgroundWorker> di generare periodicamente l'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> e annullare gli aggiornamenti asincroni.  Per ulteriori informazioni, vedere [Componente BackgroundWorker](../../../../docs/framework/winforms/controls/backgroundworker-component.md).  
  
7.  Aprire il file di origine `MarqueeText` nell'**editor di codice**.  Importare all'inizio del file i seguenti spazi dei nomi:  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#120)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#120)]  
  
8.  Modificare la dichiarazione di `MarqueeText` in modo che erediti da <xref:System.Windows.Forms.Label> e implementare l'interfaccia `IMarqueeWidget`:  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#130](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#130)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#130](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#130)]  
  
9. Dichiarare le variabili di istanza che corrispondono alle proprietà esposte e inizializzarle nel costruttore.  Il campo `isLit` determina se il testo deve essere visualizzato nel colore specificato dalla proprietà `LightColor`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#140](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#140)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#140](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#140)]  
  
10. Implementare l'interfaccia `IMarqueeWidget`.  
  
     Per avviare e arrestare l'animazione, i metodi `StartMarquee` e `StopMarquee` richiamano i metodi <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> e <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> del componente <xref:System.ComponentModel.BackgroundWorker>.  
  
     Gli attributi <xref:System.ComponentModel.CategoryAttribute.Category%2A> e <xref:System.ComponentModel.BrowsableAttribute.Browsable%2A> vengono applicati alla proprietà `UpdatePeriod` affinché venga riportata in una sezione personalizzata della finestra Proprietà denominata "Marquee".  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#150](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#150)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#150](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#150)]  
  
11. Implementare le funzioni di accesso della proprietà.  È necessario esporre ai client le due proprietà `LightColor` e `DarkColor`.  Gli attributi <xref:System.ComponentModel.CategoryAttribute.Category%2A> e <xref:System.ComponentModel.BrowsableAttribute.Browsable%2A> vengono applicati a tali proprietà affinché vengano riportate in una sezione personalizzata della finestra Proprietà denominata "Marquee".  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#160](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#160)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#160](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#160)]  
  
12. Implementare i gestori per gli eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> e  <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> del componente <xref:System.ComponentModel.BackgroundWorker>.  
  
     Il gestore dell'evento <xref:System.ComponentModel.BackgroundWorker.DoWork> resta inattivo per il numero di millisecondi specificato da `UpdatePeriod`, quindi genera l'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> finché l'animazione non viene arrestata mediante la chiamata  del metodo <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> nel codice.  
  
     Il gestore dell'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> attiva e disattiva l'illuminazione del testo per ottenere l'intermittenza.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#180](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#180)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#180](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#180)]  
  
13. Eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> per attivare l'animazione.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#170](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#170)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#170](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#170)]  
  
14. Premere F6 per compilare la soluzione.  
  
## Creazione del controllo figlio di MarqueeBorder  
 Il controllo `MarqueeBorder` è leggermente più sofisticato rispetto al controllo `MarqueeText` in quanto dispone di più proprietà e l'animazione nel metodo <xref:System.Windows.Forms.Control.OnPaint%2A> è più complessa,  anche se il principio è molto simile a quello del controllo `MarqueeText`.  
  
 Poiché il controllo `MarqueeBorder` può contenere controlli figlio, deve essere in grado di rilevare eventi <xref:System.Windows.Forms.Control.Layout>.  
  
#### Per creare il controllo MarqueeBorder  
  
1.  Aggiungere un nuovo elemento **Controllo personalizzato** al progetto `MarqueeControlLibrary`.  Assegnare al nuovo file di origine il nome di base "MarqueeBorder".  
  
2.  Trascinare un componente <xref:System.ComponentModel.BackgroundWorker> dalla **Casella degli strumenti** nel controllo `MarqueeBorder`.  Tale componente consentirà al controllo `MarqueeBorder` di aggiornarsi in modo asincrono.  
  
3.  Nella finestra Proprietà impostare le proprietà `WorkerReportsProgess` e <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> del componente <xref:System.ComponentModel.BackgroundWorker> su `true`.  Queste impostazioni consentono al componente <xref:System.ComponentModel.BackgroundWorker> di generare periodicamente l'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> e annullare gli aggiornamenti asincroni.  Per ulteriori informazioni, vedere [Componente BackgroundWorker](../../../../docs/framework/winforms/controls/backgroundworker-component.md).  
  
4.  Nella finestra Proprietà fare clic sul pulsante Eventi.  Collegare i gestori per gli eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> e <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>.  
  
5.  Aprire il file di origine `MarqueeBorder` nell'**editor di codice**.  Importare all'inizio del file i seguenti spazi dei nomi:  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#20)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#20)]  
  
6.  Modificare la dichiarazione di `MarqueeBorder` in modo che erediti da <xref:System.Windows.Forms.Panel> e implementare l'interfaccia `IMarqueeWidget`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#30)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#30)]  
  
7.  Per la gestione dello stato del controllo `MarqueeBorder` dichiarare le due enumerazioni `MarqueeSpinDirection`, che determina la direzione in cui le luci si muovono lungo i bordi, e `MarqueeLightShape`, che determina la forma delle luci, quadrata o circolare.  Inserire queste dichiarazioni prima della dichiarazione della classe `MarqueeBorder`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#97](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#97)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#97](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#97)]  
  
8.  Dichiarare le variabili di istanza che corrispondono alle proprietà esposte e inizializzarle nel costruttore.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#40](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#40)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#40](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#40)]  
  
9. Implementare l'interfaccia `IMarqueeWidget`.  
  
     Per avviare e arrestare l'animazione, i metodi `StartMarquee` e `StopMarquee` richiamano i metodi <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> e <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> del componente <xref:System.ComponentModel.BackgroundWorker>.  
  
     Poiché `MarqueeBorder` può contenere controlli figlio, il metodo `StartMarquee` enumera i controlli figlio e chiama `StartMarquee` per quelli che implementano `IMarqueeWidget`.  L'implementazione del metodo `StopMarquee` è simile.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#50](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#50)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#50](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#50)]  
  
10. Implementare le funzioni di accesso della proprietà.  Il controllo `MarqueeBorder` dispone di diverse proprietà per la gestione dell'aspetto.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#60](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#60)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#60](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#60)]  
  
11. Implementare i gestori per gli eventi <xref:System.ComponentModel.BackgroundWorker.DoWork> e  <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> del componente <xref:System.ComponentModel.BackgroundWorker>.  
  
     Il gestore dell'evento <xref:System.ComponentModel.BackgroundWorker.DoWork> resta inattivo per il numero di millisecondi specificato da `UpdatePeriod`, quindi genera l'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> finché l'animazione non viene arrestata mediante la chiamata  del metodo <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> nel codice.  
  
     Il gestore dell'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> incrementa la posizione della luce campione, dalla quale viene determino lo stato di illuminazione delle altre luci, e chiama il metodo <xref:System.Windows.Forms.Control.Refresh%2A> affinché il controllo venga ridisegnato.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#90](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#90)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#90](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#90)]  
  
12. Implementare i metodi di supporto `IsLit` e `DrawLight`.  
  
     Il metodo `IsLit` determina il colore di una luce in una determinata posizione.  Le luci accese vengono disegnate nel colore specificato dalla proprietà `LightColor` e quelle spente vengono disegnate nel colore fornito dalla proprietà `DarkColor`.  
  
     Il metodo `DrawLight` disegna una luce utilizzando il colore, la forma e la posizione appropriati.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#80](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#80)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#80](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#80)]  
  
13. Eseguire l'override dei metodi <xref:System.Windows.Forms.Control.OnLayout%2A> e <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
     Il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> disegna le luci lungo i bordi del controllo `MarqueeBorder`.  
  
     Poiché il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> dipende dalle dimensioni del controllo `MarqueeBorder`, è necessario chiamarlo ogni volta che il layout cambia.  A tale scopo, eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnLayout%2A> e chiamare il metodo <xref:System.Windows.Forms.Control.Refresh%2A>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#70](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#70)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#70](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#70)]  
  
## Creazione di una finestra di progettazione personalizzata per eseguire lo shadowing e filtrare le proprietà  
 La classe `MarqueeControlRootDesigner` fornisce l'implementazione della finestra di progettazione radice.  Oltre a questa finestra di progettazione, che viene applicata al controllo `MarqueeControl`, è necessaria una finestra di progettazione personalizzata associata specificamente al controllo `MarqueeBorder` che fornisca il comportamento personalizzato appropriato al contesto della finestra di progettazione radice personalizzata.  
  
 In particolare, `MarqueeBorderDesigner` eseguirà lo shadowing e filtrerà determinate proprietà per il controllo `MarqueeBorder` alterando l'interazione con l'ambiente di progettazione.  
  
 Lo shadowing consiste nell'intercettazione delle chiamate alla funzione di accesso alla proprietà di un componente e consente di tenere traccia del valore impostato dall'utente ed eventualmente passarlo al componente che si sta progettando.  
  
 In questo esempio, verrà eseguito lo shadowing delle proprietà <xref:System.Windows.Forms.Control.Visible%2A> e <xref:System.Windows.Forms.Control.Enabled%2A> mediante `MarqueeBorderDesigner`, impedendo così all'utente di rendere il controllo `MarqueeBorder` invisibile o disabilitarlo durante la fase di progettazione.  
  
 Nelle finestre di progettazione è inoltre possibile aggiungere e rimuovere proprietà.  In questo esempio, la proprietà <xref:System.Windows.Forms.Control.Padding%2A> verrà rimossa in fase di progettazione perché il controllo `MarqueeBorder` imposta a livello di codice la spaziatura interna in base alla dimensione delle luci specificata dalla proprietà `LightSize`.  
  
 La classe base di `MarqueeBorderDesigner` è <xref:System.ComponentModel.Design.ComponentDesigner>, che dispone di metodi per modificare gli attributi, le proprietà e gli eventi esposti da un controllo in fase di progettazione:  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterProperties%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterProperties%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterAttributes%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterAttributes%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterEvents%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterEvents%2A>  
  
 Per modificare l'interfaccia pubblica di un componente utilizzando questi metodi, è necessario attenersi alle regole riportate di seguito:  
  
-   Aggiungere o rimuovere elementi solo nei metodi `PreFilter`.  
  
-   Modificare gli elementi esistenti solo nei metodi `PostFilter`.  
  
-   Chiamare sempre l'implementazione di base per prima nei metodi `PreFilter`.  
  
-   Chiamare sempre l'implementazione di base per ultima nei metodi `PostFilter`.  
  
 Il rispetto di queste regole garantisce una visualizzazione uniforme di tutti i componenti nelle finestre di progettazione nell'ambiente di progettazione.  
  
 Poiché la classe <xref:System.ComponentModel.Design.ComponentDesigner> fornisce un dizionario per la gestione dei valori delle proprietà per le quali è stato eseguito lo shadowing, non è necessario creare variabili di istanza specifiche.  
  
#### Per creare una finestra di progettazione personalizzata per eseguire lo shadowing e filtrare le proprietà  
  
1.  Fare clic con il pulsante destro del mouse sulla cartella **Design**, quindi aggiungere una nuova classe.  Assegnare al file di origine il nome di base "MarqueeBorderDesigner".  
  
2.  Aprire il file di origine `MarqueeBorderDesigner` nell'**editor di codice**.  Importare all'inizio del file i seguenti spazi dei nomi:  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#420](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#420)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#420](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#420)]  
  
3.  Modificare la dichiarazione di `MarqueeBorderDesigner` in modo che erediti dalla classe <xref:System.Windows.Forms.Design.ParentControlDesigner>.  
  
     Poiché `MarqueeBorder` può contenere controlli figlio, `MarqueeBorderDesigner` eredita da <xref:System.Windows.Forms.Design.ParentControlDesigner> che gestisce l'interazione tra controlli padre e figlio.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#430](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#430)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#430](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#430)]  
  
4.  Eseguire l'override dell'implementazione di base di <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterProperties%2A>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#450](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#450)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#450](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#450)]  
  
5.  Implementare le proprietà <xref:System.Windows.Forms.Control.Enabled%2A> e <xref:System.Windows.Forms.Control.Visible%2A>.  Queste implementazioni eseguono lo shadowing delle proprietà del controllo.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#440](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#440)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#440](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#440)]  
  
## Gestione delle modifiche ai componenti  
 La classe `MarqueeControlRootDesigner` fornisce una fase di progettazione personalizzata per le istanze di `MarqueeControl`.  La maggioranza delle funzionalità della fase di progettazione sono ereditate dalla classe <xref:System.Windows.Forms.Design.DocumentDesigner>. Mediante codice verranno implementate due personalizzazioni specifiche: la gestione delle modifiche ai componenti e l'aggiunta di verbi di progettazione.  
  
 Quando gli utenti progettano le proprie istanze di `MarqueeControl`, la finestra di progettazione radice tiene traccia delle modifiche apportate a `MarqueeControl` e ai relativi controlli figlio.  L'ambiente della fase di progettazione offre un servizio utile, <xref:System.ComponentModel.Design.IComponentChangeService>, per tenere traccia delle modifiche apportate allo stato dei componenti.  
  
 Il riferimento a questo servizio viene ottenuto tramite una query all'ambiente con il metodo <xref:System.ComponentModel.Design.ComponentDesigner.GetService%2A>.  Se la query ha esito positivo, la finestra di progettazione può collegare un gestore per l'evento <xref:System.ComponentModel.Design.IComponentChangeService.ComponentChanged> ed eseguire le attività richieste per mantenere uno stato coerente durante la fase di progettazione.  
  
 Nel caso della classe `MarqueeControlRootDesigner`, si chiamerà il metodo <xref:System.Windows.Forms.Control.Refresh%2A> per ogni oggetto `IMarqueeWidget` contenuto nel controllo `MarqueeControl`.  In tal modo l'oggetto `IMarqueeWidget` verrà ridisegnato correttamente se vengono modificate proprietà del controllo padre, ad esempio <xref:System.Windows.Forms.Control.Size%2A>.  
  
#### Per gestire le modifiche ai componenti  
  
1.  Aprire il file di origine `MarqueeControlRootDesigner` nell'**editor di codice** ed eseguire l'override del metodo <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A>.  Chiamare l'implementazione di base di <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A> ed eseguire una query per <xref:System.ComponentModel.Design.IComponentChangeService>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#580](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#580)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#580](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#580)]  
  
2.  Implementare il gestore eventi <xref:System.ComponentModel.Design.IComponentChangeService.OnComponentChanged%2A>.  Verificare il tipo del componente che è stato modificato e, se si tratta di `IMarqueeWidget`, chiamare il relativo metodo <xref:System.Windows.Forms.Control.Refresh%2A>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#560](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#560)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#560](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#560)]  
  
## Aggiunta di verbi di progettazione alla finestra di progettazione personalizzata  
 Un verbo di progettazione è un comando di menu collegato a un gestore eventi  che viene aggiunto al menu di scelta rapida di un componente in fase di progettazione.  Per ulteriori informazioni, vedere <xref:System.ComponentModel.Design.DesignerVerb>.  
  
 Alle finestre di progettazione verranno aggiunti i due verbi di progettazione **Esegui test** e **Interrompi test** che consentono di visualizzare in fase di progettazione il comportamento in fase di esecuzione del controllo `MarqueeControl`.  Questi verbi verranno aggiunti a `MarqueeControlRootDesigner`.  
  
 Quando si richiama **Esegui test**, il gestore eventi del verbo chiamerà il metodo `StartMarquee` in `MarqueeControl`.  Quando si richiama **Interrompi test**, il gestore eventi del verbo chiamerà il metodo `StopMarquee` in `MarqueeControl`.  L'implementazione dei metodi `StartMarquee` e `StopMarquee` esegue la chiamata nei controlli contenuti che implementano `IMarqueeWidget`, in modo che il test venga eseguito anche per ogni controllo `IMarqueeWidget` contenuto.  
  
#### Per aggiungere verbi di progettazione alle finestre di progettazione personalizzate  
  
1.  Nella classe `MarqueeControlRootDesigner` aggiungere i gestori eventi `OnVerbRunTest` e `OnVerbStopTest`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#570](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#570)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#570](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#570)]  
  
2.  Connettere questi gestori eventi ai verbi di progettazione corrispondenti.  `MarqueeControlRootDesigner` eredita dalla propria classe base un <xref:System.ComponentModel.Design.DesignerVerbCollection>.  Verranno creati due nuovi oggetti <xref:System.ComponentModel.Design.DesignerVerb> e aggiunti alla raccolta nel metodo <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#590](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#590)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#590](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#590)]  
  
## Creazione di un UITypeEditor personalizzato  
 Quando si crea una fase di progettazione personalizzata per gli utenti, è spesso opportuno realizzare un'interazione personalizzata con la finestra Proprietà.  A tal fine è possibile creare un <xref:System.Drawing.Design.UITypeEditor>.  Per ulteriori informazioni, vedere [How to: Create a UI Type Editor](../Topic/How%20to:%20Create%20a%20UI%20Type%20Editor.md).  
  
 Il controllo `MarqueeBorder` espone diverse proprietà nella finestra Proprietà,  due delle quali, `MarqueeSpinDirection` e `MarqueeLightShape`, sono rappresentate da enumerazioni.  Per illustrare l'utilizzo di un editor di tipi con interfaccia utente, alla proprietà `MarqueeLightShape` verrà associata una classe <xref:System.Drawing.Design.UITypeEditor>.  
  
#### Per creare un editor di tipi con interfaccia utente personalizzato  
  
1.  Aprire il file di origine `MarqueeBorder` nell'**editor di codice**.  
  
2.  Nella definizione della classe `MarqueeBorder` dichiarare una classe denominata `LightShapeEditor` derivita da <xref:System.Drawing.Design.UITypeEditor>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#96](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#96)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#96](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#96)]  
  
3.  Dichiarare una variabile dell'istanza di <xref:System.Windows.Forms.Design.IWindowsFormsEditorService> denominata `editorService`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#92](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#92)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#92](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#92)]  
  
4.  Eseguire l'override del metodo <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A>.  Questa implementazione restituisce <xref:System.Drawing.Design.UITypeEditorEditStyle>, che indica all'ambiente di progettazione come visualizzare `LightShapeEditor`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#93](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#93)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#93](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#93)]  
  
5.  Eseguire l'override del metodo <xref:System.Drawing.Design.UITypeEditor.EditValue%2A>.  Questa implementazione richiede all'ambiente di progettazione un oggetto <xref:System.Windows.Forms.Design.IWindowsFormsEditorService>.  Se la query ha esito positivo, viene creato un controllo `LightShapeSelectionControl`,  quindi viene chiamato il metodo <xref:System.Windows.Forms.Design.IWindowsFormsEditorService.DropDownControl%2A> per avviare `LightShapeEditor`.  Il valore restituito dalla chiamata viene passato all'ambiente di progettazione.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#94](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#94)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#94](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#94)]  
  
## Creazione di un controllo di visualizzazione per l'editor di tipi con interfaccia utente personalizzato  
  
1.  La proprietà `MarqueeLightShape` supporta due tipi di forme per le luci, `Square` e `Circle`.  Verrà creato un controllo personalizzato utilizzato unicamente per visualizzare graficamente i valori nella finestra Proprietà.  Questo controllo personalizzato verrà utilizzato da <xref:System.Drawing.Design.UITypeEditor> per interagire con la finestra Proprietà.  
  
#### Per creare un controllo di visualizzazione per l'editor di tipi con interfaccia utente personalizzato  
  
1.  Aggiungere un nuovo elemento <xref:System.Windows.Forms.UserControl> al progetto `MarqueeControlLibrary`.  Assegnare al nuovo file di origine il nome di base "LightShapeSelectionControl".  
  
2.  Trascinare due controlli <xref:System.Windows.Forms.Panel> dalla **Casella degli strumenti** in `LightShapeSelectionControl`,  assegnarvi i nomi `squarePanel` e `circlePanel` e sistemarli affiancati.  Impostare la proprietà <xref:System.Windows.Forms.Control.Size%2A> di entrambi i controlli <xref:System.Windows.Forms.Panel> su \(60, 60\).  Impostare la proprietà <xref:System.Windows.Forms.Control.Location%2A> del controllo `squarePanel` su \(8, 10\).  Impostare la proprietà <xref:System.Windows.Forms.Control.Location%2A> del controllo `circlePanel` su \(80, 10\).  Infine, impostare la proprietà <xref:System.Windows.Forms.Control.Size%2A> del controllo `LightShapeSelectionControl` su \(150, 80\).  
  
3.  Aprire il file di origine `LightShapeSelectionControl` nell'**Editor di codice**.  Importare all'inizio del file lo spazio dei nomi <xref:System.Windows.Forms.Design?displayProperty=fullName>:  
  
```vb  
Imports System.Windows.Forms.Design  
```  
  
```csharp  
using System.Windows.Forms.Design;  
```  
  
1.  Implementare i gestori eventi <xref:System.Windows.Forms.Control.Click> dei controlli `squarePanel` e `circlePanel`.  Questi metodi richiamano il metodo <xref:System.Windows.Forms.Design.IWindowsFormsEditorService.CloseDropDown%2A> per terminare la sessione di modifica personalizzata di <xref:System.Drawing.Design.UITypeEditor>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#390](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#390)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#390](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#390)]  
  
2.  Dichiarare una variabile dell'istanza di <xref:System.Windows.Forms.Design.IWindowsFormsEditorService> denominata `editorService`.  
  
```vb  
Private editorService As IWindowsFormsEditorService  
```  
  
```csharp  
private IWindowsFormsEditorService editorService;  
```  
  
1.  Dichiarare una variabile dell'istanza di `MarqueeLightShape` denominata `lightShapeValue`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#330](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#330)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#330](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#330)]  
  
2.  Nel costruttore `LightShapeSelectionControl`, collegare i gestori eventi <xref:System.Windows.Forms.Control.Click> agli eventi <xref:System.Windows.Forms.Control.Click> dei controlli `squarePanel` e `circlePanel`.  Definire inoltre un overload del costruttore che assegna il valore `MarqueeLightShape` dell'ambiente di progettazione al campo `lightShapeValue`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#340](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#340)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#340](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#340)]  
  
3.  Nel metodo <xref:System.ComponentModel.Component.Dispose%2A>, scollegare i gestori eventi <xref:System.Windows.Forms.Control.Click>.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#350](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#350)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#350](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#350)]  
  
4.  In **Esplora soluzioni** fare clic sul pulsante **Mostra tutti i file**.  Aprire il file LightShapeSelectionControl.Designer.cs o il file LightShapeSelectionControl.Designer.vb e rimuovere la definizione predefinita del metodo <xref:System.ComponentModel.Component.Dispose%2A>.  
  
5.  Implementare la proprietà `LightShape`.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#360](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#360)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#360](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#360)]  
  
6.  Eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  Questa implementazione, oltre a disegnare un quadrato pieno e un cerchio,  evidenzia il valore selezionato disegnando un bordo attorno a una delle due forme.  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#380](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#380)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#380](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#380)]  
  
## Test del controllo personalizzato nella finestra di progettazione  
 A questo punto è possibile compilare il progetto `MarqueeControlLibrary`.  Testare l'implementazione creando un controllo che eredita dalla classe `MarqueeControl` e utilizzandolo su un form.  
  
#### Per creare un'implementazione di MarqueeControl personalizzata  
  
1.  Aprire `DemoMarqueeControl` in Progettazione Windows Form.  In questo modo verrà creata un'istanza del tipo `DemoMarqueeControl` visualizzata in un'istanza del tipo `MarqueeControlRootDesigner`.  
  
2.  Nella **Casella degli strumenti** aprire la scheda **Componenti MarqueeControlLibrary** in cui sarà possibile selezionare i controlli `MarqueeBorder` e `MarqueeText`.  
  
3.  Trascinare un'istanza del controllo `MarqueeBorder` nell'area di progettazione di `DemoMarqueeControl`.  Ancorare il controllo `MarqueeBorder` al controllo padre.  
  
4.  Trascinare un'istanza del controllo `MarqueeText` nell'area di progettazione di `DemoMarqueeControl`.  
  
5.  Compilare la soluzione.  
  
6.  Fare clic con il pulsante destro del mouse su `DemoMarqueeControl` e scegliere **Esegui test** dal menu di scelta rapida per avviare l'animazione.  Fare clic su **Interrompi test** per arrestare l'animazione.  
  
7.  Aprire **Form1** nella visualizzazione Progettazione.  
  
8.  Inserire due controlli <xref:System.Windows.Forms.Button> nel form,  Denominarli `startButton` e `stopButton` e modificare i valori della proprietà <xref:System.Windows.Forms.Control.Text%2A> rispettivamente in Start e Stop.  
  
9. Implementare i gestori dell'evento <xref:System.Windows.Forms.Control.Click> per entrambi i controlli <xref:System.Windows.Forms.Button>.  
  
10. Nella **Casella degli strumenti** aprire la scheda **Componenti MarqueeControlTest** in cui sarà possibile selezionare il controllo `DemoMarqueeControl`.  
  
11. Trascinare un'istanza del controllo `DemoMarqueeControl` nell'area di progettazione di **Form1**.  
  
12. Nei gestori dell'evento <xref:System.Windows.Forms.Control.Click> richiamare i metodi `Start` e `Stop` in `DemoMarqueeControl`.  
  
```vb  
Private Sub startButton_Click(sender As Object, e As System.EventArgs)  
    Me.demoMarqueeControl1.Start()  
End Sub 'startButton_Click  
  
Private Sub stopButton_Click(sender As Object, e As System.EventArgs)  
Me.demoMarqueeControl1.Stop()  
End Sub 'stopButton_Click  
```  
  
```csharp  
private void startButton_Click(object sender, System.EventArgs e)  
{  
    this.demoMarqueeControl1.Start();  
}  
  
private void stopButton_Click(object sender, System.EventArgs e)  
{  
    this.demoMarqueeControl1.Stop();  
}  
```  
  
1.  Impostare il progetto `MarqueeControlTest` come progetto di avvio ed eseguirlo.  Verrà visualizzato il form contenente il controllo `DemoMarqueeControl`.  Fare clic sul pulsante **Start** per avviare l'animazione.  Verrà visualizzato il testo lampeggiante e lo spostamento delle luci lungo i bordi.  
  
## Passaggi successivi  
 `MarqueeControlLibrary` dimostra una semplice implementazione dei controlli personalizzati e delle finestre di progettazione associate.  Questo esempio può essere reso più sofisticato in diversi modi.  
  
-   Modificare i valori delle proprietà per il controllo `DemoMarqueeControl` nella finestra di progettazione.  Aggiungere più controlli `MarqueBorder` e ancorarli nelle relative istanze padre per creare un effetto annidato.  Provare diverse impostazioni per le proprietà relative alle luci e `UpdatePeriod`.  
  
-   Creare altre implementazioni di `IMarqueeWidget`,  ad esempio per creare un'insegna al neon lampeggiante o un'insegna animata con più immagini.  
  
-   Personalizzare ulteriormente la fase di progettazione  provando a eseguire lo shadowing di altre proprietà oltre a <xref:System.Windows.Forms.Control.Enabled%2A> e <xref:System.Windows.Forms.Control.Visible%2A> e aggiungendo nuove proprietà.  Aggiungere nuovi verbi di progettazione per semplificare attività comuni quali l'ancoraggio dei controlli figlio.  
  
-   Creare una licenza per il controllo `MarqueeControl`.  Per ulteriori informazioni, vedere [How to: License Components and Controls](../Topic/How%20to:%20License%20Components%20and%20Controls.md).  
  
-   Verificare la serializzazione dei controlli e la generazione del relativo codice.  Per ulteriori informazioni, vedere [Dynamic Source Code Generation and Compilation](../../../../docs/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.UserControl>   
 <xref:System.Windows.Forms.Design.ParentControlDesigner>   
 <xref:System.Windows.Forms.Design.DocumentDesigner>   
 <xref:System.ComponentModel.Design.IRootDesigner>   
 <xref:System.ComponentModel.Design.DesignerVerb>   
 <xref:System.Drawing.Design.UITypeEditor>   
 <xref:System.ComponentModel.BackgroundWorker>   
 [How to: Create a Windows Forms Control That Takes Advantage of Design\-Time Features](../Topic/How%20to:%20Create%20a%20Windows%20Forms%20Control%20That%20Takes%20Advantage%20of%20Design-Time%20Features.md)   
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)   
 [Custom Designers](../Topic/Custom%20Designers.md)   
 [Libreria di forme .NET: esempio di finestra di progettazione](http://windowsforms.net/articles/shapedesigner.aspx)