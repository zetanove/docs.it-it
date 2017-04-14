---
title: "Procedura dettagliata: hosting di controlli Windows Form in WPF | Microsoft Docs"
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
  - "hosting di controlli Windows Form in WPF"
ms.assetid: 9cb88415-39b0-4c46-80c4-ff325b674286
caps.latest.revision: 36
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# Procedura dettagliata: hosting di controlli Windows Form in WPF
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce numerosi controlli con un'ampia gamma di funzionalità.  Talvolta si potrebbero tuttavia utilizzare i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] nelle pagine [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  È ad esempio possibile avere un investimento sostanziale in controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] esistenti o è possibile disporre di un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che fornisce funzionalità univoche.  
  
 In questa procedura dettagliata viene illustrato come eseguire l'hosting di un controllo <xref:System.Windows.Forms.MaskedTextBox?displayProperty=fullName> [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] in una pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] tramite codice.  
  
 Per un elenco di codice completo delle attività illustrate in questa procedura dettagliata, vedere [Esempio di hosting di controlli Windows Form in WPF](http://go.microsoft.com/fwlink/?LinkID=160057) \(la pagina potrebbe essere in inglese\).  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
## Hosting di un controllo Windows Form  
  
#### Per ospitare il controllo MaskedTextBox  
  
1.  Creare un progetto di applicazione WPF denominato `HostingWfInWpf`.  
  
2.  Aggiungere riferimenti agli assembly riportati di seguito.  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
3.  Aprire MainWindow.xaml in [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
4.  Denominare l'elemento <xref:System.Windows.Controls.Grid> `grid1`.  
  
     [!code-xml[HostingWfInWPF#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml#1)]  
  
5.  In visualizzazione Progettazione o XAML selezionare l'elemento <xref:System.Windows.Window>.  
  
6.  Nella finestra Proprietà fare clic sulla scheda **Eventi**.  
  
7.  Fare doppio clic sull'evento <xref:System.Windows.FrameworkElement.Loaded>.  
  
8.  Inserire il codice riportato di seguito per gestire l'evento <xref:System.Windows.FrameworkElement.Loaded>.  
  
     [!code-csharp[HostingWfInWPF#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml.cs#10)]
     [!code-vb[HostingWfInWPF#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfInWPF/VisualBasic/HostingWfInWpf/Window1.xaml.vb#10)]  
  
9. All'inizio del file, aggiungere l'istruzione `Imports` o `using` seguente.  
  
     [!code-csharp[HostingWfInWPF#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml.cs#11)]
     [!code-vb[HostingWfInWPF#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfInWPF/VisualBasic/HostingWfInWpf/Window1.xaml.vb#11)]  
  
10. Premere F5 per compilare ed eseguire l'applicazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Procedura dettagliata: hosting di controlli Windows Form in WPF tramite XAML](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf-by-using-xaml.md)   
 [Procedura dettagliata: hosting di controlli Windows Form compositi in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)   
 [Controlli Windows Form e controlli WPF equivalenti](../../../../docs/framework/wpf/advanced/windows-forms-controls-and-equivalent-wpf-controls.md)   
 [Esempio di hosting di controlli Windows Form in WPF](http://go.microsoft.com/fwlink/?LinkID=160057)