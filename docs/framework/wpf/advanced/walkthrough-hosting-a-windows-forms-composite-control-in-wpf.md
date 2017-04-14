---
title: "Procedura dettagliata: hosting di controlli Windows Form compositi in WPF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controlli composti, hosting in WPF"
  - "hosting di controlli Windows Form in WPF"
ms.assetid: 96fcd78d-1c77-4206-8928-3a0579476ef4
caps.latest.revision: 33
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# Procedura dettagliata: hosting di controlli Windows Form compositi in WPF
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornisce un ambiente dettagliato per la creazione di applicazioni.  Tuttavia, quando si dispone di una grande quantità di codice [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], può essere opportuno riutilizzare almeno parte di tale codice nell'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] anziché riscriverlo dall'inizio.  Lo scenario più comune prevede l'esistenza di controlli [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)].  In alcuni casi potrebbe non disporsi nemmeno dell'accesso al codice sorgente per questi controlli.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce una procedura molto semplice per l'hosting di tali controlli in un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  È ad esempio possibile utilizzare [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per la maggior parte della programmazione pur ospitando i controlli <xref:System.Windows.Forms.DataGridView> specializzati.  
  
 In questa procedura dettagliata viene descritta un'applicazione che ospita un controllo composito [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)] per eseguire l'immissione di dati in un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Il controllo composito è compresso in una DLL.  Questa procedura generale può essere estesa ad applicazioni e controlli più complessi.  Questa procedura dettagliata è stata progettata in modo che risulti quasi identica per aspetto e funzionalità a [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md).  La differenza primaria risiede nel fatto che lo scenario di hosting risulta invertito.  
  
 La procedura dettagliata è divisa in due sezioni.  Nella prima sezione viene brevemente descritta l'implementazione del controllo composito [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)].  Nella seconda sezione viene illustrato in dettaglio come ospitare il controllo composito in un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], come ricevere eventi dal controllo e come accedere ad alcune delle proprietà del controllo.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Implementazione del controllo composito Windows Form.  
  
-   Implementazione dell'applicazione host WPF.  
  
 Per un elenco di codice completo delle attività illustrate in questa procedura dettagliata, vedere [Esempio di hosting di controlli Windows Form compositi in WPF](http://go.microsoft.com/fwlink/?LinkID=159999) \(la pagina potrebbe essere in inglese\).  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
## Implementazione del controllo composito Windows Form  
 Il controllo composito [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)] utilizzato in questo esempio è un semplice form di immissione dati.  Questo form accetta il nome e l'indirizzo dell'utente e utilizza un evento personalizzato per restituire tali informazioni all'host.  Nell’immagine riportata di seguito viene illustrato il controllo sottoposto a rendering.  
  
 ![Controllo Windows Form semplice](../../../../docs/framework/wpf/advanced/media/wfcontrol.png "WFControl")  
Distribuire un controllo composito Windows Form  
  
### Creazione del progetto  
 Per avviare il progetto:  
  
1.  Avviare [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] e aprire la finestra di dialogo **Nuovo progetto**.  
  
2.  Nella categoria Finestra, selezionare il modello **Libreria di controllo Windows Form**.  
  
3.  Denominare il nuovo progetto `MyControls`.  
  
4.  Come posizione, specificare una cartella di livello principale denominata in modo appropriato, ad esempio `WpfHostingWindowsFormsControl`.  Successivamente, l'applicazione host verrà posizionata in questa cartella.  
  
5.  Scegliere **OK** per creare il progetto.  Il progetto predefinito contiene un singolo controllo denominato `UserControl1`.  
  
6.  In Esplora soluzioni rinominare `UserControl1` in `MyControl1`.  
  
 Il progetto dovrebbe presentare riferimenti alle DLL di sistema riportate di seguito.  Se alcune di queste DLL non sono incluse per impostazione predefinita, aggiungerle al progetto.  
  
-   Sistema  
  
-   System.Data  
  
-   System.Drawing  
  
-   System.Windows.Forms  
  
-   System.Xml  
  
### Aggiunta di controlli al form  
 Per aggiungere controlli al form:  
  
-   Aprire `MyControl1` nella finestra di progettazione.  
  
 Aggiungere cinque controlli <xref:System.Windows.Forms.Label> e i controlli <xref:System.Windows.Forms.TextBox> corrispondenti, ridimensionati e disposti come nell'illustrazione precedente.  Nell'esempio i controlli <xref:System.Windows.Forms.TextBox> sono denominati:  
  
-   `txtName`  
  
-   `txtAddress`  
  
-   `txtCity`  
  
-   `txtState`  
  
-   `txtZip`  
  
 Aggiungere due controlli <xref:System.Windows.Forms.Button> con etichetta **OK** e **Annulla**.  Nell'esempio i nomi dei pulsanti sono rispettivamente `btnOK` e `btnCancel`.  
  
### Implementazione del codice di supporto  
 Aprire il form in visualizzazione codice.  Il controllo restituisce i dati raccolti all'host corrispondente generando l'evento personalizzato `OnButtonClick`.  I dati sono contenuti nell'oggetto dell'argomento dell'evento.  Nel codice riportato di seguito viene illustrato l'evento e la dichiarazione delegate.  
  
 Aggiungere il codice seguente alla classe `MyControl1`.  
  
 [!code-csharp[WpfHostingWindowsFormsControl#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#2)]
 [!code-vb[WpfHostingWindowsFormsControl#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#2)]  
  
 La classe `MyControlEventArgs` contiene le informazioni da restituire all'host.  
  
 Aggiungere la classe seguente al form.  
  
 [!code-csharp[WpfHostingWindowsFormsControl#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#3)]
 [!code-vb[WpfHostingWindowsFormsControl#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#3)]  
  
 Quando l'utente fa clic su **OK** o su **Annulla**, il gestore eventi <xref:System.Windows.Forms.Control.Click> crea un oggetto `MyControlEventArgs` che contiene i dati e genera l'evento `OnButtonClick`.  L'unica differenza tra i due gestori è la proprietà `IsOK` dell'argomento dell'evento.  Questa proprietà consente all'host di determinare su quale pulsante è stato fatto clic.  La proprietà è impostata su `true` per il pulsante **OK** e su `false` per il pulsante **Annulla**.  Nel codice riportato di seguito vengono illustrati i gestori dei due pulsanti.  
  
 Aggiungere il codice seguente alla classe `MyControl1`.  
  
 [!code-csharp[WpfHostingWindowsFormsControl#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#4)]
 [!code-vb[WpfHostingWindowsFormsControl#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#4)]  
  
### Assegnazione di un nome sicuro all'assembly e compilazione dell'assembly  
 Perché a questo assembly venga fatto riferimento in un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario che abbia un nome sicuro.  Per creare un nome sicuro, creare un file di chiave Sn.exe e aggiungerlo al progetto.  
  
1.  Aprire il prompt dei comandi di [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)].  Per effettuare tale operazione, fare clic sul pulsante **Start** e scegliere **Programmi\/Microsoft Visual Studio 2010\/Visual Studio Tools\/Prompt dei comandi di Visual Studio**.  Viene avviata una finestra della console con le variabili di ambiente personalizzate.  
  
2.  Al prompt dei comandi utilizzare il comando `cd` per passare alla cartella del progetto.  
  
3.  Generare un file di chiave denominato MyControls.snk eseguendo il comando indicato.  
  
    ```  
    Sn.exe -k MyControls.snk  
    ```  
  
4.  Per includere il file di chiave nel progetto, fare clic con il pulsante destro del mouse sul nome del progetto in Esplora soluzioni e scegliere **Proprietà**.  In Progettazione progetti fare clic sulla scheda **Firma**, selezionare la casella di controllo **Firma assembly** e passare al file di chiave.  
  
5.  Compilare la soluzione.  La compilazione creerà una DLL denominata MyControls.dll.  
  
## Implementazione dell'applicazione host WPF.  
 L'applicazione host [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> per ospitare `MyControl1`.  L'applicazione gestisce l'evento `OnButtonClick` per ricevere i dati dal controllo.  Dispone inoltre di una raccolta di pulsanti di opzione che consente di modificare alcune delle proprietà del controllo dall'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Nell'immagine riportata di seguito viene illustrata l'applicazione finita.  
  
 ![Controllo incorporato in una pagina WPF](../../../../docs/framework/wpf/advanced/media/avalonhost.png "AvalonHost")  
Applicazione completa che mostra il controllo incorporato nell'applicazione WPF  
  
### Creazione del progetto  
 Per avviare il progetto:  
  
1.  Aprire [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] e selezionare **Nuovo progetto**.  
  
2.  Nella categoria Finestra selezionare il modello **Applicazione WPF**.  
  
3.  Denominare il nuovo progetto `WpfHost`.  
  
4.  Come posizione, specificare la stessa cartella di livello principale che contiene il progetto MyControls.  
  
5.  Scegliere **OK** per creare il progetto.  
  
 È inoltre necessario aggiungere riferimenti alla DLL che contiene `MyControl1` e altri assembly.  
  
1.  Fare clic con il pulsante destro del mouse in Esplora soluzioni e selezionare **Aggiungi riferimento**.  
  
2.  Fare clic sulla scheda **Sfoglia** e passare alla cartella che contiene MyControls.dll.  In questa procedura dettagliata, questa cartella è MyControls\\bin\\Debug.  
  
3.  Selezionare MyControls.dll, quindi scegliere **OK**.  
  
4.  Aggiungere un riferimento all'assembly WindowsFormsIntegration, denominato WindowsFormsIntegration.dll.  
  
### Implementazione del layout di base  
 L'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] dell'applicazione host viene implementata in MainWindow.xaml.  Questo file contiene il markup [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] che definisce il layout e ospita il controllo [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)].  L'applicazione è suddivisa in tre aree:  
  
-   Il pannello **Proprietà del controllo** che contiene una raccolta di pulsanti di opzione che si possono utilizzare per modificare diverse proprietà del controllo ospitato.  
  
-   Il pannello **Dati dal controllo** che contiene numerosi elementi <xref:System.Windows.Controls.TextBlock> che consentono di visualizzare i dati restituiti dal controllo ospitato.  
  
-   Il controllo ospitato stesso.  
  
 Nel codice XAML seguente viene mostrato il layout di base.  Il markup necessario per ospitare `MyControl1` viene omesso da questo esempio, ma verrà esaminato più avanti.  
  
 Sostituire il codice XAML in MainWindow.xaml con quanto segue.  Se si utilizza Visual Basic, modificare la classe in `x:Class="MainWindow"`.  
  
 [!code-xml[WpfHostingWindowsFormsControl#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#100)]  
  
 Il primo elemento <xref:System.Windows.Controls.StackPanel> contiene numerose serie di controlli <xref:System.Windows.Controls.RadioButton> che consentono di modificare diverse proprietà predefinite del controllo ospitato.  Tale elemento è seguito da un elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>, che ospita `MyControl1`.  L'elemento finale <xref:System.Windows.Controls.StackPanel> contiene numerosi elementi <xref:System.Windows.Controls.TextBlock> che consentono di visualizzare i dati restituiti dal controllo ospitato.  L'ordine degli elementi e le impostazioni degli attributi <xref:System.Windows.Controls.DockPanel.Dock%2A> e <xref:System.Windows.FrameworkElement.Height%2A> consentono di incorporare il controllo ospitato nella finestra senza spazi o distorsioni.  
  
#### Hosting del controllo  
 La versione modificata riportata di seguito del codice XAML precedente punta l'attenzione sugli elementi necessari per ospitare `MyControl1`.  
  
 [!code-xml[WpfHostingWindowsFormsControl#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#101)]  
[!code-xml[WpfHostingWindowsFormsControl#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#102)]  
  
 L'attributo del mapping dello spazio dei nomi `xmlns` crea un riferimento allo spazio dei nomi `MyControls` che contiene il controllo ospitato.  Questo mapping consente di rappresentare `MyControl1` in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] come `<mcl:MyControl1>`.  
  
 Due elementi dell'handle XAML gestiscono l'hosting:  
  
-   `WindowsFormsHost` rappresenta l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> che consente di ospitare un controllo [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)] in un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   `mcl:MyControl1`, che rappresenta `MyControl1`, viene aggiunto alla raccolta figlio dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  Di conseguenza, viene eseguito il rendering di questo controllo [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)] come parte della finestra [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ed è possibile comunicare con il controllo dall'applicazione.  
  
### Implementazione del file code\-behind  
 Il file code\-behind, MainWindow.xaml.vb o MainWindow, contiene il codice procedurale che implementa la funzionalità dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] esaminata nella sezione precedente.  Le attività principali sono:  
  
-   Associare un gestore eventi all'evento `OnButtonClick` di `MyControl1`.  
  
-   Modificare diverse proprietà di `MyControl1`, in base al modo in cui viene impostata la raccolta di pulsanti di opzione.  
  
-   Visualizzare i dati raccolti dal controllo.  
  
#### Inizializzazione dell'applicazione  
 Il codice di inizializzazione è contenuto in un gestore eventi per l'evento <xref:System.Windows.FrameworkElement.Loaded> della finestra e associa un gestore eventi all'evento `OnButtonClick` del controllo.  
  
 In MainWindow.xaml.vb o MainWindow.xaml.cs aggiungere il codice seguente alla classe `MainWindow`.  
  
 [!code-csharp[WpfHostingWindowsFormsControl#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#11)]
 [!code-vb[WpfHostingWindowsFormsControl#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#11)]  
  
 Dato che il codice [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] esaminato in precedenza ha consentito di aggiungere `MyControl1` alla raccolta di elementi figlio dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>, è possibile eseguire il cast di <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A> dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> per ottenere il riferimento a `MyControl1`.  È quindi possibile utilizzare tale riferimento per associare un gestore eventi a `OnButtonClick`.  
  
 Oltre a fornire un riferimento al controllo stesso, <xref:System.Windows.Forms.Integration.WindowsFormsHost> espone numerose proprietà del controllo, che si possono modificare dall'applicazione.  Il codice di inizializzazione assegna tali valori a variabili globali private per un uso successivo nell'applicazione.  
  
 Aggiungere l'istruzione `Imports` o `using` seguente all'inizio del file per poter accedere agevolmente ai tipi nella DLL `MyControls`.  
  
```vb  
Imports MyControls  
```  
  
```csharp  
using MyControls;  
```  
  
#### Gestione dell'evento OnButtonClick  
 `MyControl1` genera l'evento `OnButtonClick` quando l'utente fa clic su uno dei pulsanti del controllo.  
  
 Aggiungere il codice seguente alla classe `MainWindow`.  
  
 [!code-csharp[WpfHostingWindowsFormsControl#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#12)]
 [!code-vb[WpfHostingWindowsFormsControl#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#12)]  
  
 I dati nelle caselle di testo vengono compressi nell'oggetto`MyControlEventArgs`.  Se l'utente fa clic sul pulsante **OK**, il gestore eventi estrae i dati e li visualizza nel pannello sottostante a `MyControl1`.  
  
#### Modifica delle proprietà del controllo  
 L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> espone numerose proprietà predefinite del controllo ospitato.  Di conseguenza è possibile modificare l'aspetto del controllo perché corrisponda più da vicino allo stile dell'applicazione.  Le serie di pulsanti di opzione del pannello sinistro consentono all'utente di modificare numerose proprietà del colore e del carattere.  Ogni serie di pulsanti dispone di un gestore per l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click>, che rileva le selezioni del pulsante di opzione da parte dell'utente e modifica la proprietà corrispondente nel controllo.  
  
 Aggiungere il codice seguente alla classe `MainWindow`.  
  
 [!code-csharp[WpfHostingWindowsFormsControl#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#13)]
 [!code-vb[WpfHostingWindowsFormsControl#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#13)]  
  
 Compilare ed eseguire l'applicazione.  Aggiungere testo al controllo composito Windows Form, quindi scegliere **OK**.  Il testo viene visualizzato nelle etichette.  Fare clic sui diversi pulsanti di opzione per visualizzare l'effetto sul controllo.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Procedura dettagliata: hosting di controlli Windows Form in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)