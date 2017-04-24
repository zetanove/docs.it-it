---
title: "Ottimizzazione delle prestazioni: controlli | Microsoft Docs"
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
  - "riciclo del contenitore"
  - "controlli [WPF], miglioramento delle prestazioni"
  - "virtualizzazione dell'interfaccia utente"
ms.assetid: 45a31c43-ea8a-4546-96c8-0631b9934179
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Ottimizzazione delle prestazioni: controlli
In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] sono inclusi molti dei componenti dell'interfaccia utente comuni utilizzati nella maggior parte delle applicazioni Windows.  In questo argomento sono descritte le tecniche che consentono di migliorare le prestazioni dell'interfaccia utente.  
  
   
  
<a name="Displaying"></a>   
## Visualizzazione di set di dati di grandi dimensioni  
 I controlli WPF, ad esempio <xref:System.Windows.Controls.ListView> e <xref:System.Windows.Controls.ComboBox>, vengono utilizzati per visualizzare elenchi di elementi in un'applicazione.  Se l'elenco da visualizzare è molto lungo, le prestazioni dell'applicazione possono risentirne.  Ciò è dovuto al fatto che il sistema di layout standard crea un contenitore di layout per ogni elemento associato al controllo elenco e ne calcola dimensioni di layout e posizione.  Solitamente non è necessario visualizzare tutti gli elementi nello stesso tempo, ne viene invece visualizzato un sottoinsieme e l'utente scorre l'elenco.  In questo caso è utile utilizzare la *virtualizzazione* dell'interfaccia utente, ovvero la generazione del contenitore dell'elemento e il calcolo del layout associato sono rinviati al momento in cui l'elemento risulta visibile.  
  
 La virtualizzazione dell'interfaccia utente è un importante aspetto dei controlli elenco.  Non deve essere confusa con la virtualizzazione dei dati.  Con la virtualizzazione dell'interfaccia utente solo gli elementi visibili sono archiviati in memoria ma in uno scenario di associazione dati viene archiviata in memoria l'intera struttura dei dati.  Con la virtualizzazione dei dati, al contrario, vengono archiviati in memoria solo gli elementi dati che sono visibili sullo schermo.  
  
 Per impostazione predefinita, la virtualizzazione dell'interfaccia utente è abilitata per i controlli <xref:System.Windows.Controls.ListView> e <xref:System.Windows.Controls.ListBox> quando i relativi elementi elenco sono associati a dati.  La virtualizzazione di <xref:System.Windows.Controls.TreeView> può essere abilitata impostando la proprietà associata <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=fullName> su `true`.  Se si desidera abilitare la virtualizzazione dell'interfaccia utente per controlli personalizzati che derivano da <xref:System.Windows.Controls.ItemsControl> o per controlli di elementi esistenti che utilizzano la classe <xref:System.Windows.Controls.StackPanel>, ad esempio <xref:System.Windows.Controls.ComboBox>, è possibile impostare la proprietà <xref:System.Windows.Controls.ItemsControl.ItemsPanel%2A> su <xref:System.Windows.Controls.VirtualizingStackPanel> e impostare <xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizing%2A> su `true`.  Purtroppo è possibile disabilitare inavvertitamente la virtualizzazione dell'interfaccia utente per questi controlli.  Nell'elenco seguente vengono indicate le condizioni in grado di disabilitare la virtualizzazione dell'interfaccia utente.  
  
-   I contenitori di elementi vengono aggiunti direttamente a <xref:System.Windows.Controls.ItemsControl>,  Se ad esempio in un'applicazione vengono aggiunti in modo esplicito oggetti <xref:System.Windows.Controls.ListBoxItem> a un controllo <xref:System.Windows.Controls.ListBox>, <xref:System.Windows.Controls.ListBox> non virtualizza gli oggetti <xref:System.Windows.Controls.ListBoxItem>.  
  
-   I contenitori di elementi in <xref:System.Windows.Controls.ItemsControl> sono di tipi diversi.  Un oggetto <xref:System.Windows.Controls.Menu>, ad esempio, che utilizza oggetti <xref:System.Windows.Controls.Separator> non può implementare il riciclo degli elementi perché <xref:System.Windows.Controls.Menu> contiene oggetti di tipo <xref:System.Windows.Controls.Separator> e <xref:System.Windows.Controls.MenuItem>.  
  
-   Impostazione di <xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A> su `false`.  
  
-   Impostazione di <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A> su `false`.  
  
 Un aspetto importante in virtualizzate i contenitori di elementi è se si dispone di informazioni sullo stato aggiuntive associate a un contenitore di elementi che appartengono all'elemento.  In questo caso è necessario salvare lo stato aggiuntivo.  Si potrebbe disporre, ad esempio, di un elemento contenuto in un controllo <xref:System.Windows.Controls.Expander> e lo stato <xref:System.Windows.Controls.Expander.IsExpanded%2A> è associato al contenitore dell'elemento, non all'elemento stesso.  Quando il contenitore viene riutilizzato per un nuovo elemento, il valore corrente di <xref:System.Windows.Controls.Expander.IsExpanded%2A> viene utilizzato per il nuovo elemento.  L'elemento precedente, inoltre, perde il valore <xref:System.Windows.Controls.Expander.IsExpanded%2A> corretto.  
  
 Attualmente nessun controllo WPF presenta supporto incorporato per la virtualizzazione dei dati.  
  
<a name="Container"></a>   
## Riciclo del contenitore  
 Un'ottimizzazione della virtualizzazione dell'interfaccia utente aggiunta in .NET Framework 3.5 SP1 per controlli che ereditano da <xref:System.Windows.Controls.ItemsControl> è il *riciclo del contenitore*, in grado di migliorare anche l'operazione di scorrimento.  Quando viene popolato un oggetto <xref:System.Windows.Controls.ItemsControl> che utilizza la virtualizzazione dell'interfaccia utente, per ogni elemento visualizzato viene creato un contenitore mentre per ogni elemento che scompare dalla visualizzazione il contenitore relativo viene distrutto.  Il *riciclo del contenitore* consente al controllo di riutilizzare i contenitori esistenti per i vari elementi dati, di modo che i contenitori non vengano continuamente creati e distrutti man mano che l'utente scorre <xref:System.Windows.Controls.ItemsControl>.  È possibile abilitare il riciclo degli elementi impostando <xref:System.Windows.Controls.VirtualizingPanel.VirtualizationMode%2A> proprietà associata su  <xref:System.Windows.Controls.VirtualizationMode>.  
  
 Qualsiasi oggetto <xref:System.Windows.Controls.ItemsControl> che supporta la virtualizzazione può utilizzare il riciclo del contenitore.  Per un esempio di come abilitare il riciclo del contenitore in un oggetto <xref:System.Windows.Controls.ListBox>, vedere [Miglioramento delle prestazioni di scorrimento di un controllo ListBox](../../../../docs/framework/wpf/controls/how-to-improve-the-scrolling-performance-of-a-listbox.md).  
  
<a name="Supporting"></a>   
## Supporto della virtualizzazione bidirezionale  
 <xref:System.Windows.Controls.VirtualizingStackPanel> offre supporto incorporato per la virtualizzazione dell'interfaccia utente in una direzione, in senso orizzontale o verticale.  Se per i controlli si desidera utilizzare la virtualizzazione bidirezionale, è necessario implementare un pannello personalizzato che estende la classe <xref:System.Windows.Controls.VirtualizingStackPanel>.  La classe <xref:System.Windows.Controls.VirtualizingStackPanel> espone metodi virtuali, ad esempio <xref:System.Windows.Controls.VirtualizingStackPanel.OnViewportSizeChanged%2A>, <xref:System.Windows.Controls.VirtualizingStackPanel.LineUp%2A>, <xref:System.Windows.Controls.VirtualizingStackPanel.PageUp%2A> e <xref:System.Windows.Controls.VirtualizingStackPanel.MouseWheelUp%2A>. Tali metodi virtuali consentono di rilevare una modifica nella parte visibile di un elenco e di affrontarla di conseguenza.  
  
<a name="Optimizing"></a>   
## Ottimizzazione dei modelli  
 La struttura ad albero visuale contiene tutti gli elementi visivi di un'applicazione.  Oltre agli oggetti creati direttamente, contiene inoltre oggetti dovuti all'espansione del modello.  Quando ad esempio si crea un oggetto <xref:System.Windows.Controls.Button>, si ottengono anche oggetti <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> e <xref:System.Windows.Controls.ContentPresenter> nella struttura ad albero visuale.  Se non si è provveduto a ottimizzare i modelli di controllo, è possibile che si creino molti oggetti in più non necessari nella struttura ad albero visuale.  Per ulteriori informazioni sulla struttura ad albero visuale, vedere [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md).  
  
<a name="Deferred"></a>   
## Scorrimento posticipato  
 Per impostazione predefinita quando l'utente trascina il cursore su una barra di scorrimento, la visualizzazione del contenuto viene continuamente aggiornata.  Se lo scorrimento è lento nel controllo, prendere in considerazione lo scorrimento posticipato.  In tal caso il contenuto viene aggiornato solo quando l'utente rilascia il cursore.  
  
 Per implementare lo scorrimento posticipato, impostare la proprietà <xref:System.Windows.Controls.ScrollViewer.IsDeferredScrollingEnabled%2A> su `true`.  <xref:System.Windows.Controls.ScrollViewer.IsDeferredScrollingEnabled%2A> è una proprietà associata che può essere impostata in <xref:System.Windows.Controls.ScrollViewer> e in qualsiasi controllo che dispone di <xref:System.Windows.Controls.ScrollViewer> nel relativo modello.  
  
<a name="Controls"></a>   
## Controlli che implementano le funzioni relative alle prestazioni  
 Nella tabella seguente sono elencati i controlli comuni per la visualizzazione dei dati e il rispettivo supporto delle funzionalità relative alle prestazioni.  Vedere le sezioni precedenti per informazioni sull'abilitazione di queste funzionalità.  
  
|Controllo|Virtualizzazione|Riciclo del contenitore|Scorrimento posticipato|  
|---------------|----------------------|-----------------------------|-----------------------------|  
|<xref:System.Windows.Controls.ComboBox>|Può essere abilitato|Può essere abilitato|Può essere abilitato|  
|<xref:System.Windows.Controls.ContextMenu>|Può essere abilitato|Può essere abilitato|Può essere abilitato|  
|<xref:System.Windows.Controls.DocumentViewer>|Non disponibile|Non disponibile|Può essere abilitato|  
|<xref:System.Windows.Controls.ListBox>|Predefinito|Può essere abilitato|Può essere abilitato|  
|<xref:System.Windows.Controls.ListView>|Predefinito|Può essere abilitato|Può essere abilitato|  
|<xref:System.Windows.Controls.TreeView>|Può essere abilitato|Può essere abilitato|Può essere abilitato|  
|<xref:System.Windows.Controls.ToolBar>|Non disponibile|Non disponibile|Può essere abilitato|  
  
> [!NOTE]
>  Per un esempio di come abilitare la virtualizzazione e il riciclo del contenitore in un oggetto <xref:System.Windows.Controls.TreeView>, vedere [Miglioramento delle prestazioni di un controllo TreeView](../../../../docs/framework/wpf/controls/how-to-improve-the-performance-of-a-treeview.md).  
  
## Vedere anche  
 [Layout](../../../../docs/framework/wpf/advanced/layout.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Controlli](../../../../docs/framework/wpf/controls/index.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Procedura dettagliata: memorizzazione dei dati di un'applicazione nella cache di un'applicazione WPF](../../../../docs/framework/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)