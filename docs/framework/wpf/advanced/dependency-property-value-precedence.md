---
title: "Precedenza del valore della propriet&#224; di dipendenza | Microsoft Docs"
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
  - "classi, proprietarie di proprietà Dependency"
  - "proprietà di dipendenza, classi come proprietarie"
  - "proprietà di dipendenza, metadati"
  - "metadati, proprietà di dipendenza"
ms.assetid: 1fbada8e-4867-4ed1-8d97-62c07dad7ebc
caps.latest.revision: 27
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# Precedenza del valore della propriet&#224; di dipendenza
<a name="introduction"></a> In questo argomento viene illustrato il modo in cui i meccanismi del sistema di proprietà [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] possono influire sul valore di una [proprietà di dipendenza](GTMT) e viene descritta la precedenza in base alla quale gli aspetti del sistema di proprietà si applicano al valore effettivo di una proprietà.  
  
   
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si presuppone la conoscenza delle proprietà di dipendenza dal punto di vista di un consumer delle proprietà di dipendenza esistenti nelle classi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], nonché la lettura di [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  Per capire gli esempi illustrati in questo argomento, è necessaria inoltre la conoscenza di [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e della procedura di scrittura delle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
<a name="intro"></a>   
## Il sistema di proprietà WPF  
 Il sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] offre un potente strumento per consentire la determinazione del valore delle proprietà di dipendenza in base a numerosi fattori, abilitando funzionalità quali la convalida delle proprietà in tempo reale, l'associazione tardiva e la notifica alle proprietà correlate delle modifiche ai valori di altre proprietà.  L'ordine e logica precisi utilizzati per determinare i valori delle proprietà di dipendenza sono piuttosto complessi.  La conoscenza di questo ordine consentirà di evitare l'impostazione dì proprietà non necessarie e potrebbe anche eliminare i dubbi sui motivi precisi per i quali alcuni tentativi di influenzare o anticipare un valore delle proprietà di dipendenza non hanno determinato il valore atteso.  
  
<a name="multiple_sets"></a>   
## Le proprietà di dipendenza possono essere impostate in più punti  
 Di seguito viene riportato un esempio di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] in cui la stessa proprietà \(<xref:System.Windows.Controls.Control.Background%2A>\) dispone di tre operazioni di impostazione diverse che potrebbero influenzare il valore.  
  
 [!code-xml[PropertiesOvwSupport#DPPrecedence](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml#dpprecedence)]  
  
 In questo caso, quale colore ci si aspetta che verrà applicato, rosso, verde o blu?  
  
 Ad eccezione dei valori animati e della coercizione, gli insiemi di proprietà locali vengono impostati con la precedenza più elevata.  Se si imposta localmente un valore, è possibile prevedere che il valore venga accettato, anche al di là degli stili o dei modelli di controllo.  In questo esempio, <xref:System.Windows.Controls.Control.Background%2A> viene impostato localmente su Rosso.  Pertanto, lo stile definito in questo ambito, anche se è uno stile implicito che diversamente si applicherebbe a tutti gli elementi di quel tipo in quell'ambito, non ha la precedenza più elevata per assegnare alla proprietà <xref:System.Windows.Controls.Control.Background%2A> il relativo valore.  Se è stato rimosso il valore locale di Rosso dall'istanza di quel Pulsante, lo stile avrà la precedenza e il pulsante otterrà il valore dello sfondo dallo stile.  All'interno dello stile, i trigger assumono la precedenza, pertanto il pulsante sarà blu se il mouse è posizionato su di esso e verde in caso contrario.  
  
<a name="listing"></a>   
## Elenco delle precedenze per l'impostazione delle proprietà di dipendenza  
 Di seguito viene riportato l'ordine definitivo utilizzato dal sistema di proprietà per l'assegnazione dei valori di runtime delle proprietà di dipendenza.  La precedenza più elevata viene elencata per prima.  Questo elenco si basa su alcuni dei concetti generali espressi in [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
1.  **Coercizione del sistema di proprietà** Per informazioni dettagliate sulla coercizione, vedere [Coercizione, animazione e valore di base](#animations) più avanti in questo argomento.  
  
2.  **Animazioni attive o animazioni con un comportamento di attesa.** Per ottenere qualsiasi effetto pratico, l'animazione di una proprietà deve essere in grado di avere la precedenza sul valore di base \(inanimato\), anche se quel valore è stato impostato localmente.  Per informazioni dettagliate, vedere [Coercizione, animazione e valore di base](#animations) più avanti in questo argomento.  
  
3.  **Valore locale** Un valore locale potrebbe essere impostato tramite la praticità della proprietà "wrapper", che equivale anche all'impostazione come un attributo o un elemento della proprietà in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], oppure da una chiamata all'[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]<xref:System.Windows.DependencyObject.SetValue%2A> utilizzando una proprietà di un'istanza specifica.  Se si imposta un valore locale utilizzando un'associazione o una risorsa, ciascuno di questi elementi dispone della precedenza come se fosse stato impostato un valore diretto.  
  
4.  **Proprietà del modello TemplatedParent.** Un elemento dispone di <xref:System.Windows.FrameworkElement.TemplatedParent%2A> se è stato creato come parte di un modello \(<xref:System.Windows.Controls.ControlTemplate> o <xref:System.Windows.DataTemplate>\).  Per informazioni dettagliate sulle situazioni in cui viene applicato, vedere [TemplatedParent](#templatedparent) più avanti in questo argomento.  All'interno del modello, viene applicata la seguente precedenza:  
  
    1.  Trigger dal modello <xref:System.Windows.FrameworkElement.TemplatedParent%2A>.  
  
    2.  Insiemi di proprietà \(in genere tramite attributi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] \) nel modello <xref:System.Windows.FrameworkElement.TemplatedParent%2A>.  
  
5.  **Stile implicito** Si applica solo alla proprietà `Style`.  La proprietà `Style` viene riempita da qualsiasi risorsa di stile con una chiave che corrisponde al tipo di quell'elemento.  Quella risorsa di stile deve essre presente nella pagina o nell'applicazione; la ricerca per una risorsa di stile implicita non viene eseguita nei temi.  
  
6.  **Trigger degli stili** I trigger all'interno di stili da una pagina o un'applicazione \(questi stili potrebbero essere stili espliciti o impliciti, ma non derivati dagli stili predefiniti, che dispongono di una precedenza inferiore\).  
  
7.  **Trigger dei modelli.** Qualsiasi trigger da un modello all'interno di uno stile oppure un modello direttamente applicato.  
  
8.  **Metodi per l'impostazione di stili** Valori da <xref:System.Windows.Setter> all'interno di stili da pagine o applicazioni.  
  
9. **Stile \(tema\) predefinito** Per informazioni dettagliate sui casi in cui viene applicato e sul modo in cui gli stili del tema si riferiscono ai modelli all'interno degli stili del tema, vedere [Stili \(tema\) predefiniti](#themestyles) più avanti in questo argomento.  All'interno di uno stile predefinito, viene applicato il seguente ordine di precedenza:  
  
    1.  Trigger attivi nello stile del tema.  
  
    2.  Metodi per l'impostazione nello stile del tema.  
  
10. **Ereditarietà.** Alcune proprietà di dipendenza ereditano i propri valori dall'elemento padre agli elementi figlio, in modo che non devono essere specificamente impostati su ogni elemento in tutta l'applicazione.  Per informazioni dettagliate, vedere [Ereditarietà del valore della proprietà](../../../../docs/framework/wpf/advanced/property-value-inheritance.md).  
  
11. **Valore predefinito dai metadati delle proprietà di dipendenza** Qualsiasi proprietà di dipendenza specificata può avere un valore predefinito come stabilito dalla registrazione del sistema di proprietà di quella particolare proprietà.  Inoltre, le classi derivate che ereditano una proprietà di dipendenza hanno la possibilità di eseguire l'override di tali metadati \(incluso il valore predefinito\) in base al tipo.  Per ulteriori informazioni, vedere [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  Poiché l'ereditarietà è controllata prima del valore predefinito, per una proprietà ereditata un valore predefinito dell'elemento padre assume la precedenza su un elemento figlio.  Di conseguenza, se una proprietà ereditabile non viene impostata ovunque, viene utilizzato il valore predefinito come specificato nella radice o nell'elemento padre anziché il valore predefinito dell'elemento figlio.  
  
<a name="templatedparent"></a>   
## TemplatedParent  
 TemplatedParent come un elemento di precedenza non si applica a qualsiasi proprietà di un elemento che viene dichiarata direttamente nel markup dell'applicazione standard.  Il concetto di TemplatedParent esiste solo per elementi figlio all'interno di una struttura ad albero visuale che vengono creati tramite l'applicazione del modello.  Quando il sistema di proprietà ricerca un valore nel modello <xref:System.Windows.FrameworkElement.TemplatedParent%2A>, sta cercando il modello che ha creato quell'elemento.  I valori della proprietà dal modello <xref:System.Windows.FrameworkElement.TemplatedParent%2A> generalmente agiscono come se fossero stati impostati come un valore locale nell'elemento figlio, ma questa precedenza inferiore rispetto al valore locale è presente perché i modelli sono potenzialmente condivisi.  Per informazioni dettagliate, vedere <xref:System.Windows.FrameworkElement.TemplatedParent%2A>.  
  
<a name="style_property"></a>   
## Proprietà Style  
 L'ordine di ricerca descritto in precedenza si applica a tutte le possibili proprietà di dipendenza tranne una: la proprietà <xref:System.Windows.FrameworkElement.Style%2A>.  La proprietà <xref:System.Windows.FrameworkElement.Style%2A> è unica poiché ad essa non può essere applicato uno stile, quindi gli elementi di precedenza da 5 a 8 non vengono applicati.  Inoltre, l'animazione o la coercizione di <xref:System.Windows.FrameworkElement.Style%2A> non sono consigliate \(e l'animazione di <xref:System.Windows.FrameworkElement.Style%2A> richiederebbe una classe di animazione personalizzata\).  Rimangono così tre modalità in cui la proprietà <xref:System.Windows.FrameworkElement.Style%2A> può essere impostata:  
  
-   **Stile esplicito** La proprietà <xref:System.Windows.FrameworkElement.Style%2A> viene impostata direttamente.  Nella maggior parte degli scenari, lo stile non viene definito inline, ma viene invece indicato come una risorsa, tramite una chiave esplicita.  In questo caso la stessa proprietà Style agisce come se fosse un valore locale, elemento di precedenza 3.  
  
-   **Stile implicito** La proprietà <xref:System.Windows.FrameworkElement.Style%2A> non viene impostata direttamente.  Tuttavia, <xref:System.Windows.FrameworkElement.Style%2A> è presente a qualche livello nella sequenza della ricerca di risorse \(pagina, applicazione\) e viene aggiunta utilizzando una chiave di risorsa che corrisponde al tipo al quale deve essere applicato lo stile.  In questo caso, la stessa proprietà <xref:System.Windows.FrameworkElement.Style%2A> agisce in base a una precedenza identificata nella sequenza come elemento 5.  Questa condizione può essere rilevata utilizzando <xref:System.Windows.DependencyPropertyHelper> rispetto alla proprietà <xref:System.Windows.FrameworkElement.Style%2A> e cercando <xref:System.Windows.BaseValueSource> nei risultati.  
  
-   **Stile predefinito**, anche noto come **stile del tema**. La proprietà <xref:System.Windows.FrameworkElement.Style%2A> non viene impostata direttamente e infatti verrà letta come `null` fino alla fase di esecuzione.  In questo caso, lo stile deriva dalla valutazione del tema di runtime che fa parte del motore di presentazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Per gli stili impliciti non inclusi nei temi, il tipo deve corrispondere esattamente: una classe derivata da `MyButton` `Button` non utilizzerà in modo implicito uno stile per `Button`.  
  
<a name="themestyles"></a>   
## Stili \(tema\) predefiniti  
 Ogni controllo fornito con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dispone di uno stile predefinito.  Potenzialmente, lo stile predefinito varia in base al tema, motivo per il quale questo stile predefinito viene indicato in alcuni casi come uno stile del tema.  
  
 L'informazione più importante presente all'interno di un stile predefinito per un controllo è il relativo modello di controllo, presente nello stile del tema come un metodo per l'impostazione della proprietà <xref:System.Windows.Controls.Control.Template%2A>.  Se non esistesse un modello derivato dagli stili predefiniti, un controllo senza un modello personalizzato come parte di uno stile personalizzato non presenterebbe alcun aspetto visivo.  Il modello derivato dallo stile predefinito fornisce all'aspetto visivo di ciascun controllo una struttura di base e definisce anche le connessioni tra proprietà definite nella struttura ad albero visuale del modello e la classe di controlli corrispondente.  Ciascun controllo espone un insieme di proprietà che può influenzare l'aspetto visivo del controllo senza sostituire completamente il modello.  Ad esempio, si consideri l'aspetto visivo predefinito di un controllo <xref:System.Windows.Controls.Primitives.Thumb>, che è un componente di <xref:System.Windows.Controls.Primitives.ScrollBar>.  
  
 <xref:System.Windows.Controls.Primitives.Thumb> dispone di determinate proprietà personalizzabili.  Il modello predefinito di <xref:System.Windows.Controls.Primitives.Thumb> crea una struttura\/struttura ad albero visuale di base con molti componenti <xref:System.Windows.Controls.Border> annidati per creare un aspetto smussato.  Se una proprietà che fa parte del modello deve essere esposta per la personalizzazione dalla classe <xref:System.Windows.Controls.Primitives.Thumb>, quella proprietà deve essere esposta da [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md), all'interno del modello.  Nel caso di <xref:System.Windows.Controls.Primitives.Thumb>, le varie proprietà di questi bordi condividono un modello che esegue l'associazione a proprietà quali <xref:System.Windows.Controls.Border.Background%2A> o <xref:System.Windows.Controls.Border.BorderThickness%2A>.  Ma certe altre proprietà o disposizioni visive sono impostate come specificate a livello di codice \(hard\-coded\) nel modello di controllo o sono associate a valori che derivano direttamente dal tema e non possono essere modificate senza sostituire l'intero modello.  Generalmente, se una proprietà deriva da un elemento padre basato su modelli e non viene esposta da un'associazione di modelli, non può essere regolato dagli stili poiché non esiste un modo semplice per fare riferimento ad essa.  Ma tale proprietà potrebbe essere ancora influenzata dall'ereditarietà dei valore della proprietà nel modello applicato oppure dal valore predefinito.  
  
 Gli stili del tema utilizzano un tipo come chiave nelle definizioni.  Tuttavia, quando i temi sono applicati all'istanza di un determinato elemento, la ricerca dei temi per questo tipo viene eseguita controllando la proprietà <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> in un controllo.  Questa operazione è in contrasto con l'utilizzo del tipo letterale, adottato dagli stili impliciti.  Il valore di <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> verrebbe ereditato dalle classi derivate anche se l'implementatore non lo modificasse \(la modalità desiderata per la modifica della proprietà è non eseguirne l'override al livello della proprietà, ma modificarne invece il valore predefinito nei metadati della proprietà\).  Questo riferimento indiretto consente alle classi di base di definire gli stili del tema per gli elementi derivati che non dispongono di un altro stile \(oppure, in un caso più importante, che non dispongono di un modello all'interno di quello stile e che di conseguenza non presenterebbero alcun aspetto visivo predefinito\).  In questo modo, è possibile derivare `MyButton` da <xref:System.Windows.Controls.Button> e ottenere ancora il modello predefinito <xref:System.Windows.Controls.Button>.  Nel caso l'utente fosse l'autore dei controlli di `MyButton` e si desiderasse un comportamento diverso, sarebbe possibile eseguire l'override dei metadati della proprietà di dipendenza per <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> in `MyButton` per restituire una chiave diversa, quindi definire gli stili del tema attinenti incluso il modello per `MyButton` che è necessario inserire nel controllo `MyButton`.  Per ulteriori dettagli su temi, stili e creazione di controlli, vedere [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
<a name="resources"></a>   
## Riferimenti e associazione di risorse dinamiche.  
 I riferimenti alle risorse dinamiche e le operazioni di associazione rispettano la precedenza della posizione su cui sono impostati.  Ad esempio, una risorsa dinamica applicata a un valore locale agisce in base all'elemento di precedenza 3, ad un'associazione per un metodo per l'impostazione di una proprietà all'interno di un stile del tema viene applicato un elemento di precedenza 9 e così via.  Poiché i riferimenti e l'associazione alle risorse dinamiche devono essere in grado di ottenere valori dallo stato della fase di esecuzione dell'applicazione, ciò comporta che anche il processo effettivo di determinazione della precedenza del valore di proprietà per qualsiasi proprietà specificata si estende nella fase di esecuzione.  
  
 I riferimenti alle risorse dinamiche non fanno parte in senso stretto del sistema di proprietà, ma dispongono di un proprio ordine di ricerca che interagisce con la sequenza elencata in precedenza.  Tale precedenza è documentata più approfonditamente in [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  La somma di base di tale precedenza è: elemento alla radice della pagina, applicazione, tema, sistema.  
  
 Le risorse dinamiche e le associazioni hanno la precedenza relativamente a dove sono state impostate, ma il valore viene rinviato.  Una conseguenza di ciò è che, se si imposta una risorsa dinamica o un'associazione su un valore locale, qualsiasi modifica al valore locale sostituisce completamente la risorsa dinamica o l'associazione.  Anche se si chiama il metodo <xref:System.Windows.DependencyObject.ClearValue%2A> per cancellare il valore impostato localmente, la risorsa dinamica o l'associazione non verrà ripristinata.  Infatti, se si chiama <xref:System.Windows.DependencyObject.ClearValue%2A> in una proprietà che dispone di una risorsa dinamica o di un'associazione \(senza valore locale letterale\), anche queste vengono cancellate dalla chiamata <xref:System.Windows.DependencyObject.ClearValue%2A>.  
  
<a name="setcurrentvalue"></a>   
## SetCurrentValue  
 Il metodo <xref:System.Windows.DependencyObject.SetCurrentValue%2A> è un altro modo per impostare una proprietà, ma non è in ordine di precedenza.  Viceversa, <xref:System.Windows.DependencyObject.SetCurrentValue%2A> consente di modificare il valore di una proprietà senza sovrascrivere l'origine di un valore precedente.  È possibile utilizzare <xref:System.Windows.DependencyObject.SetCurrentValue%2A> ogni volta che si desidera impostare un valore senza assegnare a tale valore la precedenza di un valore locale.  Ad esempio, se una proprietà è impostata da un trigger e successivamente viene assegnato un altro valore tramite <xref:System.Windows.DependencyObject.SetCurrentValue%2A>, il sistema delle proprietà rispetta comunque il trigger e la proprietà cambia se si verifica l'azione del trigger.  <xref:System.Windows.DependencyObject.SetCurrentValue%2A> consente di modificare il valore della proprietà senza fornire ad essa un'origine con una precedenza più elevata.  Analogamente, è possibile utilizzare <xref:System.Windows.DependencyObject.SetCurrentValue%2A> per modificare il valore di una proprietà senza sovrascrivere un'associazione.  
  
<a name="animations"></a>   
## Coercizione, animazioni e valore di base  
 La coercizione e l'animazione agiscono entrambe su un valore indicato come "valore di base" in tutto l'[!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)].  Di conseguenza, il valore di base è un qualsiasi valore determinato tramite la valutazione verso l'alto negli elementi fino a raggiungere l'elemento 2.  
  
 Per un'animazione, il valore di base può avere un effetto sul valore animato, se quell'animazione non specifica le impostazioni "From" e "To" per determinati comportamenti o se l'animazione ripristina intenzionalmente il valore di base quando viene completata.  Per osservare questo comportamento nella pratica, eseguire l'[esempio di valori di destinazione dell'animazione From\/To\/By](http://go.microsoft.com/fwlink/?LinkID=159988) \(la pagina potrebbe essere in inglese\).  Tentare di impostare i valori locali dell'altezza del rettangolo nell'esempio, in modo che il valore locale iniziale sia diverso da qualsiasi impostazione "From" nell'animazione.  Si noterà che le animazioni iniziano immediatamente utilizzando i valori "From" valori e sostituiscono il valore di base una volta avviate.  Una volta completata, l'animazione potrebbe indicare di ritornare al valore trovato prima dell'animazione specificando <xref:System.Windows.Media.Animation.FillBehavior> Stop.  In seguito, verrà utilizzata la precedenza normale per la determinazione del valore di base.  
  
 Possono essere applicate più animazioni a una sola proprietà, ognuna delle quali è stata definita da punti diversi nella precedenza dei valori.  Tuttavia, queste animazioni comporranno i relativi valori, piuttosto che applicare semplicemente l'animazione dalla precedenza più elevata.  Ciò dipende dal modo preciso in cui sono definite le animazioni e dal tipo del valore che viene animato.  Per ulteriori informazioni sull'animazione di proprietà, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 La coercizione si applica al livello più elevato in assoluto.  Anche un'animazione già in esecuzione è soggetta alla coercizione del valore.  Alcune proprietà di dipendenza esistenti in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dispongono di una coercizione incorporata.  Per una proprietà di dipendenza personalizzata, il comportamento di coercizione viene definito scrivendo <xref:System.Windows.CoerceValueCallback> e passando il callback come parte dei metadati quando si crea la proprietà.  È anche possibile eseguire l'override del comportamento di coercizione di proprietà esistenti eseguendo l'override dei metadati di quella proprietà in una classe derivata.  La coercizione interagisce con il valore di base in modo tale che i vincoli di coercizione vengano applicati come i vincoli esistenti in quel momento, mantenendo tuttavia il valore di base.  Pertanto, se i vincoli nella coercizione vengono rimossi in un secondo momento, la coercizione restituirà il valore più vicino possibile a quel valore di base e l'influenza della coercizione su una proprietà cesserà appena tutti i vincoli verranno rimossi.  Per ulteriori informazioni sul comportamento di coercizione, vedere [Callback e convalida delle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md).  
  
<a name="triggers"></a>   
## Comportamenti dei trigger  
 I controlli spesso definiscono i comportamenti dei trigger come parte dello stile predefinito nei temi.  L'impostazione di proprietà locali sui controlli può impedire ai trigger di essere in grado di rispondere agli eventi generati dagli utenti sia da un punto di vista visivo sia da un punto di vista di comportamento.  L'utilizzo più comune di un trigger di proprietà è quello relativo alle proprietà di controllo o di stato come <xref:System.Windows.Controls.Primitives.Selector.IsSelected%2A>.  Ad esempio, per impostazione predefinita quando <xref:System.Windows.Controls.Button> viene disabilitato \(trigger per <xref:System.Windows.UIElement.IsEnabled%2A> è `false`\) il valore <xref:System.Windows.Controls.Control.Foreground%2A> nello stile del tema è quello che determina l'aspetto inattivo del controllo.  Ma se è stato impostato un valore <xref:System.Windows.Controls.Control.Foreground%2A> locale, il normale colore relativo allo stato inattivo verrà ignorato in base alla precedenza dall'insieme di proprietà locali, anche in questo scenario attivato da proprietà.  Prestare attenzione nell'impostazione di valori per proprietà che presentano comportamenti di trigger a livello di tema e accertarsi di non interferire impropriamente con l'esperienza utente desiderata per quel controllo.  
  
<a name="clearvalue"></a>   
## ClearValue e precedenza dei valori  
 Il metodo <xref:System.Windows.DependencyObject.ClearValue%2A> fornisce un modo efficace per cancellare tutti i valori applicati localmente da una [proprietà di dipendenza](GTMT) impostata su un elemento.  Tuttavia, chiamare <xref:System.Windows.DependencyObject.ClearValue%2A> non rappresenta una garanzia del fatto che l'impostazione predefinita come stabilita nei metadati durante la registrazione della proprietà sia il nuovo valore effettivo.  Tutti gli altri partecipanti nella precedenza dei valori ancora sono attivi.  Solo il valore impostato localmente è stato rimosso dalla sequenza di precedenza.  Ad esempio, se si chiama <xref:System.Windows.DependencyObject.ClearValue%2A> su una proprietà in cui quella proprietà è impostata anche da uno stile del tema, il valore del tema viene applicato come il nuovo valore anziché come l'impostazione predefinita basata sui metadati.  Se si desidera eliminare tutti i partecipanti dei valori di proprietà dal processo e impostare il valore sull'impostazione predefinita dei metadati registrati, è possibile ottenere definitivamente quel valore predefinito eseguendo una query sui metadati della proprietà di dipendenza e successivamente sarà possibile utilizzare il valore predefinito per impostare localmente la proprietà con una chiamata a <xref:System.Windows.DependencyObject.SetValue%2A>.  
  
## Vedere anche  
 <xref:System.Windows.DependencyObject>   
 <xref:System.Windows.DependencyProperty>   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Callback e convalida delle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)