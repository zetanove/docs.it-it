---
title: "Cenni preliminari sui controlli ToolBar | Microsoft Docs"
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
  - "controlli, ToolBar"
  - "ToolBar (controllo)"
ms.assetid: a8edb32c-118d-4f31-b6e6-8899082b504b
caps.latest.revision: 28
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 27
---
# Cenni preliminari sui controlli ToolBar
I controlli <xref:System.Windows.Controls.ToolBar> funzionano da contenitori per un gruppo di comandi o controlli le cui funzioni sono in genere correlate.  Di solito, un controllo <xref:System.Windows.Controls.ToolBar> include pulsanti per richiamare dei comandi.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="ToolBarControl"></a>   
## Controllo ToolBar  
 Il controllo <xref:System.Windows.Controls.ToolBar> prende il nome dalla disposizione dei pulsanti o di altri controlli su una singola riga o colonna, come in una barra.  I controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.ToolBar> forniscono un meccanismo di overflow che consente di collocare in un'area di overflow speciale tutti gli elementi che a causa dei limiti di spazio non rientrano in un oggetto <xref:System.Windows.Controls.ToolBar>.  Inoltre, i controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.ToolBar> vengono utilizzati in genere insieme al controllo <xref:System.Windows.Controls.ToolBarTray> correlato, che fornisce un particolare comportamento di layout e il supporto per il ridimensionamento e la disposizione delle barre degli strumenti avviati dall'utente.  
  
<a name="Creating_ToolBars"></a>   
## Specifica della posizione dei controlli ToolBar in un oggetto ToolBarTray  
 Utilizzare le proprietà <xref:System.Windows.Controls.ToolBar.Band%2A> e <xref:System.Windows.Controls.ToolBar.BandIndex%2A> per posizionare <xref:System.Windows.Controls.ToolBar> nell'oggetto <xref:System.Windows.Controls.ToolBarTray>.  La proprietà <xref:System.Windows.Controls.ToolBar.Band%2A> indica la posizione in cui viene posizionato <xref:System.Windows.Controls.ToolBar> all'interno dell'oggetto <xref:System.Windows.Controls.ToolBarTray> padre.  La proprietà <xref:System.Windows.Controls.ToolBar.BandIndex%2A> indica invece l'ordine in cui viene posizionato il controllo <xref:System.Windows.Controls.ToolBar> all'interno della banda.  Nell'esempio seguente viene mostrato come utilizzare questa proprietà per posizionare i controlli <xref:System.Windows.Controls.ToolBar> all'interno di un oggetto <xref:System.Windows.Controls.ToolBarTray>.  
  
 [!code-xml[ToolBarExample#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolBarExample/CS/Pane1.xaml#2)]  
  
<a name="ToolBars_with_Overflow_Items"></a>   
## Oggetti ToolBar con elementi di overflow  
 Spesso i controlli <xref:System.Windows.Controls.ToolBar> contengono un numero di elementi maggiore rispetto a quello che è possibile inserire nelle dimensioni di una barra degli strumenti.  In questi casi, nell'oggetto <xref:System.Windows.Controls.ToolBar> viene visualizzato un pulsante di overflow.  Per visualizzare gli elementi di overflow, è sufficiente fare clic sul pulsante di overflow. Gli elementi verranno visualizzati in una finestra popup al di sotto dell'oggetto <xref:System.Windows.Controls.ToolBar>.  Nell'immagine riportata di seguito viene mostrato un oggetto <xref:System.Windows.Controls.ToolBar> con elementi di overflow.  
  
 ![Barra degli strumenti con overflow](../../../../docs/framework/wpf/controls/media/toolbarwithoverflowitem.png "ToolbarWithOverflowItem")  
Barra degli strumenti con elementi di overflow  
  
 È possibile specificare i casi in cui un elemento della barra degli strumenti deve essere posizionato nel pannello di overflow impostando la proprietà <xref:System.Windows.Controls.ToolBar.OverflowMode%2A?displayProperty=fullName> correlata su <xref:System.Windows.Controls.OverflowMode?displayProperty=fullName>, <xref:System.Windows.Controls.OverflowMode?displayProperty=fullName> oppure <xref:System.Windows.Controls.OverflowMode?displayProperty=fullName>.  Nell'esempio seguente viene specificato che gli ultimi quattro pulsanti della barra degli strumenti devono essere sempre posizionati nel pannello di overflow.  
  
 [!code-xml[ToolBarExample#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolBarExample/CS/Pane1.xaml#3)]  
  
 <xref:System.Windows.Controls.ToolBar> utilizza <xref:System.Windows.Controls.Primitives.ToolBarPanel> e <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel> nell'oggetto <xref:System.Windows.Controls.ControlTemplate>.  La classe <xref:System.Windows.Controls.Primitives.ToolBarPanel> determina il layout degli elementi nella barra degli strumenti.  <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel> determina il layout degli elementi che non rientrano nell'oggetto <xref:System.Windows.Controls.ToolBar>.  Per un esempio di <xref:System.Windows.Controls.ControlTemplate> per un oggetto <xref:System.Windows.Controls.ToolBar>, vedere  
  
 [Stili e modelli di ToolBar](../../../../docs/framework/wpf/controls/toolbar-styles-and-templates.md).  
  
## Vedere anche  
 <xref:System.Windows.Controls.Primitives.ToolBarPanel>   
 <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>   
 [Applicare uno stile ai controlli di un oggetto ToolBar](../../../../docs/framework/wpf/controls/how-to-style-controls-on-a-toolbar.md)   
 [Esempio di raccolta di controlli WPF](http://go.microsoft.com/fwlink/?LinkID=160053)