---
title: "Procedura dettagliata: mapping delle propriet&#224; tramite il controllo ElementHost | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controllo ElementHost, mapping di proprietà"
  - "mapping di proprietà"
ms.assetid: bccd6e0d-2272-4924-9107-ff8ed58b88aa
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura dettagliata: mapping delle propriet&#224; tramite il controllo ElementHost
In questa procedura dettagliata viene mostrato l'utilizzo della proprietà <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> per eseguire il mapping delle proprietà di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] alle proprietà corrispondenti di un elemento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitato.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione del progetto.  
  
-   Definizione di un nuovo mapping della proprietà.  
  
-   Rimozione di un mapping della proprietà predefinito.  
  
-   Estensione di un mapping della proprietà predefinito.  
  
 Per un elenco di codice completo delle attività illustrate in questa procedura dettagliata, vedere [Esempio di mapping delle proprietà tramite il controllo ElementHost](http://go.microsoft.com/fwlink/?LinkID=160018) \(la pagina potrebbe essere in inglese\).  
  
 Al termine della procedura, si sarà in grado di eseguire il mapping delle proprietà di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] alle proprietà di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] corrispondenti di un elemento ospitato.  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  
  
## Creazione del progetto  
  
#### Per creare il progetto  
  
1.  Creare un progetto dell'applicazione [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] denominato `PropertyMappingWithElementHost`.  Per ulteriori informazioni, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  In Esplora soluzioni aggiungere riferimenti agli assembly [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] indicati di seguito.  
  
    -   PresentationCore  
  
    -   PresentationFramework  
  
    -   WindowsBase  
  
    -   WindowsFormsIntegration  
  
3.  Copiare il codice seguente all'inizio del file di codice `Form1`.  
  
     [!code-csharp[PropertyMappingWithElementHost#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#10)]
     [!code-vb[PropertyMappingWithElementHost#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#10)]  
  
4.  Aprire `Form1` in Progettazione Windows Form.  Fare doppio clic sul form per aggiungere un gestore eventi per l'evento <xref:System.Windows.Forms.Form.Load>.  
  
5.  Tornare a Progettazione Windows Form e aggiungere un gestore eventi per l'evento <xref:System.Windows.Forms.Control.Resize> del form.  Per ulteriori informazioni, vedere [How to: Create Event Handlers Using the Designer](http://msdn.microsoft.com/it-it/8461e9b8-14e8-406f-936e-3726732b23d2).  
  
6.  Dichiarare un campo <xref:System.Windows.Forms.Integration.ElementHost> nella classe `Form1`.  
  
     [!code-csharp[PropertyMappingWithElementHost#16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#16)]
     [!code-vb[PropertyMappingWithElementHost#16](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#16)]  
  
## Definizione di nuovi mapping della proprietà  
 Il controllo <xref:System.Windows.Forms.Integration.ElementHost> fornisce diversi mapping della proprietà predefiniti.  È possibile aggiungere un nuovo mapping della proprietà chiamando il metodo <xref:System.Windows.Forms.Integration.PropertyMap.Add%2A> sull'oggetto <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> del controllo <xref:System.Windows.Forms.Integration.ElementHost>.  
  
#### Per definire nuovi mapping della proprietà  
  
1.  Copiare il codice riportato di seguito nella definizione della classe `Form1`.  
  
     [!code-csharp[PropertyMappingWithElementHost#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#12)]
     [!code-vb[PropertyMappingWithElementHost#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#12)]  
  
     Il metodo `AddMarginMapping` aggiunge un nuovo mapping per la proprietà <xref:System.Windows.Forms.Control.Margin%2A>.  
  
     Il metodo `OnMarginChange` converte la proprietà <xref:System.Windows.Forms.Control.Margin%2A> nella proprietà <xref:System.Windows.FrameworkElement.Margin%2A> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
2.  Copiare il codice riportato di seguito nella definizione della classe `Form1`.  
  
     [!code-csharp[PropertyMappingWithElementHost#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#14)]
     [!code-vb[PropertyMappingWithElementHost#14](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#14)]  
  
     Il metodo `AddRegionMapping` aggiunge un nuovo mapping per la proprietà <xref:System.Windows.Forms.Control.Region%2A>.  
  
     Il metodo `OnRegionChange` converte la proprietà <xref:System.Windows.Forms.Control.Region%2A> nella proprietà <xref:System.Windows.UIElement.Clip%2A> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
     Il metodo `Form1_Resize` gestisce l'evento <xref:System.Windows.Forms.Control.Resize> del form e adatta le dimensioni dell'area di ritaglio all'elemento ospitato.  
  
## Rimozione di un mapping della proprietà predefinito  
 È possibile rimuovere un mapping della proprietà predefinito chiamando il metodo <xref:System.Windows.Forms.Integration.PropertyMap.Remove%2A> sull'oggetto <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> del controllo <xref:System.Windows.Forms.Integration.ElementHost>.  
  
#### Per rimuovere un mapping della proprietà predefinito  
  
-   Copiare il codice riportato di seguito nella definizione della classe `Form1`.  
  
     [!code-csharp[PropertyMappingWithElementHost#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#13)]
     [!code-vb[PropertyMappingWithElementHost#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#13)]  
  
     Il metodo `RemoveCursorMapping` elimina il mapping predefinito della proprietà <xref:System.Windows.Forms.Control.Cursor%2A>.  
  
## Estensione di un mapping della proprietà predefinito  
 È possibile utilizzare un mapping della proprietà predefinito ed estenderlo con un mapping personalizzato.  
  
#### Per estendere un mapping della proprietà predefinito  
  
-   Copiare il codice riportato di seguito nella definizione della classe `Form1`.  
  
     [!code-csharp[PropertyMappingWithElementHost#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#15)]
     [!code-vb[PropertyMappingWithElementHost#15](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#15)]  
  
     Il metodo `ExtendBackColorMapping` aggiunge un convertitore di proprietà personalizzato al mapping della proprietà <xref:System.Windows.Forms.Control.BackColor%2A> esistente.  
  
     Il metodo `OnBackColorChange` assegna una specifica immagine alla proprietà <xref:System.Windows.Controls.Control.Background%2A> del controllo ospitato.  Il metodo `OnBackColorChange` viene chiamato dopo l'applicazione del mapping della proprietà predefinito.  
  
## Inizializzazione dei mapping della proprietà  
  
#### Per inizializzare i mapping della proprietà  
  
1.  Copiare il codice riportato di seguito nella definizione della classe `Form1`.  
  
     [!code-csharp[PropertyMappingWithElementHost#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#11)]
     [!code-vb[PropertyMappingWithElementHost#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#11)]  
  
     Il metodo `Form1_Load` gestisce l'evento <xref:System.Windows.Forms.Form.Load> ed esegue la seguente inizializzazione.  
  
    -   Crea un elemento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Button>.  
  
    -   Chiama i metodi definiti in precedenza nella procedura dettagliata per configurare i mapping della proprietà.  
  
    -   Assegna i valori iniziali alle proprietà di cui è stato eseguito il mapping.  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Mapping di proprietà di Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)