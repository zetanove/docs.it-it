---
title: "Procedura dettagliata: hosting di controlli compositi 3D di WPF in Windows Form | Microsoft Docs"
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
  - "controlli composti, hosting di WPF"
  - "hosting di contenuto WPF in Windows Form"
ms.assetid: 486369a9-606a-4a3b-b086-a06f2119c7b0
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Procedura dettagliata: hosting di controlli compositi 3D di WPF in Windows Form
In questa procedura dettagliata viene illustrato come creare un controllo composito [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e inserirlo in controlli e form [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] utilizzando il controllo <xref:System.Windows.Forms.Integration.ElementHost>.  
  
 In questa procedura dettagliata viene implementato un oggetto <xref:System.Windows.Controls.UserControl> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che contiene due controlli figlio.  Nell'oggetto <xref:System.Windows.Controls.UserControl> viene visualizzato un cono tridimensionale \(3D\).  L'esecuzione del rendering di oggetti tridimensionali è più facile con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] rispetto a [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  È pertanto opportuno ospitare una classe [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.UserControl> per creare grafica 3D in [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione dell'oggetto <xref:System.Windows.Controls.UserControl> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   Creazione del progetto host Windows Form.  
  
-   Hosting dell'oggetto <xref:System.Windows.Controls.UserControl> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Per un elenco di codice completo delle attività illustrate in questa procedura dettagliata, vedere [Esempio di hosting di un controllo composito di WPF 3D in Windows Form](http://go.microsoft.com/fwlink/?LinkID=160001).  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  
  
<a name="To_Create_the_UserControl"></a>   
## Creazione di UserControl  
  
#### Per creare UserControl  
  
1.  Creare un progetto di libreria di controlli utente WPF denominato `HostingWpfUserControlInWf`.  
  
2.  Aprire UserControl1.xaml in [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
3.  Sostituire il codice generato con il seguente.  
  
     Con questo codice viene definito un oggetto <xref:System.Windows.Controls.UserControl?displayProperty=fullName> che contiene due controlli figlio.  Il primo controllo figlio è un controllo <xref:System.Windows.Controls.Label?displayProperty=fullName>, il secondo è un controllo <xref:System.Windows.Controls.Viewport3D> che consente di visualizzare un cono tridimensionale.  
  
     [!code-xml[HostingWpfUserControlInWf#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/HostingWpfUserControlInWf/ConeControl.xaml#1)]  
  
<a name="To_Create_the_Windows_Forms_Host_Project"></a>   
## Creazione del progetto host Windows Form  
  
#### Per creare il progetto host  
  
1.  Aggiungere un progetto di applicazione Windows denominato `WpfUserControlHost` alla soluzione.  Per ulteriori informazioni, vedere [Procedura: creare un nuovo progetto di applicazione WPF](http://msdn.microsoft.com/it-it/1f6aea7a-33e1-4d3f-8555-1daa42e95d82).  
  
2.  In Esplora soluzioni aggiungere un riferimento all'assembly WindowsFormsIntegration, denominato WindowsFormsIntegration.dll.  
  
3.  Aggiungere riferimenti agli assembly [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] riportati di seguito:  
  
    -   PresentationCore  
  
    -   PresentationFramework  
  
    -   WindowsBase  
  
4.  Aggiungere un riferimento al progetto `HostingWpfUserControlInWf`.  
  
5.  In Esplora soluzioni, impostare il progetto `WpfUserControlHost` come progetto di avvio.  
  
<a name="To_Host_the_Windows_Presentation_Foundation"></a>   
## Hosting di UserControl di Windows Presentation Foundation  
  
#### Per ospitare UserControl  
  
1.  In Progettazione Windows Form aprire Form1.  
  
2.  Fare clic sul pulsante **Eventi** nella finestra Proprietà, quindi fare doppio clic sull'evento <xref:System.Windows.Forms.Form.Load> per creare un gestore eventi.  
  
     L'editor di codice si apre in corrispondenza del gestore eventi `Form1_Load` appena generato.  
  
3.  Sostituire il codice in Form1.cs con il codice riportato di seguito.  
  
     Il gestore eventi `Form1_Load` crea un'istanza di `UserControl1` e la aggiunge `` alla raccolta di controlli figlio del controllo <xref:System.Windows.Forms.Integration.ElementHost>.  Il controllo <xref:System.Windows.Forms.Integration.ElementHost> viene aggiunto alla raccolta di controlli figlio del form.  
  
     [!code-csharp[HostingWpfUserControlInWf#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/WpfUserControlHost/Form1.cs#10)]
     [!code-vb[HostingWpfUserControlInWf#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWpfUserControlInWf/VisualBasic/WpfUserControlHost/Form1.vb#10)]  
  
4.  Premere F5 per compilare ed eseguire l'applicazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)   
 [Procedura dettagliata: hosting di controlli Windows Form compositi in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [Esempio di hosting di un controllo composito in Windows Form](http://go.microsoft.com/fwlink/?LinkID=160001)