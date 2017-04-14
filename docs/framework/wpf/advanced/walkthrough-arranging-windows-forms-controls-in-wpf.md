---
title: "Procedura dettagliata: disposizione di controlli Windows Form in WPF | Microsoft Docs"
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
  - "disposizione di controlli"
  - "applicazioni ibride [interoperabilità WPF]"
ms.assetid: a1db8049-15c7-45d6-ae3d-36a6735cb848
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 28
---
# Procedura dettagliata: disposizione di controlli Windows Form in WPF
In questa procedura dettagliata viene illustrato come utilizzare le funzionalità di layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per disporre controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] in un'applicazione ibrida.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione del progetto.  
  
-   Utilizzo delle impostazioni di layout predefinite.  
  
-   Ridimensionamento in base al contenuto.  
  
-   Utilizzo delle posizioni assolute.  
  
-   Specifica esplicita delle dimensioni.  
  
-   Impostazione delle proprietà di layout.  
  
-   Informazioni sulle limitazioni dell'ordine Z.  
  
-   Ancoraggio.  
  
-   Impostazione della visibilità.  
  
-   Hosting di un controllo che non si adatta.  
  
-   Ridimensionamento.  
  
-   Rotazione.  
  
-   Impostazione della spaziatura interna e dei margini.  
  
-   Utilizzo di contenitori di layout dinamici.  
  
 Per un elenco di codice completo delle attività illustrate in questa procedura dettagliata, vedere [Esempio di disposizione di controlli Windows Form in WPF](http://go.microsoft.com/fwlink/?LinkID=159971) \(la pagina potrebbe essere in inglese\).  
  
 Questa procedura consente di approfondire le funzionalità di layout di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] nelle applicazioni basate su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
## Creazione del progetto  
  
#### Per creare e configurare il progetto  
  
1.  Creare un progetto di applicazione WPF denominato `WpfLayoutHostingWf`.  
  
2.  In Esplora soluzioni aggiungere riferimenti agli assembly indicati di seguito.  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
    -   System.Drawing  
  
3.  Fare doppio clic su MainWindow.xaml per aprirlo in visualizzazione XAML.  
  
4.  Nell'elemento <xref:System.Windows.Window> aggiungere il mapping dello spazio dei nomi [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] seguente.  
  
    ```xaml  
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"  
    ```  
  
5.  Nell'elemento <xref:System.Windows.Controls.Grid> impostare la proprietà <xref:System.Windows.Controls.Grid.ShowGridLines%2A> su `true` e definire cinque righe e tre colonne.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#2)]  
  
## Utilizzo delle impostazioni di layout predefinite  
 Per impostazione predefinita, l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> gestisce il layout del controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato.  
  
#### Per utilizzare le impostazioni di layout predefinite  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#3)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  Il controllo <xref:System.Windows.Forms.Button?displayProperty=fullName> [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] verrà visualizzato in <xref:System.Windows.Controls.Canvas>.  Il controllo ospitato viene ridimensionato in base al contenuto e l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> viene ridimensionato in base al controllo ospitato.  
  
## Ridimensionamento in base al contenuto  
 L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> garantisce che il controllo ospitato venga ridimensionato per visualizzare correttamente il contenuto.  
  
#### Per ridimensionare in base al contenuto  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#4)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  I due nuovi controlli pulsante vengono ridimensionati per visualizzare correttamente la stringa di testo più lunga e la dimensione del carattere più grande e gli elementi <xref:System.Windows.Forms.Integration.WindowsFormsHost> vengono ridimensionati in base ai controlli ospitati.  
  
## Utilizzo delle posizioni assolute  
 È possibile utilizzare le posizioni assolute per posizionare l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> in qualsiasi punto dell'interfaccia utente.  
  
#### Per utilizzare le posizioni assolute  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#5)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> viene posizionato a 20 pixel dal lato superiore della cella della griglia e a 20 pixel da sinistra.  
  
## Specifica esplicita delle dimensioni  
 È possibile specificare la dimensione dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> mediante le proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A>.  
  
#### Per specificare in modo esplicito le dimensioni  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#6)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> viene impostato a una dimensione di 50 pixel di larghezza per 70 pixel di altezza, impostazioni più ridotte rispetto a quelle del layout predefinito.  Il contenuto del controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] viene ridisposto di conseguenza.  
  
## Impostazione delle proprietà di layout  
 Impostare sempre le proprietà correlate al layout del controllo ospitato utilizzando le proprietà dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  L'impostazione diretta delle proprietà di layout nel controllo ospitato darà risultati imprevisti.  
  
 L'impostazione delle proprietà correlate al layout nel controllo ospitato in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] non ha alcun effetto.  
  
#### Per visualizzare gli effetti dell'impostazione delle proprietà nel controllo  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#7)]  
  
2.  In Esplora soluzioni fare doppio clic su MainWindow.xaml.  vb o MainWindow.xaml.cs per aprirlo nell'editor del codice.  
  
3.  Copiare il codice riportato di seguito nella definizione della classe `MainWindow`.  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#101)]
     [!code-vb[WpfLayoutHostingWfWithXaml#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#101)]  
  
4.  Premere F5 per compilare ed eseguire l'applicazione.  
  
5.  Scegliere il pulsante **Fare clic qui**.  Il gestore eventi `button1_Click` imposta le proprietà <xref:System.Windows.Forms.Control.Top%2A> e <xref:System.Windows.Forms.Control.Left%2A> nel controllo ospitato.  Ciò fa sì che il controllo ospitato venga riposizionato all'interno dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  L'host mantiene la stessa area dello schermo, ma il controllo ospitato viene ritagliato.  Al contrario, il controllo ospitato dovrebbe sempre occupare l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
## Informazioni sulle limitazioni dell'ordine Z  
 per impostazione predefinita, visibile <xref:System.Windows.Forms.Integration.WindowsFormsHost> gli elementi vengono sempre tracciati sopra altro  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] gli elementi e che non vengono influenzati dall'ordine z.  Per abilitare l'ordine z, impostare <xref:System.Windows.Interop.HwndHost.IsRedirected%2A> proprietà di  <xref:System.Windows.Forms.Integration.WindowsFormsHost> per allineare e  <xref:System.Windows.Interop.HwndHost.CompositionMode%2A> proprietà di  <xref:System.Windows.Interop.CompositionMode.Full> o  <xref:System.Windows.Interop.CompositionMode.OutputOnly>.  
  
#### Per visualizzare il comportamento predefinito dell'ordine z  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#8)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> viene disegnato sopra l'elemento etichetta.  
  
#### Per visualizzare il comportamento dell'ordine z quando IsRedirected è true  
  
1.  Sostituire l'esempio precedente dell'ordine z con il codice XAML seguente.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#8b](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml#8b)]  
  
     Premere F5 per compilare ed eseguire l'applicazione.  L'elemento etichetta viene disegnato sopra <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento.  
  
## Ancoraggio  
 L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> supporta l'ancoraggio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Impostare la proprietà associata <xref:System.Windows.Controls.DockPanel.Dock%2A> per ancorare il controllo ospitato in un elemento <xref:System.Windows.Controls.DockPanel>.  
  
#### Per ancorare un controllo ospitato  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#9)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> viene ancorato al lato destro dell'elemento <xref:System.Windows.Controls.DockPanel>.  
  
## Impostazione della visibilità  
 È possibile rendere il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] invisibile o comprimerlo impostando la proprietà <xref:System.Windows.UIElement.Visibility%2A> dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  Quando un controllo non è visibile, non viene visualizzato ma occupa spazio del layout.  Quando un controllo è compresso, non viene visualizzato né occupa spazio del layout.  
  
#### Per impostare la visibilità di un controllo ospitato  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#10)]  
  
2.  In MainWindow.xaml.vb o MainWindow.xaml.cs copiare il codice seguente nella definizione della classe.  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#102)]
     [!code-vb[WpfLayoutHostingWfWithXaml#102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#102)]  
  
3.  Premere F5 per compilare ed eseguire l'applicazione.  
  
4.  Fare clic sul pulsante **Fare clic per rendere invisibile** per rendere invisibile l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
5.  Fare clic sul pulsante **Fare clic per comprimere** per nascondere completamente l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> dal layout.  Dopo avere compresso il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], gli elementi circostanti vengono ridisposti per occuparne lo spazio.  
  
## Hosting di un controllo che non si adatta  
 Alcuni controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] hanno una dimensione fissa e non si adattano per occupare lo spazio disponibile nel layout.  Ad esempio il controllo <xref:System.Windows.Forms.MonthCalendar> consente di visualizzare un mese in uno spazio fisso.  
  
#### Per ospitare un controllo che non si adatta  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#11)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> viene centrato nella riga della griglia, ma non si adatta per occupare lo spazio disponibile.  Se la finestra è sufficientemente grande, potrebbero essere visibili due o più mesi tramite il controllo <xref:System.Windows.Forms.MonthCalendar> ospitato, ma saranno centrati nella riga.  Il motore di layout [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] centra gli elementi che non possono essere ridimensionati per occupare lo spazio disponibile.  
  
## Ridimensionamento  
 A differenza degli elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la maggior parte dei controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non è continuamente ridimensionabile.  per impostazione predefinita, <xref:System.Windows.Forms.Integration.WindowsFormsHost> l'elemento ridimensiona il controllo ospitato quando possibile.  Per abilitare gli esperta ridimensionamento, impostare <xref:System.Windows.Interop.HwndHost.IsRedirected%2A> proprietà di  <xref:System.Windows.Forms.Integration.WindowsFormsHost> per allineare e  <xref:System.Windows.Interop.HwndHost.CompositionMode%2A> proprietà di  <xref:System.Windows.Interop.CompositionMode.Full> o  <xref:System.Windows.Interop.CompositionMode.OutputOnly>.  
  
#### Per ridimensionare un controllo ospitato utilizzando il comportamento predefinito  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#12)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  Il controllo ospitato e gli elementi che lo circondano vengono ridimensionati in base a un fattore di 0,5.  Tuttavia il tipo di carattere del controllo ospitato non viene ridimensionato.  
  
#### Per ridimensionare un controllo ospitato impostando IsRedirected per allineare  
  
1.  Sostituire l'esempio precedente di ridimensionamento con il codice XAML seguente.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#12b](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml#12b)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  Il controllo ospitato, gli elementi che lo circondano e il tipo del controllo ospitato viene ridimensionato in base a un fattore di 0,5.  
  
## Rotazione  
 A differenza degli elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non supportano la rotazione.  per impostazione predefinita, <xref:System.Windows.Forms.Integration.WindowsFormsHost> l'elemento non ruota con altro  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elementi quando viene applicata una trasformazione di rotazione.  Qualsiasi valore di rotazione diverso da 180 gradi genera l'evento <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError>.  Per abilitare lo spin in qualsiasi angolo, impostare <xref:System.Windows.Interop.HwndHost.IsRedirected%2A> proprietà di  <xref:System.Windows.Forms.Integration.WindowsFormsHost> per allineare e  <xref:System.Windows.Interop.HwndHost.CompositionMode%2A> proprietà di  <xref:System.Windows.Interop.CompositionMode.Full> o  <xref:System.Windows.Interop.CompositionMode.OutputOnly>.  
  
#### Per verificare l'effetto della rotazione in un'applicazione ibrida  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#13)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  Il controllo ospitato non viene ruotato, ma gli elementi che lo circondano vengono ruotati in base a un angolo di 180 gradi.  Potrebbe essere necessario ridimensionare la finestra per vedere gli elementi.  
  
#### Per visualizzare l'effetto della rotazione in un'applicazione ibrida quando IsRedirected è true  
  
1.  Sostituire l'esempio precedente di rotazione con il codice XAML seguente.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#13b](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml#13b)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  Il controllo ospitato viene ruotato.  si noti che <xref:System.Windows.Media.RotateTransform.Angle%2A> la proprietà può essere impostata su qualsiasi valore.  Potrebbe essere necessario ridimensionare la finestra per vedere gli elementi.  
  
## Impostazione della spaziatura interna e dei margini  
 La spaziatura interna e i margini nel layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono simili alla spaziatura interna e ai margini in [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  Impostare semplicemente le proprietà <xref:System.Windows.Controls.Control.Padding%2A> e <xref:System.Windows.FrameworkElement.Margin%2A> nell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
#### Per impostare la spaziatura interna e i margini per un controllo ospitato  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#14)]  
    [!code-xml[WpfLayoutHostingWfWithXaml#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#15)]  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  Le impostazioni della spaziatura interna e dei margini vengono applicate ai controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitati nello stesso modo in cui verrebbero applicate in [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
## Utilizzo di contenitori di layout dinamici  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] fornisce due contenitori di layout dinamici, <xref:System.Windows.Forms.FlowLayoutPanel> e <xref:System.Windows.Forms.TableLayoutPanel>.  È anche possibile utilizzare questi contenitori nei layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
#### Per utilizzare un contenitore di layout dinamico  
  
1.  Copiare il codice XAML riportato di seguito nell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#16)]  
  
2.  In MainWindow.xaml.vb o MainWindow.xaml.cs copiare il codice seguente nella definizione della classe.  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#103)]
     [!code-vb[WpfLayoutHostingWfWithXaml#103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#103)]  
  
3.  Aggiungere nel costruttore una chiamata al metodo `InitializeFlowLayoutPanel`.  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#104)]
     [!code-vb[WpfLayoutHostingWfWithXaml#104](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#104)]  
  
4.  Premere F5 per compilare ed eseguire l'applicazione.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> occupa <xref:System.Windows.Controls.DockPanel> e <xref:System.Windows.Forms.FlowLayoutPanel> dispone i controlli figlio nell'oggetto <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> predefinito.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Considerazioni sul layout per l'elemento WindowsFormsHost](../../../../docs/framework/wpf/advanced/layout-considerations-for-the-windowsformshost-element.md)   
 [Esempio di disposizione di controlli Windows Form in WPF](http://go.microsoft.com/fwlink/?LinkId=159971)   
 [Procedura dettagliata: hosting di controlli Windows Form compositi in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)