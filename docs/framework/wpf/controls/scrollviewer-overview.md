---
title: "Cenni preliminari sull&#39;elemento ScrollViewer | Microsoft Docs"
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
  - "controlli, ScrollViewer"
  - "ScrollViewer (controllo), informazioni sul controllo ScrollViewer"
ms.assetid: 94a13b94-cfdf-4b12-a1aa-90cb50c6e9b9
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Cenni preliminari sull&#39;elemento ScrollViewer
Il contenuto all'interno di un'interfaccia utente è spesso di dimensioni maggiori dell'area di visualizzazione dello schermo di un computer.  Il controllo <xref:System.Windows.Controls.ScrollViewer> consente di attivare lo scorrimento del contenuto nelle applicazioni [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  In questo argomento vengono forniti cenni preliminari sul controllo <xref:System.Windows.Controls.ScrollViewer> e diversi esempio di utilizzo.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
-   [Controllo ScrollViewer](#what_is_a_scrollviewer_element)  
  
-   [Scorrimento fisicoe logico](#scrollviewer_physical_vs_logical)  
  
-   [Definizione e utilizzo dell'elemento ScrollViewer](#scrollviewer_markup_syntax_and_sample)  
  
-   [Applicazione di uno stile a un elemento ScrollViewer](#scrollviewer_styling_scrollviewer)  
  
-   [Paginazione di documenti](#scrollviewer_scroll_vs_paginate)  
  
-   [Related Topics](#seeAlsoToggle)  
  
<a name="what_is_a_scrollviewer_element"></a>   
## Controllo ScrollViewer  
 Due elementi predefiniti consentono lo scorrimento nelle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]: <xref:System.Windows.Controls.Primitives.ScrollBar> e <xref:System.Windows.Controls.ScrollViewer>.  Il controllo <xref:System.Windows.Controls.ScrollViewer> incapsula gli elementi <xref:System.Windows.Controls.Primitives.ScrollBar> orizzontale e verticale e un contenitore di contenuto \(ad esempio un elemento <xref:System.Windows.Controls.Panel>\) per visualizzare gli altri elementi visibili in un'area scorrevole.  È necessario compilare un oggetto personalizzato per utilizzare l'elemento <xref:System.Windows.Controls.Primitives.ScrollBar> per lo scorrimento di contenuto.  Tuttavia, è possibile utilizzare da solo l'elemento <xref:System.Windows.Controls.ScrollViewer> perché è un controllo composito che incapsula la funzionalità <xref:System.Windows.Controls.Primitives.ScrollBar>.  
  
 Il controllo <xref:System.Windows.Controls.ScrollViewer> risponde a comandi del mouse e della tastiera, oltre a definire numerosi metodi con cui scorrere il contenuto in base a incrementi predeterminati.  È possibile utilizzare l'evento <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> per rilevare una modifica nello stato di un controllo <xref:System.Windows.Controls.ScrollViewer>.  
  
 Un controllo <xref:System.Windows.Controls.ScrollViewer> può includere un unico elemento figlio, solitamente un elemento <xref:System.Windows.Controls.Panel> che può contenere una raccolta <xref:System.Windows.Controls.Panel.Children%2A> di elementi.  La proprietà <xref:System.Windows.Controls.ContentPresenter.Content%2A> definisce l'unico elemento figlio del controllo <xref:System.Windows.Controls.ScrollViewer>.  
  
<a name="scrollviewer_physical_vs_logical"></a>   
## Scorrimento fisicoe logico  
 Lo scorrimento fisico viene utilizzato per scorrere il contenuto in base a un incremento fisico predeterminato, in genere un valore dichiarato in pixel.  Lo spostamento logico viene utilizzato per scorrere fino all'elemento successivo nella struttura ad albero logica.  Lo scorrimento fisico rappresenta il comportamento predefinito per la maggior parte degli elementi <xref:System.Windows.Controls.Panel>.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] supporta entrambi i tipi di scorrimento.  
  
#### Interfaccia IScrollInfo  
 L'interfaccia <xref:System.Windows.Controls.Primitives.IScrollInfo> rappresenta l'area di scorrimento principale all'interno di un controllo <xref:System.Windows.Controls.ScrollViewer> o di un controllo derivato.  L'interfaccia definisce le proprietà e i metodi di scorrimento che possono essere implementati dagli elementi <xref:System.Windows.Controls.Panel> che richiedono lo scorrimento in base a un'unità logica, anziché a un incremento fisico.  Il cast di un'istanza di <xref:System.Windows.Controls.Primitives.IScrollInfo> in un controllo <xref:System.Windows.Controls.Panel> derivato e quindi l'utilizzo dei relativi metodi di scorrimento consentono di scorrere fino all'unità logica successiva in una raccolta figlio, anziché in base a un incremento in pixel.  Per impostazione predefinita, il controllo <xref:System.Windows.Controls.ScrollViewer> supporta lo scorrimento in base a unità fisiche.  
  
 I controlli <xref:System.Windows.Controls.StackPanel> e <xref:System.Windows.Controls.VirtualizingStackPanel> implementano <xref:System.Windows.Controls.Primitives.IScrollInfo> e supportano a livello nativo lo scorrimento logico.  Per i controlli del layout che supportano a livello nativo lo scorrimento logico, è comunque possibile ottenere lo scorrimento fisico eseguendo il wrapping dell'elemento <xref:System.Windows.Controls.Panel> host in un controllo <xref:System.Windows.Controls.ScrollViewer> e impostando la proprietà <xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A> su `false`.  
  
 Nell'esempio di codice seguente viene illustrato come eseguire il cast di un'istanza di <xref:System.Windows.Controls.Primitives.IScrollInfo> in un controllo <xref:System.Windows.Controls.StackPanel> e come utilizzare i metodi di scorrimento del contenuto \(<xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A> e <xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A>\) definiti dall'interfaccia.  
  
 [!code-csharp[IScrollInfoMethods#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
<a name="scrollviewer_markup_syntax_and_sample"></a>   
## Definizione e utilizzo dell'elemento ScrollViewer  
 Nell'esempio seguente viene creato un oggetto <xref:System.Windows.Controls.ScrollViewer> in una finestra che contiene testo e un rettangolo.  Gli elementi <xref:System.Windows.Controls.Primitives.ScrollBar> vengono visualizzati solo quando sono necessari.  Quando si ridimensiona la finestra, gli elementi <xref:System.Windows.Controls.Primitives.ScrollBar> vengono visualizzati e nascosti a causa dei valori aggiornati delle proprietà <xref:System.Windows.Controls.ScrollViewer.ComputedHorizontalScrollBarVisibility%2A> e <xref:System.Windows.Controls.ScrollViewer.ComputedVerticalScrollBarVisibility%2A>.  
  
 [!code-cpp[ScrollViewer#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/ScrollViewer/CPP/ScrollViewer_wcp.cpp#1)]
 [!code-csharp[ScrollViewer#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewer/CSharp/ScrollViewer_wcp.cs#1)]
 [!code-vb[ScrollViewer#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewer/VisualBasic/ScrollViewer.vb#1)]
 [!code-xml[ScrollViewer#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/ScrollViewer/XAML/Pane1.xaml#1)]  
  
<a name="scrollviewer_styling_scrollviewer"></a>   
## Applicazione di uno stile a un elemento ScrollViewer  
 Come per tutti i controlli di Windows Presentation Foundation, è possibile applicare uno stile all'elemento <xref:System.Windows.Controls.ScrollViewer> in modo da modificarne il comportamento di rendering predefinito.  Per ulteriori informazioni sull'applicazione di stili ai controlli, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
<a name="scrollviewer_scroll_vs_paginate"></a>   
## Paginazione di documenti  
 Per il contenuto di un documento, in alternativa allo scorrimento è possibile scegliere un contenitore di documenti che supporta la paginazione.  <xref:System.Windows.Documents.FlowDocument> è per i documenti progettati per essere ospitati all'interno di un controllo di visualizzazione, ad esempio <xref:System.Windows.Controls.FlowDocumentPageViewer>, che supporta l'impaginazione del contenuto tra più pagine, evitando di dover ricorrere allo scorrimento.  <xref:System.Windows.Controls.DocumentViewer> fornisce una soluzione per la visualizzazione del contenuto <xref:System.Windows.Documents.FixedDocument>, che utilizza lo scorrimento tradizionale per visualizzare il contenuto all'esterno dell'area di autenticazione dell'area di visualizzazione.  
  
 Per ulteriori informazioni sui formati di documento e le opzioni di presentazione, vedere [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md).  
  
## Vedere anche  
 <xref:System.Windows.Controls.ScrollViewer>   
 <xref:System.Windows.Controls.Primitives.ScrollBar>   
 <xref:System.Windows.Controls.Primitives.IScrollInfo>   
 [Create a Scroll Viewer](http://msdn.microsoft.com/it-it/c8e46af7-b417-441b-aa30-791cbdbd43ef)   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Stili e modelli di ScrollBar](../../../../docs/framework/wpf/controls/scrollbar-styles-and-templates.md)   
 [Controlli](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)