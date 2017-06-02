---
title: "Procedura dettagliata: hosting di un controllo ActiveX in WPF | Microsoft Docs"
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
  - "Active X (controlli) [interoperabilità WPF]"
  - "hosting di controlli ActiveX"
ms.assetid: 1931d292-0dd1-434f-963c-dcda7638d75a
caps.latest.revision: 30
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# Procedura dettagliata: hosting di un controllo ActiveX in WPF
Per migliorare l'interazione con i browser, è possibile utilizzare i controlli [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] nelle applicazioni basate su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  In questa procedura dettagliata viene illustrato come ospitare [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] come controllo in una pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione del progetto.  
  
-   Creazione del controllo ActiveX.  
  
-   Hosting del controllo ActiveX in una pagina WPF.  
  
 Dopo avere completato questa procedura dettagliata, si sarà in grado di utilizzare i controlli [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] in un applicazione basata su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] installato nel computer in cui è installato [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
## Creazione del progetto  
  
#### Per creare e configurare il progetto  
  
1.  Creare un progetto di applicazione WPF denominato `HostingAxInWpf`.  
  
2.  Aggiungere un progetto Libreria di controlli Windows Form alla soluzione e denominare il progetto `WmpAxLib`.  
  
3.  Nel progetto WmpAxLib aggiungere un riferimento all'assembly Windows Media Player denominato wmp.dll.  
  
4.  Aprire la **Casella degli strumenti**.  
  
5.  Fare clic con il pulsante destro del mouse sulla **Casella degli strumenti** e fare clic su **Scegli elementi**.  
  
6.  Fare clic sulla scheda **Componenti COM** selezionare il controllo **Windows Media Player**, quindi fare clic su **OK**.  
  
     Il controllo Windows Media Player viene aggiunto alla **Casella degli strumenti**.  
  
7.  In Esplora soluzioni, fare clic con il pulsante destro del mouse sul file **UserControl1**, quindi scegliere **Rinomina**.  
  
8.  Impostare il nome su `WmpAxControl.vb` o su `WmpAxControl.cs`, a seconda del linguaggio.  
  
9. Se viene chiesto di rinominare tutti i riferimenti, scegliere **Sì**.  
  
## Creazione del controllo ActiveX  
 In [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] viene automaticamente generata una classe wrapper <xref:System.Windows.Forms.AxHost> per un controllo [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] quando il controllo viene aggiunto in un'area di progettazione.  La procedura descritta di seguito consente di creare un assembly gestito denominato AxInterop.WMPLib.dll.  
  
#### Per creare il controllo ActiveX  
  
1.  Aprire WmpAxControl.vb o WmpAxControl.cs in Progettazione Windows Form.  
  
2.  Dalla **Casella degli strumenti** aggiungere il controllo Windows Media Player all'area di progettazione.  
  
3.  Nella finestra Proprietà impostare il valore della proprietà <xref:System.Windows.Forms.Control.Dock%2A> del controllo Windows Media Player su <xref:System.Windows.Forms.DockStyle>.  
  
4.  Compilare il progetto di libreria di controlli WmpAxLib.  
  
## Hosting del controllo ActiveX in una pagina WPF.  
  
#### Per ospitare il controllo ActiveX  
  
1.  Nel progetto HostingAxInWpf, aggiungere un riferimento all'assembly di interoperabilità [!INCLUDE[TLA2#tla_actx](../../../../includes/tla2sharptla-actx-md.md)] generato.  
  
     Questo assembly è denominato AxInterop.WMPLib.dll ed è stato aggiunto alla cartella Debug del progetto WmpAxLib al momento dell'importazione del controllo Windows Media Player.  
  
2.  Aggiungere un riferimento all'assembly WindowsFormsIntegration, denominato WindowsFormsIntegration.dll.  
  
3.  Aggiungere un riferimento all'assembly [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], denominato System.Windows.Forms.dll.  
  
4.  Aprire MainWindow.xaml nella finestra di progettazione WPF.  
  
5.  Denominare l'elemento <xref:System.Windows.Controls.Grid> `grid1`.  
  
     [!code-xml[HostingAxInWpf#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml#1)]  
  
6.  In visualizzazione Progettazione o XAML selezionare l'elemento <xref:System.Windows.Window>.  
  
7.  Nella finestra Proprietà fare clic sulla scheda **Eventi**.  
  
8.  Fare doppio clic sull'evento <xref:System.Windows.FrameworkElement.Loaded>.  
  
9. Inserire il codice riportato di seguito per gestire l'evento <xref:System.Windows.FrameworkElement.Loaded>.  
  
     Tramite questo codice viene creata un'istanza del controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> e viene aggiunta un'istanza del controllo `AxWindowsMediaPlayer` come relativo elemento figlio.  
  
     [!code-csharp[HostingAxInWpf#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml.cs#11)]
     [!code-vb[HostingAxInWpf#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HostingAxInWpf/VisualBasic/HostingAxInWpf/window1.xaml.vb#11)]  
  
10. Premere F5 per compilare ed eseguire l'applicazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Procedura dettagliata: hosting di controlli Windows Form compositi in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)