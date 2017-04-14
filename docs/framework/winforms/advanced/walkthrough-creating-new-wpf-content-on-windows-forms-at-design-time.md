---
title: "Procedura dettagliata: creazione di nuovo contenuto WPF in Windows Form in fase di progettazione | Microsoft Docs"
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
  - "controllo ElementHost"
  - "hosting di contenuto WPF in Windows Form"
  - "interoperabilità, WPF e Windows Form"
  - "contenuto WPF, hosting in Windows Form"
  - "controllo utente WPF, hosting in Windows Form"
ms.assetid: 2e92d8e8-f0e4-4df7-9f07-2acf35cd798c
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Procedura dettagliata: creazione di nuovo contenuto WPF in Windows Form in fase di progettazione
Questo argomento descrive come creare un controllo Windows Presentation Foundation \(WPF\) da usare nelle applicazioni basate su Windows Form.  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   Creare il progetto.  
  
-   Creare un nuovo controllo WPF.  
  
-   Aggiungere il nuovo controllo WPF a un Windows Form.  Il controllo WPF è ospitato in un controllo <xref:System.Windows.Forms.Integration.ElementHost>.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  
  
## Creazione del progetto  
 Il primo passaggio consiste nella creazione del progetto Windows Form.  
  
> [!NOTE]
>  Con il contenuto WPF sono supportati solo progetti C\# e Visual Basic.  
  
#### Per creare il progetto  
  
-   Creare un nuovo progetto di applicazione Windows Form in Visual Basic o Visual C\# denominato `HostingWpf`.  
  
## Creazione di un nuovo controllo WPF  
 Creare un nuovo controllo WPF e aggiungerlo al progetto è facile come aggiungere qualsiasi altro elemento.   Progettazione Windows Form usa un particolare tipo di controllo denominato *controllo composito* o *controllo utente*.  Per altre informazioni sui controlli utente WPF, vedere <xref:System.Windows.Controls.UserControl>.  
  
> [!NOTE]
>  Il tipo <xref:System.Windows.Controls.UserControl?displayProperty=fullName> per WPF è distinto dal tipo di controllo utente fornito da Windows Form, denominato anch'esso <xref:System.Windows.Forms.UserControl?displayProperty=fullName>.  
  
#### Per creare un nuovo controllo WPF.  
  
1.  In **Esplora soluzioni** aggiungere un nuovo progetto di **Libreria di controlli utente WPF** alla soluzione.  Usare il nome predefinito per la libreria di controlli, `WpfControlLibrary1`.  Il nome predefinito del controllo è `UserControl1.xaml`.  
  
     L'aggiunta del nuovo controllo ha gli effetti seguenti:  
  
    -   Viene aggiunto il file UserControl1.xaml.  
  
    -   Viene aggiunto il file UserControl1.xaml.cs o UserControl1.xaml.vb.  Questo file contiene il code\-behind per i gestori eventi e l'altra implementazione.  
  
    -   Vengono aggiunti riferimenti agli assembly WPF.  
  
    -   Il file UserControl1.xaml viene aperto in [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)].  
  
2.  In visualizzazione Progettazione verificare che `UserControl1` sia selezionato.  Per altre informazioni, vedere [Procedura: selezionare e spostare elementi sull'area di progettazione](http://msdn.microsoft.com/it-it/54cb70b6-b35b-46e4-a0cc-65189399c474).  
  
3.  Nella finestra **Proprietà** impostare il valore delle proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> su `200`.  
  
4.  Trascinare un controllo <xref:System.Windows.Controls.TextBox?displayProperty=fullName> nell'area di progettazione dalla **Casella degli strumenti**.  
  
5.  Nella finestra **Proprietà** impostare il valore della proprietà <xref:System.Windows.Controls.TextBox.Text%2A> su Hosted Content.  
  
    > [!NOTE]
    >  In generale, è opportuno ospitare contenuto WPF più sofisticato.  Il controllo <xref:System.Windows.Controls.TextBox?displayProperty=fullName> è qui usato a solo a titolo esemplificativo.  
  
6.  Compilare il progetto.  
  
## Aggiunta di un controllo WPF a un Windows Form  
 Il nuovo controllo WPF è pronto per l'uso sul form.  Windows Forms usa il controllo <xref:System.Windows.Forms.Integration.ElementHost> per ospitare contenuto WPF  
  
#### Per aggiungere un controllo WPF a un Windows Form  
  
1.  Aprire `Form1` in Progettazione Windows Form.  
  
2.  Nella **Casella degli strumenti** individuare la scheda con etichetta **Controlli utente WPF WPFUserControlLibrary**.  
  
3.  Trascinare un'istanza di `UserControl1` sul form.  
  
    -   Un controllo <xref:System.Windows.Forms.Integration.ElementHost> verrà creato automaticamente sul form per ospitare il controllo WPF.  
  
    -   Il controllo <xref:System.Windows.Forms.Integration.ElementHost> viene denominato `elementHost1` e nella finestra **Proprietà** è possibile visualizzare la relativa proprietà <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> impostata su **UserControl1**.  
  
    -   I riferimenti agli assembly WPF vengono aggiunti al progetto.  
  
    -   Il controllo `elementHost1` include un pannello smart tag che mostra le opzioni di hosting disponibili.  
  
4.  Nel pannello smart tag **ElementHost Tasks** selezionare **Ancora nel contenitore padre**.  
  
5.  Premere F5 per compilare ed eseguire l'applicazione.  
  
## Passaggi successivi  
 Windows Form e WPF sono tecnologie diverse progettate per interagire strettamente.  Per migliorare l'aspetto e il comportamento nelle applicazioni, provare le operazioni seguenti.  
  
-   Ospitare un controllo Windows Form in una pagina WPF.  Per altre informazioni, vedere [Procedura dettagliata: hosting di controlli Windows Form in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md).  
  
-   Applicare stili di visualizzazione Windows Form al contenuto WPF.  Per altre informazioni, vedere [Procedura: attivare stili di visualizzazione in un'applicazione ibrida](../../../../docs/framework/wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md).  
  
-   Modificare lo stile del contenuto WPF.  Per altre informazioni, vedere [Procedura dettagliata: applicazione di stili al contenuto WPF](../../../../docs/framework/winforms/advanced/walkthrough-styling-wpf-content.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [Utilizzo di controlli WPF](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)