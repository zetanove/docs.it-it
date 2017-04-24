---
title: "Cenni preliminari sulle propriet&#224; di dipendenza | Microsoft Docs"
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
  - "proprietà associate"
  - "associazione dati"
  - "proprietà di dipendenza"
  - "proprietà, associate"
  - "proprietà, panoramica"
  - "risorse, riferimenti"
  - "stili"
ms.assetid: d119d00c-3afb-48d6-87a0-c4da4f83dee5
caps.latest.revision: 30
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# Cenni preliminari sulle propriet&#224; di dipendenza
In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] viene fornito un set di servizi che è possibile utilizzare per estendere la funzionalità di una proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  In genere, questi servizi vengono definiti collettivamente come sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Una proprietà supportata dal sistema delle proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è nota come [proprietà di dipendenza](GTMT). Nei cenni preliminari vengono descritti il sistema delle proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e le funzionalità di una [proprietà di dipendenza](GTMT). Viene anche spiegato come utilizzare le [proprietà di dipendenza](GTMT) esistenti in XAML e nel codice.  In questi cenni preliminari vengono anche illustrati aspetti specifici delle proprietà di dipendenza, ad esempio i metadati della proprietà di dipendenza e la creazione della proprietà di dipendenza in una classe personalizzata.  
  
   
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si presuppone che l'utente disponga di una conoscenza di base di [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] e della programmazione orientata a oggetti.  Per seguire gli esempi di questo argomento, è necessaria inoltre conoscere [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e la modalità di scrittura delle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Per ulteriori informazioni, vedere [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md).  
  
<a name="why_dependency_properties"></a>   
## Proprietà di dipendenza e proprietà CLR  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], le proprietà vengono generalmente esposte come proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  A un livello di base, si potrebbe interagire direttamente con queste proprietà senza sapere che vengono implementate come una [proprietà di dipendenza](GTMT).  Tuttavia, è necessario acquisire familiarità con alcune o tutte le funzionalità del sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], in modo da poterle sfruttare.  
  
 Lo scopo delle [proprietà di dipendenza](GTMT) consiste nel fornire un modo per calcolare il valore di una proprietà in base al valore di altri input.  Questi potrebbero includere proprietà del sistema, quali temi e preferenze dell'utente, meccanismi di determinazione della proprietà JIT, ad esempio associazione dati e animazionio storyboard, modelli multiuso, quali risorse e stili oppure valori noti tramite relazioni padre\-figlio con altri elementi della struttura ad albero dell'elemento.  Inoltre, una [proprietà di dipendenza](GTMT) può essere implementata per fornire una convalida autonoma, valori predefiniti, callback per il monitoraggio delle modifiche di altre proprietà, nonché un sistema che può assegnare valori della proprietà mediante la coercizione in base a potenziali informazioni di runtime.  Le classi derivate possono anche modificare alcune caratteristiche specifiche di una proprietà esistente, eseguendo l'override dei metadati della proprietà di dipendenza invece dell'override dell'implementazione effettiva delle proprietà esistenti oppure della creazione di nuove proprietà.  
  
 Nel riferimento SDK, è possibile identificare la proprietà di dipendenza grazie alla sezione Informazioni sulle proprietà di dipendenza, presente nella pagina di riferimento gestita per quella proprietà.  Nella sezione sono inclusi un collegamento al campo dell'identificatore <xref:System.Windows.DependencyProperty> per quella proprietà di dipendenza e un elenco delle opzioni dei metadati impostati per quella proprietà, informazioni sull'override per classe e altri dettagli.  
  
<a name="back_dependency_properties"></a>   
## Proprietà di dipendenza che supportano le proprietà CLR  
 [Le proprietà di dipendenza](GTMT) e il sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] estendono le funzionalità della proprietà fornendo un tipo che supporta una proprietà, come implementazione alternativa al modello standard di supporto della proprietà con un campo privato.  Questo tipo è denominato <xref:System.Windows.DependencyProperty>.  L'altro tipo importante che definisce il sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è <xref:System.Windows.DependencyObject>. L'oggetto <xref:System.Windows.DependencyObject> definisce la classe base che può essere registrata ed essere proprietario di una [proprietà di dipendenza](GTMT).  
  
 Di seguito viene riportato un riepilogo della terminologia utilizzata in questa documentazione [!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] per la descrizione delle [proprietà di dipendenza](GTMT):  
  
-   **Proprietà di dipendenza:** una proprietà supportata da un oggetto <xref:System.Windows.DependencyProperty>.  
  
-   **Identificatore della proprietà di dipendenza:** istanza di <xref:System.Windows.DependencyProperty>, ottenuta come valore restituito quando si registra una [proprietà di dipendenza](GTMT), quindi archiviata come membro statico di una classe.  Questo identificatore viene utilizzato come parametro per molte [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] che interagiscono con il sistema delle proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   **"Wrapper" CLR:** le effettive implementazioni ottenute e impostate della proprietà.  Queste implementazioni incorporano l'identificatore della proprietà di dipendenza utilizzandolo nelle chiamate agli oggetti <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A>, fornendo in tal modo il supporto alla proprietà tramite il sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Nell'esempio seguente viene definita la `IsSpinning` [proprietà di dipendenza](GTMT) e illustrata la relazione dell'identificatore <xref:System.Windows.DependencyProperty> con la proprietà supportata.  
  
 [!code-csharp[PropertiesOvwSupport#DPFormBasic](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#dpformbasic)]
 [!code-vb[PropertiesOvwSupport#DPFormBasic](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#dpformbasic)]  
[!code-csharp[PropertiesOvwSupport#DPFormBasic2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#dpformbasic2)]  
  
 La convenzione di denominazione della proprietà e del relativo campo <xref:System.Windows.DependencyProperty> di supporto è importante.  Il nome del campo è sempre il nome della proprietà al quale viene aggiunto il suffisso `Property`.  Per ulteriori informazioni su questa convenzione e i relativi motivi, vedere [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  
  
<a name="setting_property_values"></a>   
## Impostazione dei valori della proprietà  
 È possibile impostare le proprietà nel codice o in XAML.  
  
<a name="local_property_values"></a>   
### Impostazione dei valori della proprietà in XAML  
 Nell'esempio di XAML seguente viene specificato il colore di sfondo rosso per un pulsante.  In questo esempio viene illustrato un caso in cui il valore di stringa semplice per un attributo XAML viene convertito dal parser XAML WPF in un tipo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] \(<xref:System.Windows.Media.Color> tramite <xref:System.Windows.Media.SolidColorBrush>\) nel codice generato.  
  
 [!code-xml[PropertiesOvwSupport#MostBasicProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml#mostbasicproperty)]  
  
 XAML supporta diverse sintassi per l'impostazione delle proprietà.  La sintassi da utilizzare per una proprietà particolare dipende dal tipo di valore utilizzato da una proprietà e da altri fattori, quali la presenza di un convertitore dei tipi.  Per ulteriori informazioni sulla sintassi XAML per l'impostazione di proprietà, vedere [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md) e [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
 Come esempio di sintassi senza attributi, nell'esempio di XAML seguente viene illustrato lo sfondo di un altro pulsante.  Questa volta, invece di impostare un semplice colore a tinta unita, lo sfondo viene impostato su un'immagine, con un elemento che rappresenta tale immagine e la relativa origine, specificate come un attributo dell'elemento annidato.  Si tratta di un esempio di sintassi per gli elementi proprietà.  
  
 [!code-xml[PropertiesOvwSupport#PESyntaxProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml#pesyntaxproperty)]  
  
<a name="setting_properties_code"></a>   
### Impostazione delle proprietà nel codice  
 L'impostazione dei valori della [proprietà di dipendenza](GTMT) nel codice consiste, in genere, solo in una chiamata all'implementazione definita esposta dal "wrapper" [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  
  
 [!code-csharp[PropertiesOvwSupport#ProceduralPropertySet](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml.cs#proceduralpropertyset)]
 [!code-vb[PropertiesOvwSupport#ProceduralPropertySet](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page1.xaml.vb#proceduralpropertyset)]  
  
 Anche l'ottenimento di un valore della proprietà prevede sostanzialmente una chiamata all'implementazione del "wrapper" ottenuta:  
  
 [!code-csharp[PropertiesOvwSupport#ProceduralPropertyGet](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml.cs#proceduralpropertyget)]
 [!code-vb[PropertiesOvwSupport#ProceduralPropertyGet](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page1.xaml.vb#proceduralpropertyget)]  
  
 È inoltre possibile chiamare direttamente le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] del sistema di proprietà <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A>.  In genere, questa operazione non è necessaria se si stanno utilizzando proprietà esistenti \(i wrapper sono più utili e forniscono una migliore esposizione della proprietà per gli strumenti dello sviluppatore\), tuttavia la chiamata diretta delle [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] risulta appropriata per determinati scenari.  
  
 È anche possibile impostare le proprietà in XAML e successivamente accedervi nel codice tramite code\-behind.  Per informazioni dettagliate, vedere [Code\-behind e XAML in WPF](../../../../docs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md).  
  
<a name="functionality"></a>   
## Funzionalità della proprietà fornite da una proprietà di dipendenza  
 Una proprietà di dipendenza fornisce funzionalità che consentono di estendere la funzionalità di una proprietà, rispetto a una proprietà supportata da un campo.  Spesso, ciascuna di queste funzionalità rappresenta o supporta una funzione specifica dell'intero set di funzioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
-   [Risorse](#setting_properties_resources)  
  
-   [Associazione dati](#setting_properties_data_binding)  
  
-   [Stili](#setting_properties_styles)  
  
-   [Animations](#animations)  
  
-   [Override dei metadati](#metadata)  
  
-   [Ereditarietà del valore della proprietà](#setting_properties_inheritance)  
  
-   [Integrazione della finestra di Progettazione WPF](#vs2008_integration)  
  
<a name="setting_properties_resources"></a>   
### Risorse  
 Un valore della proprietà di dipendenza può essere impostato facendo riferimento a una risorsa.  Le risorse vengono in genere specificate come valore della proprietà `Resources` di un elemento radice della pagina o dell'applicazione \(questi percorsi consentono un accesso più semplice alla risorsa\).  Nell'esempio seguente viene illustrato come definire una risorsa <xref:System.Windows.Media.SolidColorBrush>.  
  
 [!code-xml[PropertiesOvwSupport#ResourcesResource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page2.xaml#resourcesresource)]  
  
 Una volta definita, è possibile fare riferimento alla risorsa e utilizzarla per fornire un valore della proprietà:  
  
 [!code-xml[PropertiesOvwSupport#ResourcesReference](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page2.xaml#resourcesreference)]  
  
 A questa risorsa particolare viene fatto riferimento come [Estensione del markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md) \(in XAML WPF è possibile utilizzare un riferimento di risorsa statica o dinamica\).  Per utilizzare un riferimento di risorsa dinamica, è necessario eseguire l'impostazione su una proprietà di dipendenza, in modo che il sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] attivi l'utilizzo spedifico del riferimento di risorsa dinamica.  Per ulteriori informazioni, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
> [!NOTE]
>  Le risorse vengono considerate come valore locale, per cui se si imposta un altro valore locale, il riferimento di risorsa sarà eliminato.  Per ulteriori informazioni, vedere [Precedenza del valore della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md).  
  
<a name="setting_properties_data_binding"></a>   
### Associazione dati  
 Una proprietà di dipendenza può fare riferimento a un valore tramite l'associazione dati.  Quest'ultima funziona tramite una sintassi per estensione di markup specifica in XAML o nell'oggetto <xref:System.Windows.Data.Binding> nel codice.  Con l'associazione dati, la determinazione del valore della proprietà finale viene rinviata fino al runtime, momento in cui il valore viene ottenuto da un'origine dati.  
  
 Nell'esempio seguente viene impostata la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> per un oggetto <xref:System.Windows.Controls.Button>, utilizzando un'associazione dichiarata in XAML.  L'associazione utilizza un contesto dati ereditato e un'origine dati <xref:System.Windows.Data.XmlDataProvider> \(non visualizzata\).  L'associazione stessa specifica la proprietà di origine desiderata mediante l'oggetto <xref:System.Windows.Data.Binding.XPath%2A> all'interno dell'origine dati.  
  
 [!code-xml[PropertiesOvwSupport#BasicInlineBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#basicinlinebinding)]  
  
> [!NOTE]
>  Le associazioni vengono considerate come valore locale, per cui se si imposta un altro valore locale, l'associazione sarà eliminata.  Per informazioni dettagliate, vedere [Precedenza del valore della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md).  
  
 Le proprietà di dipendenza o la classe <xref:System.Windows.DependencyObject> non supportano in modo nativo l'oggetto <xref:System.ComponentModel.INotifyPropertyChanged> per la produzione delle notifiche delle modifiche del valore della proprietà di origine <xref:System.Windows.DependencyObject> per le operazioni di associazione dati.  Per ulteriori informazioni su come creare proprietà da utilizzare nell'associazione dati che consentano di segnalare modifiche di una destinazione di associazione dati, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
<a name="setting_properties_styles"></a>   
### Stili  
 Stili e modelli sono due degli scenari principali che giustificano l'utilizzo delle proprietà di dipendenza.  Gli stili sono particolarmente utili per l'impostazione di proprietà che definiscono l'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] dell'applicazione.  In genere gli stili vengono definiti come risorse in XAML.  e interagiscono con il sistema di proprietà in quanto di solito contengono metodi di impostazione per proprietà particolari, nonché "trigger" che modificano un valore della proprietà in base al valore in tempo reale per un'altra proprietà.  
  
 Nell'esempio seguente viene creato uno stile molto semplice \(definito all'interno di un dizionario <xref:System.Windows.FrameworkElement.Resources%2A>, non visualizzato\) che viene successivamente applicato direttamente alla proprietà <xref:System.Windows.FrameworkElement.Style%2A> di un oggetto <xref:System.Windows.Controls.Button>.  Il metodo di impostazione dello stile imposta la proprietà <xref:System.Windows.Controls.Control.Background%2A> di un oggetto <xref:System.Windows.Controls.Button> a cui è stato applicato uno stile sul colore verde.  
  
 [!code-xml[PropertiesOvwSupport#SimpleStyleDef](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#simplestyledef)]  
  
 [!code-xml[PropertiesOvwSupport#SimpleStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#simplestyle)]  
  
 Per ulteriori informazioni, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
<a name="animations"></a>   
### Animations  
 Alle proprietà di dipendenza è possibile aggiungere un'animazione.  Quando un'animazione viene applicata ed è in esecuzione, il valore a cui è stata aggiunta un'animazione opera a un livello di precedenza superiore rispetto a qualsiasi altro valore \(ad esempio un valore locale\) di cui la proprietà dispone.  
  
 Nell'esempio seguente viene aggiunta un'animazione all'oggetto <xref:System.Windows.Controls.Control.Background%2A> in una proprietà <xref:System.Windows.Controls.Button>. Tecnicamente, all'oggetto <xref:System.Windows.Controls.Control.Background%2A> viene aggiunta un'animazione utilizzando la sintassi per elementi della proprietà per specificare un oggetto <xref:System.Windows.Media.SolidColorBrush> vuoto come oggetto <xref:System.Windows.Controls.Control.Background%2A>, quindi la proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> di quell'oggetto <xref:System.Windows.Media.SolidColorBrush> è la proprietà a cui viene aggiunta direttamente l'animazione.  
  
 [!code-xml[PropertiesOvwSupport#MiniAnimate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#minianimate)]  
  
 Per ulteriori informazioni sull'animazione di proprietà, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md) e [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
<a name="metadata"></a>   
### Override dei metadati  
 È possibile modificare determinati comportamenti di una [proprietà di dipendenza](GTMT) eseguendo l'override dei metadati per quella proprietà, quando si deriva dalla classe che registra originariamente la [proprietà di dipendenza](GTMT).  L'esecuzione dell'override dei metadati si basa sull'identificatore <xref:System.Windows.DependencyProperty>.  L'esecuzione dell'override dei metadati non richiede una nuova implementazione della proprietà.  La modifica dei metadati viene gestita in modo nativo dal sistema di proprietà; ogni classe contiene, potenzialmente, i metadati specifici per tutte le proprietà ereditate dalle classi base, in base al tipo.  
  
 Nell'esempio seguente viene eseguito l'override dei metadati per una proprietà di dipendenza <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A>.  L'esecuzione dell'override dei metadati di questa particolare proprietà di dipendenza fa parte di un modello di implementazione che consente di creare controlli che possono utilizzare stili predefiniti dai temi.  
  
 [!code-csharp[PropertiesOvwSupport#OverrideMetadata](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml.cs#overridemetadata)]
 [!code-vb[PropertiesOvwSupport#OverrideMetadata](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page3.xaml.vb#overridemetadata)]  
  
 Per ulteriori informazioni sull'override o su come ottenere i metadati delle proprietà, vedere [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
<a name="setting_properties_inheritance"></a>   
### Ereditarietà del valore della proprietà  
 Un elemento può ereditare il valore di una proprietà di dipendenza dal relativo elemento padre nella struttura ad albero di oggetti.  
  
> [!NOTE]
>  Il comportamento dell'ereditarietà del valore della proprietà non viene abilitato a livello globale per tutte le proprietà di dipendenza, poiché il tempo di calcolo per l'ereditarietà influisce negativamente sulle prestazioni.  In genere, l'ereditarietà del valore della proprietà viene abilitata solo per le proprietà in cui uno scenario particolare suggerisce che tale ereditarietà è appropriata.  La possibilità di ereditare di una proprietà di dipendenza può essere determinata consultando la sezione **relativa alle informazioni sulle proprietà di dipendenza** per una determinata proprietà di dipendenza, nel riferimento SDK.  
  
 Nell'esempio seguente viene descritta un'associazione e impostata la proprietà <xref:System.Windows.FrameworkElement.DataContext%2A> che specifica l'origine dell'associazione, non illustrata nell'esempio di associazione precedente.  Non è necessario che le associazioni successive negli oggetti figlio specifichino l'origine in quanto possono utilizzare il valore ereditato da <xref:System.Windows.FrameworkElement.DataContext%2A> nell'oggetto <xref:System.Windows.Controls.StackPanel> padre.  In alternativa, un oggetto figlio potrebbe invece specificare direttamente il relativo valore <xref:System.Windows.FrameworkElement.DataContext%2A> o <xref:System.Windows.Data.Binding.Source%2A> nell'oggetto <xref:System.Windows.Data.Binding> e non utilizzare il valore ereditato per il contesto dati delle relative associazioni.  
  
 [!code-xml[PropertiesOvwSupport#InheritanceContext](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#inheritancecontext)]  
  
 Per ulteriori informazioni, vedere [Ereditarietà del valore della proprietà](../../../../docs/framework/wpf/advanced/property-value-inheritance.md).  
  
<a name="vs2008_integration"></a>   
### Integrazione della finestra di Progettazione WPF  
 Un controllo personalizzato con proprietà implementate come proprietà di dipendenza riceverà un supporto [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] appropriato.  Un esempio è rappresentato dalla capacità di modificare proprietà di dipendenza dirette e associate tramite la finestra **Proprietà**.  Per ulteriori informazioni, vedere [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
<a name="value_determination"></a>   
## Precedenza del valore della proprietà di dipendenza  
 Quando si ottiene il valore di una [proprietà di dipendenza](GTMT), si ottiene un valore che era stato impostato in quella proprietà tramite uno qualsiasi degli altri input basati sulla proprietà che partecipano al sistema di proprietà di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  La precedenza del valore della proprietà di dipendenza consente a una varietà di scenari relativi alla modalità di ottenimento dei valori da parte delle proprietà di interagire in modo prevedibile.  
  
 Prendere in considerazione l'esempio riportato di seguito.  Nell'esempio viene incluso uno stile applicato a tutti i pulsanti e alle relative proprietà <xref:System.Windows.Controls.Control.Background%2A>; tuttavia viene anche specificato un pulsante con un valore <xref:System.Windows.Controls.Control.Background%2A> impostato localmente.  
  
> [!NOTE]
>  Nella documentazione SDK i termini "valore locale" o "valore impostato localmente" vengono utilizzati talvolta per la descrizione delle proprietà di dipendenza.  Un valore impostato localmente è un valore di proprietà che viene impostato direttamente in un'istanza di oggetto nel codice o come attributo di un elemento in XAML.  
  
 In teoria, per il primo pulsante la proprietà viene impostata due volte, ma viene applicato un solo valore, quello con la precedenza più elevata.  Un valore impostato localmente ha la massima precedenza \(eccetto per un'animazione in esecuzione; tuttavia, in questo esempio non viene applicata nessuna animazione\), pertanto per lo sfondo del primo pulsante viene utilizzato il valore impostato localmente anziché il valore del metodo di impostazione dello stile.  Il secondo pulsante non dispone di un valore locale \(e di nessun altro valore con precedenza più elevata rispetto a un metodo di impostazione dello stile\), pertanto lo sfondo di quel pulsante proviene dal metodo di impostazione dello stile.  
  
 [!code-xml[PropertiesOvwSupport#MiniPrecedence](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#miniprecedence)]  
  
### Ragioni dell'esistenza della precedenza della proprietà di dipendenza  
 In genere, non si desidera che gli stili vengano sempre applicati e che nascondano persino un valore impostato localmente di un singolo elemento \(altrimenti sarebbe molto difficile utilizzare gli stili o gli elementi in generale\).  Pertanto, i valori che provengono dagli stili operano a un livello di precedenza inferiore rispetto a un valore impostato localmente.  Per un elenco più completo delle proprietà di dipendenza e per la possibile provenienza di un valore effettivo di una proprietà di dipendenza, vedere [Precedenza del valore della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md).  
  
> [!NOTE]
>  Molte proprietà definite negli elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non sono proprietà di dipendenza.  In generale, le proprietà vengono implementate come proprietà di dipendenza solo quando è necessario supportare almeno uno degli scenari abilitati dal sistema di proprietà: associazione dati, applicazione degli stili, animazione, supporto del valore predefinito, ereditarietà, proprietà associate o annullamento della convalida.  
  
<a name="dp_implement_roadmap"></a>   
## Ulteriori informazioni sulle proprietà di dipendenza  
  
-   Una [proprietà associata](GTMT) è un tipo di proprietà che supporta una sintassi specializzata in XAML.  Una proprietà associata spesso non dispone di una corrispondenza 1:1 con una proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] e non è necessariamente una [proprietà di dipendenza](GTMT).  Lo scopo tipico di una [proprietà associata](GTMT) consiste nel consentire agli elementi figlio di segnalare i valori della proprietà a un elemento padre, anche se quest'ultimo e l'elemento figlio non possiedono tale proprietà, come parte degli elenchi dei membri della classe.  Uno scenario principale prevede la possibilità per gli elementi figlio di informare l'elemento padre del modo in cui vengono presentati nell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]; per un esempio, vedere <xref:System.Windows.Controls.DockPanel.Dock%2A> o <xref:System.Windows.Controls.Canvas.Left%2A>.  Per informazioni dettagliate, vedere [Cenni preliminari sulle proprietà associate](../../../../docs/framework/wpf/advanced/attached-properties-overview.md).  
  
-   Gli sviluppatori di componenti o di applicazioni possono decidere di creare una [proprietà di dipendenza](GTMT) personalizzata al fine di abilitare funzionalità quali l'associazione dati o il supporto degli stili oppure per il supporto dell'annullamento della convalida e della coercizione del valore.  Per informazioni dettagliate, vedere [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  
  
-   Generalmente, le proprietà di dipendenza devono essere considerate come proprietà pubbliche, accessibili o almeno individuabili da parte di qualsiasi chiamante con accesso a un'istanza.  Per ulteriori informazioni, vedere [Sicurezza della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-security.md).  
  
## Vedere anche  
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Proprietà di dipendenza di sola lettura](../../../../docs/framework/wpf/advanced/read-only-dependency-properties.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Architettura WPF](../../../../docs/framework/wpf/advanced/wpf-architecture.md)