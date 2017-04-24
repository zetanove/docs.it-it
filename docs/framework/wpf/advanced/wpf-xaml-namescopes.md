---
title: "NameScope XAML WPF | Microsoft Docs"
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
  - "API, correlate ai nomi"
  - "classi, FrameworkContentElement"
  - "classi, FrameworkElement"
  - "classi, RegisterName"
  - "FrameworkContentElement (classe)"
  - "FrameworkElement (classe)"
  - "correlate ai nomi (API)"
  - "ambiti dei nomi"
  - "RegisterName (classe)"
  - "stili, ambiti dei nomi"
  - "modelli, ambiti dei nomi"
  - "XAML, ambiti dei nomi"
ms.assetid: 52bbf4f2-15fc-40d4-837b-bb4c21ead7d4
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# NameScope XAML WPF
Con NameScope XAML vengono identificati oggetti definiti in XAML.  I nomi in un NameScope XAML può essere utilizzato per stabilire relazioni tra i nomi di oggetti definiti in XAML e gli equivalenti delle istanze in una struttura ad albero di oggetti.  In genere, i NameScope XAML in codice gestito [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono creati quando si caricano i singoli elementi radice di pagina per un'applicazione XAML.  I NameScope XAML come oggetto di programmazione vengono definiti dall'interfaccia <xref:System.Windows.Markup.INameScope> e sono anche implementati dalla classe pratica <xref:System.Windows.NameScope>.  
  
   
  
<a name="Namescopes_in_Loaded_XAML_Applications"></a>   
## Ambiti dei nomi in applicazioni XAML caricate  
 In un contesto di programmazione o di informatica più ampio, tra i concetti di programmazione è spesso incluso il principio di un identificatore o di un nome univoco utilizzabile per accedere a un oggetto.  Per sistemi che utilizzano identificatori o nomi, il NameScope definisce i limiti entro cui verrà eseguita la ricerca di un oggetto con il dato nome da parte di un processo o una tecnica o i limiti entro cui è l'applicata l'univocità di identificazione dei nomi.  Questi principi generali si applicano ai NameScope XAML.  I NameScope XAML vengono creati nell'elemento radice per una pagina XAML al momento dell'elaborazione di tale pagina.  Ogni nome specificato all'interno della pagina XAML a partire dalla radice della pagina viene aggiunto a un NameScope XAML pertinente.  
  
 In XAML WPF, gli elementi che rappresentano elementi radice comuni \(ad esempio <xref:System.Windows.Controls.Page> e <xref:System.Windows.Window>\) controllano sempre un NameScope XAML.  Se un elemento quale <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> è l'elemento radice della pagina nel markup, un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] aggiunge in modo implicito una radice <xref:System.Windows.Controls.Page> affinché <xref:System.Windows.Controls.Page> possa fornire un NameScope XAML funzionante.  
  
> [!NOTE]
>  Le azioni di compilazione di WPF creano un NameScope XAML per una produzione XAML anche se non viene definito alcun attributo `Name` o `x:Name` su alcun elemento nel markup [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 Se si tenta di utilizzare due volte lo stesso nome in qualsiasi NameScope XAML, viene generata un'eccezione.  Per XAML di WPF che presenta code\-behind e fa parte di un'applicazione compilata, l'eccezione viene generata in fase di compilazione da parte delle azioni di compilazione di WPF, quando si crea la classe generata per la pagina durante la compilazione del markup iniziale.  Per XAML non compilato dal markup da parte di alcuna azione di compilazione, possono venire generate eccezioni correlate con problemi di NameScope XAML quando viene caricato il codice XAML.  Le finestre di progettazione XAML possono inoltre anticipare i problemi di NameScope XAML in case di progettazione.  
  
### Aggiunta di oggetti a strutture ad albero di oggetti in fase di esecuzione  
 Il momento in cui il codice XAML viene analizzato rappresenta il momento in cui viene creato e definito un NameScope XAML WPF.  Se si aggiunge un oggetto a una struttura ad albero di oggetti in un punto nel tempo successivo all'analisi del codice XAML che ha prodotto tale struttura ad albero, un valore `Name` o `x:Name` sul nuovo oggetto non aggiorna automaticamente le informazioni un NameScope XAML.  Per aggiungere un nome per un oggetto in un NameScope XAML WPF dopo il caricamento del codice XAML, è necessario chiamare l'implementazione appropriata di <xref:System.Windows.Markup.INameScope.RegisterName%2A> sull'oggetto che definisce il NameScope XAML che in genere è la radice della pagina XAML.  Se il nome non è registrato, non è possibile fare riferimento all'oggetto aggiunto tramite nome mediante metodi quali <xref:System.Windows.FrameworkElement.FindName%2A> e non è possibile utilizzare tale nome per assegnare la destinazione dell'animazione.  
  
 Lo scenario più comune per gli sviluppatori di applicazioni è costituito dall'utilizzo di <xref:System.Windows.FrameworkElement.RegisterName%2A> per registrare nomi nel NameScope XAML sulla radice corrente della pagina.  <xref:System.Windows.FrameworkElement.RegisterName%2A> fa parte di uno scenario importante di storyboard destinati agli oggetti per le animazioni.  Per ulteriori informazioni, vedere [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
 Se si chiama <xref:System.Windows.FrameworkElement.RegisterName%2A> su un oggetto diverso dall'oggetto che definisce i NameScope XAML, il nome viene comunque registrato nel NameScope XAML in cui è contenuto l'oggetto chiamante, come se fosse stato chiamato <xref:System.Windows.FrameworkElement.RegisterName%2A> sull'oggetto di definizione del NameScope XAML.  
  
### NameScope XAML nel codice  
 È possibile creare e quindi utilizzare NameScope XAML nel codice.  Le API utilizzate e i concetti implicati nella creazione di NameScope XAML sono i medesimi anche per l'utilizzo del codice puro, poiché vengono impiegati dal processore XAML per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] durante l'elaborazione del codice XAML stesso.  I concetti e le API hanno lo scopo principale di consentire la ricerca di oggetti per nome all'interno di una struttura ad albero di oggetti, in genere definita parzialmente o internamente in XAML.  
  
 Per le applicazioni create a livello di codice e non da XAML caricato, l'oggetto che definisce un NameScope XAML deve implementare <xref:System.Windows.Markup.INameScope> o essere una classe derivata <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>, per supportare la creazione di un NameScope XAML nelle proprie istanze.  
  
 Inoltre, per qualsiasi elemento che non viene caricato ed elaborato da un processore XAML, il NameScope XAML per l'oggetto non viene creato né inizializzato per impostazione predefinita.  È necessario creare in modo esplicito un nuovo NameScope XAML per ogni oggetto nel quale si intende successivamente registrare nomi.  Per creare un NameScope XAML per un elemento, chiamare il metodo <xref:System.Windows.NameScope.SetNameScope%2A> statico.  Specificare l'oggetto proprietario come parametro `dependencyObject` e una nuova chiamata al costruttore <xref:System.Windows.NameScope.%23ctor%2A> come parametro `value`.  
  
 Se l'oggetto fornito come `dependencyObject` per <xref:System.Windows.NameScope.SetNameScope%2A> non è un'implementazione di <xref:System.Windows.Markup.INameScope>, <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>, la chiamata a <xref:System.Windows.FrameworkElement.RegisterName%2A> su qualsiasi elemento figlio non avrà effetto.  Se non si riesce a creare in modo esplicito il nuovo NameScope XAML, le chiamate a <xref:System.Windows.FrameworkElement.RegisterName%2A> genereranno un'eccezione.  
  
 Per un esempio dell'utilizzo delle API dei NameScope XAML nel codice, vedere [Definire un ambito del nome](../../../../docs/framework/wpf/graphics-multimedia/how-to-define-a-name-scope.md).  
  
<a name="Namescopes_in_Styles_and_Templates"></a>   
## NameScope XAML negli stili e nei modelli  
 Stili e i modelli in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] offrono la possibilità di riutilizzare e riapplicare il contenuto in modo semplice.  Tuttavia, stili e modelli possono anche includere elementi con nomi XAML definiti a livello del modello.  Lo stesso modello potrebbe essere utilizzato più volte in una pagina.  Per questo motivo, stili e modelli definiscono entrambi i relativi NameScope XAML, indipendentemente dalla posizione in una struttura ad albero di oggetti in cui viene applicato lo stile o il modello.  
  
 Si consideri l'esempio seguente:  
  
 [!code-xml[XamlOvwSupport#NameScopeTemplates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page6.xaml#namescopetemplates)]  
  
 In questo caso, lo stesso modello viene applicato a due pulsanti diversi.  Se i modelli non disponessero di NameScope XAML discreti, il nome `TheBorder` utilizzato nel modello provocherebbe un conflitto di nomi nel NameScope XAML.  Poiché ogni creazione di un'istanza del modello dispone di un proprio NameScope XAML, in questo esempio ciascun NameScope XAML del modello di cui è stata creata un'istanza contiene esattamente un nome.  
  
 Anche gli stili definiscono il relativo NameScope XAML, principalmente in modo tale che sia possibile assegnare determinati nomi alle parti degli storyboard.  Questi nomi attivano comportamenti specifici di controllo destinati a elementi di tale nome, anche se il modello è stato ridefinito come parte della personalizzazione del controllo.  
  
 A causa dei NameScope XAML separati, l'individuazione di elementi denominati in un modello è più complessa rispetto all'individuazione di un elemento denominato non basato su modelli in una pagina.  Per prima cosa, è necessario determinare il modello applicato, ottenendo il valore della proprietà <xref:System.Windows.Controls.Control.Template%2A> del controllo in cui è applicato il modello.  Quindi, chiamare la versione del modello di <xref:System.Windows.FrameworkTemplate.FindName%2A>, passando il controllo in cui era applicato il modello come secondo parametro.  
  
 Se l'autore di un controllo genera una convenzione in cui un determinato elemento denominato in un modello applicato è la destinazione per un comportamento definito dal controllo stesso, può utilizzare il metodo <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> dal codice di implementazione del controllo.  Il metodo <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> è protetto, di conseguenza solo l'autore del controllo può accedervi.  
  
 Se si opera dall'interno un modello ed è necessario accedere al NameScope XAML in cui viene applicato il modello, ottenere il valore di <xref:System.Windows.FrameworkElement.TemplatedParent%2A>, quindi chiamare <xref:System.Windows.FrameworkElement.FindName%2A>.  Un esempio di questo tipo di operazione è il caso in cui si scrive l'implementazione del gestore eventi in cui verrà generato l'evento da un elemento in un modello applicato.  
  
<a name="Namescopes_and_Name_related_APIs"></a>   
## API relative ai nomi e ai NameScope XAML  
 <xref:System.Windows.FrameworkElement> dispone dei metodi <xref:System.Windows.FrameworkElement.FindName%2A>, <xref:System.Windows.FrameworkElement.RegisterName%2A> e <xref:System.Windows.FrameworkElement.UnregisterName%2A>.  Se l'oggetto su cui si chiamano questi metodi è proprietario di un NameScope XAML, i metodi dell'elemento vengono semplicemente chiamati nei metodi del NameScope XAML.  In caso contrario, l'elemento padre viene controllato per verificare se è proprietario di un NameScope XAML e questo processo continua in modo ricorsivo fino a quando non viene trovato un NameScope XAML \(a causa del comportamento del processore XAML, è garantito che vi sia un ambito dei nomi in corrispondenza della radice\).  <xref:System.Windows.FrameworkContentElement> presenta comportamenti analoghi, con l'eccezione che nessun oggetto <xref:System.Windows.FrameworkContentElement> sarà mai proprietario di NameScope XAML.  I metodi sono presenti in <xref:System.Windows.FrameworkContentElement> affinché sia possibile inoltrare le chiamate in ultima analisi a un elemento padre <xref:System.Windows.FrameworkElement>.  
  
 <xref:System.Windows.NameScope.SetNameScope%2A> viene utilizzato per eseguire il mapping di un nuovo NameScope XAML a un oggetto esistente.  È possibile chiamare <xref:System.Windows.NameScope.SetNameScope%2A> più di una volta per reimpostare o cancellare il NameScope XAML, ma non si tratta di un utilizzo comune.  Inoltre, in genere <xref:System.Windows.NameScope.GetNameScope%2A> non viene utilizzato dal codice.  
  
### Implementazioni dei NameScope XAML  
 Le classi riportate di seguito implementano direttamente <xref:System.Windows.Markup.INameScope>:  
  
-   <xref:System.Windows.NameScope>  
  
-   <xref:System.Windows.Style>  
  
-   <xref:System.Windows.ResourceDictionary>  
  
-   <xref:System.Windows.FrameworkTemplate>  
  
 <xref:System.Windows.ResourceDictionary> non utilizza nomi o NameScope XAML, ma chiavi perché si tratta di un'implementazione di dizionario.  L'unico motivo per cui <xref:System.Windows.ResourceDictionary> implementa <xref:System.Windows.Markup.INameScope> è che in questo modo può generare eccezioni al codice utente che rendono più chiara la distinzione tra un NameScope XAML effettivo e la modalità di gestione delle chiavi di <xref:System.Windows.ResourceDictionary>, oltre ad assicurare che i NameScope XAML non vengano applicati in particolare a <xref:System.Windows.ResourceDictionary> da parte di elementi padre.  
  
 <xref:System.Windows.FrameworkTemplate> e <xref:System.Windows.Style> implementano <xref:System.Windows.Markup.INameScope> tramite definizioni di interfaccia esplicite.  Le implementazioni esplicite consentono a questi NameScope XAML di mantenere un comportamento convenzionale quando vi si accede tramite l'interfaccia <xref:System.Windows.Markup.INameScope>, che rappresenta il modo in cui i NameScope XAML sono comunicati dai processi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] interni.  Ma le definizioni di interfaccia esplicite non fanno parte della superficie dell'API convenzionale di <xref:System.Windows.FrameworkTemplate> e <xref:System.Windows.Style>, poiché raramente è necessario chiamare direttamente i metodi <xref:System.Windows.Markup.INameScope> su <xref:System.Windows.FrameworkTemplate> e <xref:System.Windows.Style> e si utilizza un'API differente, quale <xref:System.Windows.FrameworkElement.GetTemplateChild%2A>.  
  
 Le classi riportate di seguito definiscono il proprio NameScope XAML, utilizzando la classe di supporto <xref:System.Windows.NameScope?displayProperty=fullName> e connettendosi all'implementazione del relativo NameScope XAML tramite la proprietà associata <xref:System.Windows.NameScope.NameScope%2A?displayProperty=fullName>:  
  
-   <xref:System.Windows.FrameworkElement>  
  
-   <xref:System.Windows.FrameworkContentElement>  
  
## Vedere anche  
 [Spazi dei nomi XAML e mapping dello spazio dei nomi per XAML WPF](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)   
 [Direttiva x:Name](../../../../docs/framework/xaml-services/x-name-directive.md)