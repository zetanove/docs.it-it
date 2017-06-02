---
title: "Ottimizzazione delle prestazioni: altri suggerimenti | Microsoft Docs"
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
  - "pennelli, prestazioni"
  - "hit test (oggetti) [WPF]"
  - "opacità"
  - "ScrollBarVisibility (enumerazione)"
  - "Servizi terminal (rendering)"
ms.assetid: d028cc65-7e97-4a4f-9859-929734eaf40d
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Ottimizzazione delle prestazioni: altri suggerimenti
<a name="introduction"></a> In questo argomento vengono forniti ulteriori suggerimenti sulle prestazioni, in aggiunta a quelli riportati negli argomenti della sezione [Ottimizzazione delle prestazioni di applicazioni WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md).  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Pennelli opachi ed elementi opachi](#Opacity)  
  
-   [Navigazione a un oggetto](#Navigation_Objects)  
  
-   [Hit testing su superfici tridimensionali ampie](#Hit_Testing)  
  
-   [Evento CompositionTarget.Rendering](#CompositionTarget_Rendering_Event)  
  
-   [Evitare l'utilizzo di ScrollBarVisibility\=Auto](#Avoid_Using_ScrollBarVisibility)  
  
-   [Configurare il servizio Cache tipi di carattere per ridurre i tempi di avvio](#FontCache)  
  
<a name="Opacity"></a>   
## Pennelli opachi ed elementi opachi  
 Quando si utilizza un oggetto <xref:System.Windows.Media.Brush> per impostare l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> o <xref:System.Windows.Shapes.Shape.Stroke%2A> di un elemento, è preferibile impostare il valore di <xref:System.Windows.Media.Brush.Opacity%2A?displayProperty=fullName> anziché la proprietà <xref:System.Windows.UIElement.Opacity%2A> dell'elemento.  La modifica della proprietà <xref:System.Windows.UIElement.Opacity%2A> di un elemento può determinare la creazione di un'area temporanea in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
<a name="Navigation_Objects"></a>   
## Navigazione a un oggetto  
 L'oggetto <xref:System.Windows.Navigation.NavigationWindow> deriva da <xref:System.Windows.Window> e lo estende con il supporto per la navigazione sul contenuto, principalmente mediante l'aggregazione di <xref:System.Windows.Navigation.NavigationService> e del journal.  È possibile aggiornare l'area client di <xref:System.Windows.Navigation.NavigationWindow> specificando un [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] oppure un oggetto.  Nell'esempio riportato di seguito vengono illustrati entrambi i metodi:  
  
 [!code-csharp[Performance#PerformanceSnippet14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/TestNavigation.xaml.cs#performancesnippet14)]
 [!code-vb[Performance#PerformanceSnippet14](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/testnavigation.xaml.vb#performancesnippet14)]  
  
 Ciascun oggetto <xref:System.Windows.Navigation.NavigationWindow> dispone di un journal per la registrazione della cronologia di navigazione dell'utente in quella finestra.  Uno degli scopi del journal è quello di consentire agli utenti di ritracciare i passaggi eseguiti.  
  
 Durante gli spostamenti tramite [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)], nel journal viene archiviato solo il riferimento all'[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)].  Di conseguenza, ogni volta che quella stessa pagina viene visitata nuovamente, sarà ricostruita in modo dinamico; tale operazione può richiedere molto tempo, a seconda della complessità della pagina.  In questo caso, il costo di archiviazione nel journal è basso, ma il tempo necessario per la ricostruzione della pagina è potenzialmente lungo.  
  
 Durante gli spostamenti tramite l'utilizzo di un oggetto, nel journal viene archiviata l'intera struttura ad albero visiva dell'oggetto.  Pertanto, ogni volta che quella stessa pagina viene visitata nuovamente, viene eseguito immediatamente il rendering, senza che sia necessario ricostruirla.  In questo caso, il costo di archiviazione nel journal è elevato, ma il tempo necessario per la ricostruzione della pagina è breve.  
  
 Quando si utilizza l'oggetto <xref:System.Windows.Navigation.NavigationWindow>, è necessario tenere presenti gli effetti del supporto di inserimento nel journal sulle prestazioni dell'applicazione.  Per ulteriori informazioni, vedere [Cenni preliminari sulla navigazione](../../../../docs/framework/wpf/app-development/navigation-overview.md).  
  
<a name="Hit_Testing"></a>   
## Hit testing su superfici tridimensionali ampie  
 L'hit testing su superfici tridimensionali ampie richiede prestazioni particolarmente elevate in termini di consumo della CPU,  soprattutto in caso di aggiunta di un'animazione alla superficie tridimensionale.  Se l'hit testing su tali superfici non è necessario, è opportuno disabilitarlo.  Per gli oggetti che derivano da <xref:System.Windows.UIElement> è possibile disabilitare l'hit testing impostando la proprietà <xref:System.Windows.UIElement.IsHitTestVisible%2A> su `false`.  
  
<a name="CompositionTarget_Rendering_Event"></a>   
## Evento CompositionTarget.Rendering  
 L'evento <xref:System.Windows.Media.CompositionTarget.Rendering?displayProperty=fullName> determina l'aggiunta continua di animazione a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Se si utilizza questo evento, disconnetterlo quando possibile.  
  
<a name="Avoid_Using_ScrollBarVisibility"></a>   
## Evitare l'utilizzo di ScrollBarVisibility\=Auto  
 Quando possibile, evitare l'utilizzo del valore <xref:System.Windows.Controls.ScrollBarVisibility?displayProperty=fullName> per le proprietà `HorizontalScrollBarVisibility` e `VerticalScrollBarVisibility`.  Tali proprietà sono definite per gli oggetti <xref:System.Windows.Controls.RichTextBox>, <xref:System.Windows.Controls.ScrollViewer>, e <xref:System.Windows.Controls.TextBox> e, come proprietà associata per l'oggetto <xref:System.Windows.Controls.ListBox>.  Impostare invece <xref:System.Windows.Controls.ScrollBarVisibility> su <xref:System.Windows.Controls.ScrollBarVisibility>, <xref:System.Windows.Controls.ScrollBarVisibility> o <xref:System.Windows.Controls.ScrollBarVisibility>.  
  
 L'utilizzo del valore <xref:System.Windows.Controls.ScrollBarVisibility> è destinato ai casi in cui lo spazio è limitato e le barre di scorrimento devono essere visualizzate solo se necessario.  Ad esempio, l'utilizzo di questo valore <xref:System.Windows.Controls.ScrollBarVisibility> può rivelarsi utile con un oggetto <xref:System.Windows.Controls.ListBox> di 30 elementi, ma non con un oggetto <xref:System.Windows.Controls.TextBox> con centinaia di righe di testo.  
  
<a name="FontCache"></a>   
## Configurare il servizio Cache tipi di carattere per ridurre i tempi di avvio  
 Tramite il servizio Cache tipi di carattere di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], i dati relativi ai tipi di carattere vengono condivisi tra le applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Il servizio viene avviato insieme alla prima applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] eseguita, a meno che non sia già in esecuzione.  Se si sta utilizzando [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)], è possibile modificare l'impostazione del servizio "Cache tipi di carattere [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 3.0.0.0" da "Manuale" \(impostazione predefinita\) ad "Automatico \(Avvio ritardato\)" per ridurre il tempo di avvio delle applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
## Vedere anche  
 [Pianificazione delle prestazioni dell'applicazione](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [Sfruttare appieno l'hardware](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Comportamento dell'oggetto](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Risorse delle applicazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Suggerimenti sulle animazioni](../../../../docs/framework/wpf/graphics-multimedia/animation-tips-and-tricks.md)