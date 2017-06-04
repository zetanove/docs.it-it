---
title: "Procedura dettagliata: associazione ai dati in applicazioni ibride | Microsoft Docs"
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
  - "associazione dati [interoperabilità WPF]"
  - "applicazioni ibride [interoperabilità WPF]"
ms.assetid: 18997e71-745a-4425-9c69-2cbce1d8669e
caps.latest.revision: 39
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 36
---
# Procedura dettagliata: associazione ai dati in applicazioni ibride
L'associazione di un'origine dati a un controllo è fondamentale per fornire agli utenti l'accesso ai dati sottostanti, sia che si utilizzi [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  In questa procedura dettagliata viene illustrato come utilizzare l’associazione dati in applicazioni ibride che includono controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione del progetto.  
  
-   Definizione del modello di dati.  
  
-   Definizione del layout del form.  
  
-   Definizione delle associazioni dati.  
  
-   Visualizzazione dei dati utilizzando l'interoperabilità.  
  
-   Aggiunta dell'origine dati al progetto.  
  
-   Associazione all'origine dati.  
  
 Per un elenco di codice completo delle attività illustrate in questa procedura dettagliata, vedere [Esempio di associazione dati in applicazioni ibride](http://go.microsoft.com/fwlink/?LinkID=159983) \(la pagina potrebbe essere in inglese\).  
  
 Questa procedura consente di approfondire le funzionalità dell'associazione dati nelle applicazioni ibride.  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
-   Accedere al database di esempio Northwind eseguito in Microsoft SQL Server.  
  
## Creazione del progetto  
  
#### Per creare e configurare il progetto  
  
1.  Creare un progetto di applicazione WPF denominato `WPFWithWFAndDatabinding`.  
  
2.  In Esplora soluzioni aggiungere riferimenti agli assembly indicati di seguito.  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
3.  Aprire MainWindow.xaml in [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
4.  Nell'elemento <xref:System.Windows.Window> aggiungere il mapping degli spazi dei nomi [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] seguente.  
  
    ```xaml  
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"  
    ```  
  
5.  Denominare l'elemento <xref:System.Windows.Controls.Grid> predefinito `mainGrid` assegnando la proprietà <xref:System.Windows.FrameworkElement.Name%2A>.  
  
     [!code-xml[WPFWithWFAndDatabinding#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#8)]  
  
## Definizione del modello di dati  
 L'elenco principale di clienti viene visualizzato in un controllo <xref:System.Windows.Controls.ListBox>.  Nell'esempio di codice riportato di seguito viene definito un oggetto <xref:System.Windows.DataTemplate> denominato `ListItemsTemplate` che controlla la struttura ad albero visuale del controllo <xref:System.Windows.Controls.ListBox>.  Questo oggetto <xref:System.Windows.DataTemplate> viene assegnato alla proprietà <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> del controllo <xref:System.Windows.Controls.ListBox>.  
  
#### Per definire il modello di dati  
  
-   Copiare il codice XAML seguente nella dichiarazione dell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WPFWithWFAndDatabinding#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#3)]  
  
## Definizione del layout del form  
 Il layout del form è definito da una griglia con tre righe e tre colonne.  I controlli <xref:System.Windows.Controls.Label> sono forniti per identificare ogni colonna nella tabella Customers.  
  
#### Per impostare il layout della griglia  
  
-   Copiare il codice XAML seguente nella dichiarazione dell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WPFWithWFAndDatabinding#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#4)]  
  
#### Per configurare i controlli Label  
  
-   Copiare il codice XAML seguente nella dichiarazione dell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WPFWithWFAndDatabinding#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#5)]  
  
## Definizione delle associazioni dati  
 L'elenco principale di clienti viene visualizzato in un controllo <xref:System.Windows.Controls.ListBox>.  L'oggetto `ListItemsTemplate` collegato associa un controllo <xref:System.Windows.Controls.TextBlock> al campo `ContactName` del database.  
  
 I dettagli di ogni record cliente vengono visualizzati in molti controlli <xref:System.Windows.Controls.TextBox>.  
  
#### Per definire le associazioni dati  
  
-   Copiare il codice XAML seguente nella dichiarazione dell'elemento <xref:System.Windows.Controls.Grid>.  
  
     La classe <xref:System.Windows.Data.Binding> associa i controlli <xref:System.Windows.Controls.TextBox> ai campi appropriati del database.  
  
     [!code-xml[WPFWithWFAndDatabinding#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#6)]  
  
## Visualizzazione dei dati utilizzando l'interazione  
 Gli ordini corrispondenti al cliente selezionato vengono visualizzati in un controllo <xref:System.Windows.Forms.DataGridView?displayProperty=fullName> denominato `dataGridView1`.  Il controllo `dataGridView1` è associato all'origine dati nel file code\-behind.  Un controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> è l'elemento padre di questo controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
#### Per visualizzare dati nel controllo DataGridView  
  
-   Copiare il codice XAML seguente nella dichiarazione dell'elemento <xref:System.Windows.Controls.Grid>.  
  
     [!code-xml[WPFWithWFAndDatabinding#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#7)]  
  
## Aggiunta dell'origine dati al progetto  
 In [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] è possibile aggiungere con facilità un'origine dati al progetto.  Tramite questa procedura viene aggiunto un dataset fortemente tipizzato al progetto.  Vengono inoltre aggiunte altre classi di supporto, ad esempio adattatori di tabella per ognuna delle tabelle scelte.  
  
#### Per aggiungere l'origine dati  
  
1.  Scegliere **Aggiungi nuova origine dati** dal menu **Dati**.  
  
2.  Nella **Configurazione guidata origine dati** creare una connessione al database Northwind utilizzando un dataset.  Per ulteriori informazioni, vedere [Procedura: connettersi ai dati di un database](../Topic/How%20to:%20Connect%20to%20Data%20in%20a%20Database.md).  
  
3.  Quando viene richiesto da **Configurazione guidata origine dati**, salvare la stringa di connessione come `NorthwindConnectionString`.  
  
4.  Quando viene richiesto di scegliere gli oggetti di database, selezionare le tabelle `Customers` e `Orders` e denominare il dataset generato `NorthwindDataSet`.  
  
## Associazione all'origine dati  
 Il componente <xref:System.Windows.Forms.BindingSource?displayProperty=fullName> fornisce un'interfaccia uniforme per l'origine dati dell'applicazione.  L'associazione all'origine dati è implementata nel file code\-behind.  
  
#### Per eseguire l'associazione all'origine dati  
  
1.  Aprire il file code\-behind denominato MainWindow.xaml.vb o MainWindow.xaml.cs.  
  
2.  Copiare il codice riportato di seguito nella definizione della classe `MainWindow`.  
  
     In questo codice viene dichiarato il componente <xref:System.Windows.Forms.BindingSource> e classi di supporto associate per la connessione al database.  
  
     [!code-csharp[WPFWithWFAndDatabinding#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#11)]
     [!code-vb[WPFWithWFAndDatabinding#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#11)]  
  
3.  Copiare il codice riportato di seguito nel costruttore.  
  
     Tramite questo codice viene creato e inizializzato il componente <xref:System.Windows.Forms.BindingSource>.  
  
     [!code-csharp[WPFWithWFAndDatabinding#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#12)]
     [!code-vb[WPFWithWFAndDatabinding#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#12)]  
  
4.  Aprire MainWindow.xaml.  
  
5.  In visualizzazione Progettazione o XAML selezionare l'elemento <xref:System.Windows.Window>.  
  
6.  Nella finestra Proprietà fare clic sulla scheda **Eventi**.  
  
7.  Fare doppio clic sull'evento <xref:System.Windows.FrameworkElement.Loaded>.  
  
8.  Copiare il codice riportato di seguito nel gestore eventi <xref:System.Windows.FrameworkElement.Loaded>:  
  
     Mediante questo codice viene assegnato il componente <xref:System.Windows.Forms.BindingSource> come contesto dati e vengono compilati gli oggetti adattatore `Customers` e `Orders`.  
  
     [!code-csharp[WPFWithWFAndDatabinding#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#13)]
     [!code-vb[WPFWithWFAndDatabinding#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#13)]  
  
9. Copiare il codice riportato di seguito nella definizione della classe `MainWindow`.  
  
     Questo metodo gestisce l'evento <xref:System.Windows.Data.CollectionView.CurrentChanged> e aggiorna l'elemento corrente dell'associazione dati.  
  
     [!code-csharp[WPFWithWFAndDatabinding#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#14)]
     [!code-vb[WPFWithWFAndDatabinding#14](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#14)]  
  
10. Premere F5 per compilare ed eseguire l'applicazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Esempio di associazione dati in applicazioni ibride](http://go.microsoft.com/fwlink/?LinkID=159983)   
 [Procedura dettagliata: hosting di controlli Windows Form compositi in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)