---
title: "Procedura: creare un componente aggiuntivo che restituisce un&#39;interfaccia utente | Microsoft Docs"
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
  - "componente aggiuntivo [WPF], restituzione di un'interfaccia utente"
  - "creazione di un componente aggiuntivo che restituisce un'interfaccia utente [WPF]"
  - "implementazione dei segmenti della pipeline del componente aggiuntivo [WPF]"
ms.assetid: 57f274b7-4c66-4b72-92eb-81939a393776
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: creare un componente aggiuntivo che restituisce un&#39;interfaccia utente
In questo esempio viene illustrato come creare un componente aggiuntivo che restituisce un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] di [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] a un'applicazione host [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] autonoma.  
  
 Il componente aggiuntivo restituisce un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] che rappresenta un controllo utente di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Il contenuto del controllo utente è costituito da un unico pulsante che consente di visualizzare una finestra di messaggio.  Nell'applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] autonoma viene ospitato il componente aggiuntivo e visualizzato il controllo utente, restituito da quest'ultimo, come contenuto della finestra principale dell'applicazione.  
  
 **Prerequisiti**  
  
 In questo esempio vengono evidenziate le estensioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] al modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] responsabile dell'abilitazione di tale scenario e si presuppongono le seguenti condizioni:  
  
-   Conoscenza del modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], incluso lo sviluppo di pipeline, componenti aggiuntivi e host.  Per informazioni su questi concetti, vedere [Componenti aggiuntivi ed estensibilità](../../../../ml/index.xml).  Per un'esercitazione in cui venga illustrata l'implementazione di una pipeline, un componente aggiuntivo e un'applicazione host, vedere [Procedura dettagliata: creazione di un'applicazione estendibile](../Topic/Walkthrough:%20Creating%20an%20Extensible%20Application.md).  
  
-   Conoscenza delle estensioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] al modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], disponibile in: [Cenni preliminari sui componenti aggiuntivi di WPF](../../../../docs/framework/wpf/app-development/wpf-add-ins-overview.md).  
  
## Esempio  
 La creazione di un componente aggiuntivo che restituisce un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] richiede l'utilizzo di codice specifico per ciascun segmento di pipeline, per il componente aggiuntivo e per l'applicazione host.  
  
   
  
<a name="Contract"></a>   
## Implementazione del segmento di pipeline di contratto  
 Per poter restituire un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], un metodo deve essere definito dal contratto e il relativo valore restituito deve essere di tipo <xref:System.AddIn.Contract.INativeHandleContract>,  come illustrato dal metodo `GetAddInUI` del contratto `IWPFAddInContract` nel codice seguente.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#ContractCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/Contracts/IWPFAddInContract.cs#contractcode)]
 [!code-vb[SimpleAddInReturnsAUISample#ContractCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/Contracts/IWPFAddInContract.vb#contractcode)]  
  
<a name="AddInView"></a>   
## Implementazione del segmento di pipeline di visualizzazione del componente aggiuntivo  
 Poiché il componente aggiuntivo implementa le [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] fornite come sottoclassi di <xref:System.Windows.FrameworkElement>, il metodo nella visualizzazione del componente aggiuntivo correlata a `IWPFAddInView.GetAddInUI` deve restituire un valore di tipo <xref:System.Windows.FrameworkElement>.  Nel codice riportato di seguito viene illustrata la visualizzazione del componente aggiuntivo del contratto, implementata come interfaccia.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInViewCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/AddInViews/IWPFAddInView.cs#addinviewcode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInViewCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/AddInViews/IWPFAddInView.vb#addinviewcode)]  
  
<a name="AddInSideAdapter"></a>   
## Implementazione del segmento di pipeline dell'adattatore sul lato componente aggiuntivo  
 Il metodo del contratto restituisce <xref:System.AddIn.Contract.INativeHandleContract>, ma il componente aggiuntivo restituisce <xref:System.Windows.FrameworkElement>, come specificato dalla visualizzazione del componente.  Di conseguenza, l'oggetto <xref:System.Windows.FrameworkElement> deve essere convertito in <xref:System.AddIn.Contract.INativeHandleContract> prima di oltrepassare il limite di isolamento.  La conversione viene eseguita dall'adattatore sul lato componente aggiuntivo mediante una chiamata a <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>, come illustrato nel codice seguente.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInSideAdapterCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.cs#addinsideadaptercode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInSideAdapterCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.vb#addinsideadaptercode)]  
  
<a name="HostView"></a>   
## Implementazione del segmento di pipeline di visualizzazione host  
 Poiché l'applicazione host visualizzerà <xref:System.Windows.FrameworkElement>, il metodo nella visualizzazione host correlata a `IWPFAddInHostView.GetAddInUI` deve restituire un valore di tipo <xref:System.Windows.FrameworkElement>.  Nel codice riportato di seguito viene illustrata la visualizzazione host del contratto, implementata come interfaccia.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#HostViewCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/HostViews/IWPFAddInHostView.cs#hostviewcode)]
 [!code-vb[SimpleAddInReturnsAUISample#HostViewCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/HostViews/IWPFAddInHostView.vb#hostviewcode)]  
  
<a name="HostSideAdapter"></a>   
## Implementazione del segmento di pipeline dell'adattatore sul lato host  
 Il metodo del contratto restituisce <xref:System.AddIn.Contract.INativeHandleContract>, ma l'applicazione host prevede <xref:System.Windows.FrameworkElement>, come specificato dalla visualizzazione host.  Di conseguenza, l'oggetto <xref:System.AddIn.Contract.INativeHandleContract> deve essere convertito in <xref:System.Windows.FrameworkElement> dopo aver oltrepassato il limite di isolamento.  La conversione viene eseguita dall'adattatore sul lato host mediante una chiamata a <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>, come illustrato nel codice seguente.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#HostSideAdapterCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.cs#hostsideadaptercode)]
 [!code-vb[SimpleAddInReturnsAUISample#HostSideAdapterCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.vb#hostsideadaptercode)]  
  
<a name="AddIn"></a>   
## Implementazione del componente aggiuntivo  
 Dopo aver creato l'adattatore sul lato componente aggiuntivo e la visualizzazione del componente, il componente aggiuntivo \(`WPFAddIn1.AddIn`\) deve implementare il metodo `IWPFAddInView.GetAddInUI` per restituire un oggetto <xref:System.Windows.FrameworkElement> \(<xref:System.Windows.Controls.UserControl> in questo esempio\).  Nel codice riportato di seguito viene illustrata l'implementazione di <xref:System.Windows.Controls.UserControl>, `AddInUI`.  
  
 [!code-xml[SimpleAddInReturnsAUISample#AddInUIMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddInUI.xaml#addinuimarkup)]  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInUICodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddInUI.xaml.cs#addinuicodebehind)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInUICodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/WPFAddIn1/AddInUI.xaml.vb#addinuicodebehind)]  
  
 L'implementazione di `IWPFAddInView.GetAddInUI` da parte del componente aggiuntivo deve semplicemente restituire una nuova istanza di `AddInUI`, come illustrato nel codice seguente.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddIn.cs#addincode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/WPFAddIn1/AddIn.vb#addincode)]  
  
<a name="App"></a>   
## Implementazione dell'applicazione host  
 Una volta creato l'adattatore sul lato host e la visualizzazione host, nell'applicazione host è possibile utilizzare il modello di componente aggiuntivo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per aprire la pipeline, acquisire una visualizzazione host del componente aggiuntivo e chiamare il metodo `IWPFAddInHostView.GetAddInUI`.  Nel codice riportato di seguito vengono illustrati i diversi passaggi.  
  
 [!code-csharp[SimpleAddInReturnsAUISample#GetUICode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/Host/MainWindow.xaml.cs#getuicode)]
 [!code-vb[SimpleAddInReturnsAUISample#GetUICode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/Host/MainWindow.xaml.vb#getuicode)]  
  
## Vedere anche  
 [Componenti aggiuntivi ed estensibilità](../../../../ml/index.xml)   
 [Cenni preliminari sui componenti aggiuntivi di WPF](../../../../docs/framework/wpf/app-development/wpf-add-ins-overview.md)