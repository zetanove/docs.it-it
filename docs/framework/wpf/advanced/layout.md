---
title: "Layout | Microsoft Docs"
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
  - "controlli [WPF], sistema di layout"
  - "sistema di layout [WPF]"
  - "WPF (sistema di layout)"
ms.assetid: 3eecdced-3623-403a-a077-7595453a9221
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# Layout
In questo argomento viene illustrato il sistema di layout di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  È fondamentale comprendere come e quando vengono eseguiti i calcoli di layout per la creazione di interfacce utente in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Riquadri degli elementi](#LayoutSystem_BoundingBox)  
  
-   [Sistema di layout](#LayoutSystem_Overview)  
  
-   [Misurazione e disposizione di elementi figlio](#LayoutSystem_Measure_Arrange)  
  
-   [Elementi Panel e comportamenti di layout personalizzati](#LayoutSystem_PanelsCustom)  
  
-   [Considerazioni sulle prestazioni correlate al layout](#LayoutSystem_Performance)  
  
-   [Rendering dei subpixel e arrotondamento del layout](#LayoutSystem_LayoutRounding)  
  
-   [Argomenti successivi](#LayoutSystem_whatsnext)  
  
<a name="LayoutSystem_BoundingBox"></a>   
## Riquadri degli elementi  
 Nella valutazione del layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è importante tenere presente il riquadro che racchiude tutti gli elementi.  Ogni oggetto <xref:System.Windows.FrameworkElement> utilizzato dal sistema di layout può essere considerato come un rettangolo inciso nel layout.  La classe <xref:System.Windows.Controls.Primitives.LayoutInformation> restituisce i limiti dell'allocazione del layout di un elemento o slot.  Le dimensioni del rettangolo vengono determinate dal sistema in base allo spazio disponibile sullo schermo, alle dimensioni di eventuali vincoli, a proprietà specifiche del layout, ad esempio margine e spaziatura interna, e al comportamento dell'elemento <xref:System.Windows.Controls.Panel> padre.  L'elaborazione di questi dati consente al sistema di layout di calcolare la posizione di tutti gli elementi figlio di un determinato oggetto <xref:System.Windows.Controls.Panel>.  È importante ricordare che le caratteristiche delle dimensioni definite sull'elemento padre, ad esempio <xref:System.Windows.Controls.Border>, influiscono sui relativi elementi figlio.  
  
 Nell'immagine seguente viene illustrato un layout semplice.  
  
 ![Tipico oggetto Grid senza riquadro sovrapposto](../../../../docs/framework/wpf/advanced/media/boundingbox1.png "boundingbox1")  
  
 È possibile ottenere questo layout utilizzando il codice [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] seguente.  
  
 [!code-xml[LayoutInformation#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml#1)]  
  
 Un singolo elemento <xref:System.Windows.Controls.TextBlock> è ospitato all'interno di un oggetto <xref:System.Windows.Controls.Grid>.  Mentre il testo riempie solo l'angolo superiore sinistro della prima colonna, lo spazio allocato per <xref:System.Windows.Controls.TextBlock> è effettivamente più grande.  Il riquadro di un oggetto <xref:System.Windows.FrameworkElement> può essere recuperato utilizzando il metodo <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A>.  Nella figura seguente viene illustrato il riquadro dell'elemento <xref:System.Windows.Controls.TextBlock>.  
  
 ![Il riquadro di TextBlock è ora visibile](../../../../docs/framework/wpf/advanced/media/boundingbox2.png "boundingbox2")  
  
 Come indicato dal rettangolo giallo, lo spazio allocato per l'elemento <xref:System.Windows.Controls.TextBlock> è effettivamente più grande di quanto non appaia.  Con l'aggiunta di ulteriori elementi all'oggetto <xref:System.Windows.Controls.Grid>, questa sezione potrà espandersi o ridursi, a seconda del tipo e delle dimensioni di tali elementi.  
  
 Lo slot di layout di <xref:System.Windows.Controls.TextBlock> viene convertito in un oggetto <xref:System.Windows.Shapes.Path> tramite il metodo <xref:System.Windows.Controls.Primitives.LayoutInformation.GetLayoutSlot%2A>.  Questa tecnica può essere utile per visualizzare il riquadro di un elemento.  
  
 [!code-csharp[LayoutInformation#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LayoutInformation/CSharp/Window1.xaml.cs#2)]
 [!code-vb[LayoutInformation#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/LayoutInformation/VisualBasic/Window1.xaml.vb#2)]  
  
<a name="LayoutSystem_Overview"></a>   
## Sistema di layout  
 Nella sua forma più semplice il layout è un sistema ricorsivo di ridimensionamento, posizionamento e disegno di un elemento.  In modo più specifico, con il termine layout si intende descrivere il processo di misurazione e disposizione dei membri della raccolta <xref:System.Windows.Controls.Panel.Children%2A> di un elemento <xref:System.Windows.Controls.Panel>.  Il layout è un processo intensivo.  Più grande è la raccolta <xref:System.Windows.Controls.Panel.Children%2A>, maggiore è il numero di calcoli da eseguire.  La complessità può dipendere anche dal comportamento di layout definito dall'elemento <xref:System.Windows.Controls.Panel> proprietario della raccolta.  Le prestazioni di un oggetto <xref:System.Windows.Controls.Panel> relativamente semplice, ad esempio <xref:System.Windows.Controls.Canvas>, possono essere significativamente migliori di quelle di un oggetto <xref:System.Windows.Controls.Panel> più complesso, ad esempio <xref:System.Windows.Controls.Grid>.  
  
 Ogni volta che un oggetto <xref:System.Windows.UIElement> figlio cambia posizione può potenzialmente attivare un nuovo passaggio da parte del sistema di layout.  È pertanto importante comprendere gli eventi che possono richiamare il sistema di layout, poiché una chiamata non necessaria può influire negativamente sulle prestazioni dell'applicazione.  Di seguito viene descritto il processo che si verifica quando viene richiamato il sistema di layout.  
  
1.  Un oggetto <xref:System.Windows.UIElement> figlio avvia innanzitutto il processo di layout con la misurazione delle relative proprietà principali.  
  
2.  Vengono valutate le proprietà di ridimensionamento definite in <xref:System.Windows.FrameworkElement>, ad esempio <xref:System.Windows.FrameworkElement.Width%2A>, <xref:System.Windows.FrameworkElement.Height%2A> e <xref:System.Windows.FrameworkElement.Margin%2A>.  
  
3.  Viene applicata la logica specifica di <xref:System.Windows.Controls.Panel>, ad esempio la direzione <xref:System.Windows.Controls.Dock> o l'orientamento \(<xref:System.Windows.Controls.StackPanel.Orientation%2A>\) di sovrapposizione.  
  
4.  Il contenuto viene disposto dopo la misurazione di tutti gli oggetti figlio.  
  
5.  La raccolta <xref:System.Windows.Controls.Panel.Children%2A> viene disegnata sullo schermo.  
  
6.  Il processo viene nuovamente richiamato se vengono aggiunti ulteriori elementi <xref:System.Windows.Controls.Panel.Children%2A> alla raccolta, se viene applicata la proprietà <xref:System.Windows.FrameworkElement.LayoutTransform%2A> o se viene chiamato il metodo <xref:System.Windows.UIElement.UpdateLayout%2A>.  
  
 Questo processo e il modo in cui viene richiamato vengono illustrati in dettaglio nelle sezioni seguenti.  
  
<a name="LayoutSystem_Measure_Arrange"></a>   
## Misurazione e disposizione di elementi figlio  
 Il sistema di layout completa due passaggi per ogni membro della raccolta <xref:System.Windows.Controls.Panel.Children%2A>, un passaggio di misurazione e un passaggio di disposizione.  Ogni oggetto <xref:System.Windows.Controls.Panel> figlio fornisce metodi <xref:System.Windows.FrameworkElement.MeasureOverride%2A> e <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> personalizzati per ottenere un comportamento di layout specifico personalizzato.  
  
 Durante il passaggio di misurazione, viene valutato ogni membro della raccolta <xref:System.Windows.Controls.Panel.Children%2A>.  Il processo ha inizio con una chiamata al metodo <xref:System.Windows.UIElement.Measure%2A>.  Questo metodo viene chiamato all'interno dell'implementazione dell'elemento <xref:System.Windows.Controls.Panel> padre e non deve essere chiamato in modo esplicito per eseguire il layout.  
  
 Innanzitutto vengono valutate le proprietà di dimensione native dell'oggetto <xref:System.Windows.UIElement>, ad esempio <xref:System.Windows.UIElement.Clip%2A> e <xref:System.Windows.UIElement.Visibility%2A>.  Viene generato un valore denominato `constraintSize` che viene passato a <xref:System.Windows.FrameworkElement.MeasureCore%2A>.  
  
 In secondo luogo, vengono elaborate le proprietà di framework definite su <xref:System.Windows.FrameworkElement>, che determina la modifica del valore di `constraintSize`.  Queste proprietà descrivono in genere le caratteristiche di ridimensionamento dell'oggetto <xref:System.Windows.UIElement> sottostante, ad esempio le relative proprietà <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.Width%2A>, <xref:System.Windows.FrameworkElement.Margin%2A> e <xref:System.Windows.FrameworkElement.Style%2A>.  Ognuna di queste proprietà può modificare lo spazio necessario per la visualizzazione dell'elemento.  Il metodo <xref:System.Windows.FrameworkElement.MeasureOverride%2A> viene quindi chiamato con `constraintSize` come parametro.  
  
> [!NOTE]
>  Esiste una differenza tra le proprietà di <xref:System.Windows.FrameworkElement.Height%2A> e <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.ActualHeight%2A> e <xref:System.Windows.FrameworkElement.ActualWidth%2A>.  Ad esempio, la proprietà <xref:System.Windows.FrameworkElement.ActualHeight%2A> è un valore calcolato basato su altri input di altezza e sul sistema di layout.  Il valore viene impostato dal sistema di layout in base a un passaggio di rendering effettivo e potrebbe subire un rallentamento rispetto al valore impostato di proprietà quali <xref:System.Windows.FrameworkElement.Height%2A> che rappresentano la base della modifica dell'input.  
>   
>  Poiché <xref:System.Windows.FrameworkElement.ActualHeight%2A> è un valore calcolato, tenere presente che potrebbe subire più modifiche o modifiche incrementali in seguito a varie operazioni eseguite dal sistema di layout.  Il sistema di layout potrebbe calcolare lo spazio di misurazione necessario per gli elementi figlio, i vincoli imposti dall'elemento padre e così via.  
  
 L'obiettivo finale del passaggio di misurazione consiste nel determinare per l'elemento figlio la proprietà <xref:System.Windows.UIElement.DesiredSize%2A> corrispondente, operazione che viene eseguita durante la chiamata al metodo <xref:System.Windows.FrameworkElement.MeasureCore%2A>.  Il valore <xref:System.Windows.UIElement.DesiredSize%2A> viene archiviato da <xref:System.Windows.UIElement.Measure%2A> e verrà utilizzato durante il passaggio di disposizione del contenuto.  
  
 Il passaggio di disposizione ha inizio con una chiamata al metodo <xref:System.Windows.UIElement.Arrange%2A>.  Durante il passaggio di disposizione, l'elemento <xref:System.Windows.Controls.Panel> padre genera un rettangolo che rappresenta i limiti dell'elemento figlio.  Questo valore viene passato al metodo <xref:System.Windows.FrameworkElement.ArrangeCore%2A> affinché venga elaborato.  
  
 Il metodo <xref:System.Windows.FrameworkElement.ArrangeCore%2A> valuta la proprietà <xref:System.Windows.UIElement.DesiredSize%2A> dell'elemento figlio e gli eventuali margini aggiuntivi che potrebbero modificare le dimensioni di rendering dell'elemento.  Il metodo <xref:System.Windows.FrameworkElement.ArrangeCore%2A> genera un oggetto `arrangeSize`, che viene passato al metodo <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> di <xref:System.Windows.Controls.Panel> come parametro.  <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> genera l'oggetto `finalSize` dell'elemento figlio.  Il metodo <xref:System.Windows.FrameworkElement.ArrangeCore%2A> esegue infine una valutazione delle proprietà di offset, ad esempio margine e allineamento, e posiziona l'elemento figlio all'interno del relativo slot di layout.  L'elemento figlio non deve riempire \(e spesso non lo farà\) l'intero spazio allocato.  Quando il controllo viene restituito all'elemento <xref:System.Windows.Controls.Panel> padre, il processo di layout può essere considerato completato.  
  
<a name="LayoutSystem_PanelsCustom"></a>   
## Elementi Panel e comportamenti di layout personalizzati  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è incluso un gruppo di elementi che derivano da <xref:System.Windows.Controls.Panel>.  Questi elementi <xref:System.Windows.Controls.Panel> consentono l'utilizzo di molti layout complessi.  Tramite l'elemento <xref:System.Windows.Controls.StackPanel> è ad esempio possibile realizzare con facilità scenari comuni quali la sovrapposizione di elementi, mentre layout più complessi e dinamici possono essere ottenuti utilizzando l'elemento <xref:System.Windows.Controls.Canvas>.  
  
 Nella tabella seguente vengono riepilogati gli elementi <xref:System.Windows.Controls.Panel> di layout disponibili.  
  
|Nome Panel|Descrizione|  
|----------------|-----------------|  
|<xref:System.Windows.Controls.Canvas>|Definisce un'area nella quale è possibile posizionare in modo esplicito gli elementi figlio utilizzando coordinate relative all'area <xref:System.Windows.Controls.Canvas>.|  
|<xref:System.Windows.Controls.DockPanel>|Definisce un'area all'interno della quale è possibile disporre gli elementi figlio orizzontalmente o verticalmente l'uno rispetto all'altro.|  
|<xref:System.Windows.Controls.Grid>|Definisce un'area flessibile della griglia costituita da colonne e righe.|  
|<xref:System.Windows.Controls.StackPanel>|Dispone gli elementi figlio in una singola riga che può essere orientata orizzontalmente o verticalmente.|  
|<xref:System.Windows.Controls.VirtualizingPanel>|Fornisce un framework per gli elementi <xref:System.Windows.Controls.Panel> che virtualizzano la raccolta dei dati figlio.  Questa è una classe astratta.|  
|<xref:System.Windows.Controls.WrapPanel>|Posiziona gli elementi figlio in sequenza da sinistra verso destra, interrompendo il contenuto quando viene raggiunto il bordo della casella contenitore e facendolo ripartire dalla riga successiva.  L'ordinamento successivo procede in sequenza dall'alto verso il basso o da destra verso sinistra, a seconda del valore della proprietà <xref:System.Windows.Controls.WrapPanel.Orientation%2A>.|  
  
 Per le applicazioni che richiedono un layout impossibile da realizzare utilizzando questi elementi <xref:System.Windows.Controls.Panel> predefiniti, è possibile ottenere comportamenti di layout personalizzati ereditando da <xref:System.Windows.Controls.Panel> ed eseguendo l'override dei metodi <xref:System.Windows.FrameworkElement.MeasureOverride%2A> e <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>.  Per un esempio, vedere [Esempio di pannello radiale personalizzato](http://go.microsoft.com/fwlink/?LinkID=159982) \(la pagina potrebbe essere in inglese\).  
  
<a name="LayoutSystem_Performance"></a>   
## Considerazioni sulle prestazioni correlate al layout  
 Il layout è un processo ricorsivo.  Ogni elemento figlio di una raccolta <xref:System.Windows.Controls.Panel.Children%2A> viene elaborato durante ogni chiamata del sistema di layout.  Di conseguenza, è consigliabile evitare di attivare il sistema di layout quando non è necessario.  Per ottenere prestazioni ottimali, tenere presenti le considerazioni seguenti.  
  
-   Essere consapevoli delle modifiche a valori di proprietà che forzeranno un aggiornamento ricorsivo da parte del sistema di layout.  
  
     Le proprietà di dipendenza i cui valori possono determinare l'inizializzazione del sistema di layout sono contrassegnate con flag pubblici.  Le proprietà <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> e <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> forniscono indicazioni utili relativamente alle modifiche a valori di proprietà che forzeranno un aggiornamento ricorsivo da parte del sistema di layout.  In generale, le proprietà che possono influire sulle dimensioni del riquadro di un elemento dispongono di un flag <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> impostato su true.  Per ulteriori informazioni, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
-   Quando è possibile, utilizzare <xref:System.Windows.UIElement.RenderTransform%2A> anziché <xref:System.Windows.FrameworkElement.LayoutTransform%2A>.  
  
     Una proprietà <xref:System.Windows.FrameworkElement.LayoutTransform%2A> può rappresentare un modo molto utile di influire sul contenuto di un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  Se l'effetto della trasformazione non deve tuttavia avere alcun impatto sulla posizione di altri elementi, è consigliabile utilizzare la proprietà <xref:System.Windows.UIElement.RenderTransform%2A>, in quanto <xref:System.Windows.UIElement.RenderTransform%2A> non richiama il sistema di layout.  <xref:System.Windows.FrameworkElement.LayoutTransform%2A> applica la trasformazione e forza un aggiornamento del layout ricorsivo in modo che venga considerata la nuova posizione dell'elemento interessato.  
  
-   Evitare chiamate non necessarie al metodo <xref:System.Windows.UIElement.UpdateLayout%2A>.  
  
     Il metodo <xref:System.Windows.UIElement.UpdateLayout%2A> forza un aggiornamento ricorsivo del layout che spesso non è necessario.  A meno che non si sia certi della reale necessità di un aggiornamento completo, lasciare che questo metodo venga chiamato automaticamente dal sistema di layout.  
  
-   Quando si utilizza una raccolta <xref:System.Windows.Controls.Panel.Children%2A> di grandi dimensioni, considerare l'opportunità di utilizzare un oggetto <xref:System.Windows.Controls.VirtualizingStackPanel> anziché un normale oggetto <xref:System.Windows.Controls.StackPanel>.  
  
     Virtualizzando la raccolta figlio, <xref:System.Windows.Controls.VirtualizingStackPanel> determina il mantenimento in memoria solo degli oggetti che si trovano attualmente all'interno dell'oggetto [Riquadro di visualizzazione](GTMT) dell'elemento padre.  Di conseguenza, nella maggior parte degli scenari le prestazioni risultano notevolmente migliorate.  
  
<a name="LayoutSystem_LayoutRounding"></a>   
## Rendering dei subpixel e arrotondamento del layout  
 Il sistema grafico [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza unità indipendenti dal dispositivo per consentire l'indipendenza dalla risoluzione e dal dispositivo.  Ogni pixel indipendente dal dispositivo viene ridimensionato automaticamente in base all'impostazione dei [!INCLUDE[TLA#tla_dpi](../../../../includes/tlasharptla-dpi-md.md)] del sistema.  In questo modo, le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono ridimensionate correttamente per diverse impostazioni [!INCLUDE[TLA2#tla_dpi](../../../../includes/tla2sharptla-dpi-md.md)] e l'applicazione rileva automaticamente i [!INCLUDE[TLA2#tla_dpi](../../../../includes/tla2sharptla-dpi-md.md)].  
  
 Questa indipendenza dai [!INCLUDE[TLA2#tla_dpi](../../../../includes/tla2sharptla-dpi-md.md)] può tuttavia determinare un rendering irregolare dei bordi a causa dell'anti\-aliasing.  Questo fenomeno, che si presenta in genere sotto forma di bordi sfuocati o semitrasparenti, può verificarsi quando un bordo si trova in corrispondenza del centro di un pixel, anziché tra i pixel del dispositivo.  Il sistema di layout consente di regolare questo fenomeno con l'arrotondamento del layout.  L'arrotondamento del layout consiste nell'arrotondamento da parte del sistema di layout di qualsiasi valore di pixel non integrale durante il passaggio di layout.  
  
 L'arrotondamento del layout è disabilitato per impostazione predefinita.  Per abilitare l'arrotondamento del layout, impostare la proprietà <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> su `true` su qualsiasi oggetto <xref:System.Windows.FrameworkElement>.  Poiché si tratta di una proprietà di dipendenza, il valore verrà propagato a tutti gli elementi figlio nella struttura ad albero visuale.  Per abilitare l'arrotondamento del layout per l'intera interfaccia utente, impostare <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> su `true` sul contenitore radice.  Per un esempio, vedere <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A>.  
  
<a name="LayoutSystem_whatsnext"></a>   
## Argomenti successivi  
 La comprensione dei processi di misurazione e disposizione degli elementi illustrati nel primo passaggio è fondamentale per la comprensione del layout.  Per ulteriori informazioni sugli elementi <xref:System.Windows.Controls.Panel> disponibili, vedere [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md).  Per comprendere meglio le varie proprietà di posizionamento che possono influire sul layout, vedere [Panoramica su allineamento, margini e spaziatura interna](../../../../docs/framework/wpf/advanced/alignment-margins-and-padding-overview.md).  Per un esempio di elemento <xref:System.Windows.Controls.Panel> personalizzato, vedere [Esempio di pannello radiale personalizzato](http://go.microsoft.com/fwlink/?LinkID=159982) \(la pagina potrebbe essere in inglese\).  Per mettere in pratica tutte queste nozioni realizzando una semplice applicazione, vedere [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md).  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.UIElement>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Panoramica su allineamento, margini e spaziatura interna](../../../../docs/framework/wpf/advanced/alignment-margins-and-padding-overview.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)