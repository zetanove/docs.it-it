---
title: "Procedura: attivare stili di visualizzazione in un&#39;applicazione ibrida | Microsoft Docs"
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
  - "applicazioni ibride [interoperabilità WPF]"
  - "stili visivi [Windows Form]"
ms.assetid: 95de9b9c-d804-405c-b2d1-49a88c1e0fe1
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: attivare stili di visualizzazione in un&#39;applicazione ibrida
In questo argomento viene illustrato come abilitare gli stili di visualizzazione di [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] su un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato in un'applicazione basata su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Se l'applicazione chiama il metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>, la maggior parte dei controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] utilizzerà automaticamente gli stili di visualizzazione quando l'applicazione viene eseguita in [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)].  Per ulteriori informazioni, vedere [Rendering dei controlli con stili visivi](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md).  
  
 Per un elenco di codice completo delle attività illustrate in questo argomento, vedere [Esempio di abilitazione di stili di visualizzazione in un'applicazione ibrida](http://go.microsoft.com/fwlink/?LinkID=159986) \(la pagina potrebbe essere in inglese\).  
  
## Abilitazione degli stili di visualizzazione Windows Forms  
  
#### Per abilitare gli stili di visualizzazione Windows Forms  
  
1.  Creare un progetto dell'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] denominato `HostingWfWithVisualStyles`.  
  
2.  In Esplora soluzioni aggiungere riferimenti agli assembly indicati di seguito.  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
3.  Nella Casella degli strumenti fare doppio clic sull'icona <xref:System.Windows.Controls.Grid> per inserire un elemento <xref:System.Windows.Controls.Grid> nell'area di progettazione.  
  
4.  Nella finestra Proprietà impostare i valori delle proprietà <xref:System.Windows.FrameworkElement.Height%2A> e <xref:System.Windows.FrameworkElement.Width%2A> su **Auto**.  
  
5.  In visualizzazione Progettazione, selezionare l'oggetto <xref:System.Windows.Window>.  
  
6.  Nella finestra Proprietà fare clic sulla scheda **Eventi**.  
  
7.  Fare doppio clic sull'evento <xref:System.Windows.FrameworkElement.Loaded>.  
  
8.  In MainWindow.xaml.vb o MainWindow.xaml.cs inserire il codice seguente per gestire l'evento <xref:System.Windows.FrameworkElement.Loaded>.  
  
     [!code-csharp[HostingWfWithVisualStyles#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWfWithVisualStyles/CSharp/HostingWfWithVisualStyles/Window1.xaml.cs#11)]
     [!code-vb[HostingWfWithVisualStyles#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfWithVisualStyles/VisualBasic/HostingWfWithVisualStyles/Window1.xaml.vb#11)]  
  
9. Premere F5 per compilare ed eseguire l'applicazione.  
  
     Il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] viene disegnato con gli stili di visualizzazione.  
  
## Disabilitazione degli stili di visualizzazione Windows Forms  
 Per disabilitare gli stili di visualizzazione, rimuovere semplicemente la chiamata al metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>.  
  
#### Per disabilitare gli stili di visualizzazione Windows Forms  
  
1.  Nell'editor di codice aprire MainWindow.xaml.vb o MainWindow.xaml.cs.  
  
2.  Impostare la chiamata come commento al metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>.  
  
3.  Premere F5 per compilare ed eseguire l'applicazione.  
  
     Il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] viene disegnato con lo stile predefinito di sistema.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>   
 <xref:System.Windows.Forms.VisualStyles>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Rendering dei controlli con stili visivi](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)   
 [Procedura dettagliata: hosting di controlli Windows Form in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)