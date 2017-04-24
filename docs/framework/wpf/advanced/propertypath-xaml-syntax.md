---
title: "Sintassi XAML di PropertyPath | Microsoft Docs"
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
  - "PropertyPath (oggetto)"
  - "XAML, PropertyPath (oggetto)"
ms.assetid: 0e3cdf07-abe6-460a-a9af-3764b4fd707f
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Sintassi XAML di PropertyPath
L'oggetto <xref:System.Windows.PropertyPath> supporta una sintassi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] inline complessa per l'impostazione di varie proprietà che accettano il tipo <xref:System.Windows.PropertyPath> come valore.  In questo argomento viene illustrata la sintassi di <xref:System.Windows.PropertyPath> applicata alle sintassi di animazione e di associazione.  
  
   
  
<a name="where"></a>   
## Utilizzo di PropertyPath  
 <xref:System.Windows.PropertyPath> è un oggetto comune utilizzato in diverse funzionalità [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Nonostante l'utilizzo dell'oggetto <xref:System.Windows.PropertyPath> comune per comunicare informazioni sul percorso della proprietà, l'impiego di ciascun'area di funzionalità in cui è utilizzato <xref:System.Windows.PropertyPath> come tipo variano.  È pertanto più pratico documentare le sintassi per ogni funzionalità.  
  
 Principalmente, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza <xref:System.Windows.PropertyPath> per descrivere i percorsi di modelli a oggetti per attraversare le proprietà di un'origine dati oggetto e per descrivere il percorso di destinazione per le animazioni di destinazione.  
  
 Alcune proprietà di stile e modello quali <xref:System.Windows.Setter.Property%2A?displayProperty=fullName> accettano un nome di proprietà qualificato in apparenza analogo a <xref:System.Windows.PropertyPath>.  Non si tratta tuttavia di un effettivo oggetto <xref:System.Windows.PropertyPath>, bensì dell'utilizzo di un formato stringa *proprietario.proprietà* qualificato, abilitato dal processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] WPF in combinazione con il convertitore dei tipi per <xref:System.Windows.DependencyProperty>.  
  
<a name="databinding_s"></a>   
## PropertyPath per oggetti in associazione dati  
 L'associazione dati è una funzionalità di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che consente di associare al valore di destinazione qualsiasi [proprietà di dipendenza](GTMT).  Tuttavia, l'origine di tale associazione dati non deve essere necessariamente una [proprietà di dipendenza](GTMT), ma può essere qualsiasi tipo di proprietà riconosciuto dal provider di dati applicabile.  I percorsi delle proprietà vengono utilizzati in particolare per <xref:System.Windows.Data.ObjectDataProvider>, utilizzato a sua volta per ottenere origini di associazione da oggetti [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] e dalle relative proprietà.  
  
 Si noti che l'associazione dati a [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] non utilizza <xref:System.Windows.PropertyPath>, poiché non utilizza <xref:System.Windows.Data.Binding.Path%2A> in <xref:System.Windows.Data.Binding>.  Utilizzare invece <xref:System.Windows.Data.Binding.XPath%2A> e specificare la sintassi XPath valida nel [!INCLUDE[TLA#tla_xmldom](../../../../includes/tlasharptla-xmldom-md.md)] dei dati.  La proprietà <xref:System.Windows.Data.Binding.XPath%2A> viene inoltre specificata come stringa, ma questo comportamento non è oggetto di trattazione in questa sede. Vedere [Eseguire l'associazione ai dati XML utilizzando un oggetto XMLDataProvider e le query XPath](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md).  
  
 Una chiave per comprendere i percorsi delle proprietà nell'associazione dati consiste nel distinguere se è possibile ottenere l'associazione a un singolo valore di proprietà o, viceversa, se è possibile l'associazione a proprietà di destinazione che utilizzano elenchi o raccolte.  Se si associano raccolte, ad esempio un oggetto <xref:System.Windows.Controls.ListBox> che si espanderà in base alla quantità di elementi di dati presenti nella raccolta, il percorso della proprietà deve fare riferimento all'oggetto Collection e non a singoli elementi della raccolta.  Il motore di associazione dati determinerà automaticamente la corrispondenza tra la raccolta utilizzata come origine dati e la destinazione dell'associazione, con il conseguente popolamento di un oggetto <xref:System.Windows.Controls.ListBox> con una matrice di elementi.  
  
<a name="singlecurrent"></a>   
### Proprietà singola sull'oggetto immediato come contesto dei dati  
  
```  
<Binding Path="propertyName" .../>  
```  
  
 *nomeProprietà* deve essere risolto nel nome di una proprietà contenuto nell'oggetto <xref:System.Windows.FrameworkElement.DataContext%2A> corrente per un utilizzo di <xref:System.Windows.Data.Binding.Path%2A>.  Se l'associazione aggiorna l'origine, tale proprietà deve essere di lettura\/scrittura e l'oggetto di origine deve essere modificabile.  
  
<a name="singleindex"></a>   
### Indicizzatore singolo sull'oggetto immediato come contesto dei dati  
  
```  
<Binding Path="[key]" .../>  
```  
  
 `key` deve essere l'indice tipizzato su un dizionario o una tabella hash oppure l'indice integer di una matrice.  Inoltre, il valore della chiave deve essere un tipo direttamente associabile alla proprietà a cui è applicato.  Ad esempio, una tabella hash che contiene chiavi di stringa e valori stringa può essere utilizzata in questo modo per l'associazione a testo per un oggetto <xref:System.Windows.Controls.TextBox>.  In alternativa, se la chiave punta a una raccolta di elementi o a un indice secondario, è possibile utilizzare questa sintassi per l'associazione a una proprietà di raccolta di destinazione.  In caso contrario, è necessario fare riferimento a una proprietà specifica, tramite una sintassi quale `<Binding Path="[``key``].``propertyName``" .../>`.  
  
 È possibile specificare il tipo dell'indice, se necessario.  Per informazioni dettagliate su questo aspetto del percorso di una proprietà indicizzata, vedere <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName>.  
  
<a name="multipleindirect"></a>   
### Più proprietà \(impostazione indiretta delle destinazioni delle proprietà\)  
  
```  
<Binding Path="propertyName.propertyName2" .../>  
```  
  
 `propertyName` deve essere risolto nel nome di una proprietà corrispondente all'oggetto <xref:System.Windows.FrameworkElement.DataContext%2A> corrente.  Le proprietà di percorso `propertyName` e `propertyName2` possono essere costituite da qualsiasi proprietà presente in una relazione, dove `propertyName2` è una proprietà esistente sul tipo che corrisponde al valore di `propertyName`.  
  
<a name="singleattached"></a>   
### Singola proprietà, connesso o qualificato dal tipo in altro modo  
  
```  
<object property="(ownerType.propertyName)" .../>  
```  
  
 Le parentesi indicano che questa proprietà in un oggetto <xref:System.Windows.PropertyPath> deve essere costruita utilizzando una qualifica parziale.  Può utilizzare uno spazio dei nomi XML per trovare il tipo con un mapping appropriato.  `ownerType` esegue la ricerca dei tipi a cui ha accesso un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], tramite le dichiarazioni <xref:System.Windows.Markup.XmlnsDefinitionAttribute> in ogni assembly.  Nella maggior parte delle applicazioni, lo spazio dei nomi XML predefinito è mappato allo spazio dei nomi [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)], pertanto un prefisso è in genere necessario solo per i tipi personalizzati o per i tipi che altrimenti sarebbero esterni allo spazio dei nomi.  `propertyName` deve essere risolto nel nome di una proprietà esistente nel parametro `ownerType`.  Questa sintassi viene in genere utilizzata per uno dei casi seguenti:  
  
-   Il percorso viene specificato in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], ovvero in uno stile o modello che non ha un tipo di destinazione specificato.  Un utilizzo qualificato non è generalmente valido in casi diversi da questo, poiché in casi non relativi a uno stile o a un modello, la proprietà esiste in un'istanza, non in un tipo.  
  
-   La proprietà è una proprietà associata.  
  
-   Viene eseguita l'associazione a una proprietà statica.  
  
 Per l'utilizzo come destinazione di storyboard, la proprietà specificata come `propertyName` deve essere un oggetto <xref:System.Windows.DependencyProperty>.  
  
<a name="sourcetraversal"></a>   
### Attraversamento di origine \(associazione a gerarchie di raccolte\)  
  
```  
<object Path="propertyName/propertyNameX" .../>  
```  
  
 Il carattere \/ in questa sintassi viene utilizzato per spostarsi in un oggetto di origine dati gerarchico; sono supportati più passaggi nella gerarchia con successivi caratteri \/.  L'attraversamento di origine tiene conto della posizione del puntatore a record corrente, determinata dalla sincronizzazione dei dati con l'interfaccia utente della relativa visualizzazione.  Per informazioni dettagliate sull'associazione a oggetti di origine dati gerarchici e per informazioni sul concetto di puntatore a record corrente nell'associazione dati, vedere [Utilizzare il modello Master\-Details con dati gerarchici](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md) o [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
> [!NOTE]
>  Questa sintassi è apparentemente analoga a [!INCLUDE[TLA2#tla_xpath](../../../../includes/tla2sharptla-xpath-md.md)].  Un'espressione [!INCLUDE[TLA2#tla_xpath](../../../../includes/tla2sharptla-xpath-md.md)] effettiva per l'associazione a un'origine dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] non viene utilizzata come valore di <xref:System.Windows.Data.Binding.Path%2A> e deve viceversa essere utilizzata per la proprietà <xref:System.Windows.Data.Binding.XPath%2A> reciprocamente esclusiva.  
  
### Visualizzazioni di raccolte  
 Per fare riferimento a una visualizzazione di raccolta denominata, premettere il carattere hash \(`#`\) al nome della visualizzazione di raccolta.  
  
### Puntatore al record corrente  
 Per fare riferimento al puntatore al record corrente relativo a una visualizzazione di raccolta o a uno scenario di associazione dati master\-dettagli, iniziare la stringa di percorso con una barra \(`/`\).  Qualsiasi percorso oltre la barra viene attraversato a partire dal puntatore al record corrente.  
  
### Più indicizzatori  
  
```  
<object Path="[index1,index2...]" .../>  
or  
<object Path="propertyName[index,index2...]" .../>  
```  
  
 Se un determinato oggetto supporta più indicizzatori, è possibile specificare tali indicizzatori in ordine, analogamente a una sintassi che fa riferimento a una matrice.  L'oggetto in questione può essere il contesto corrente o il valore di una proprietà contenente un oggetto a più indici.  
  
 Per impostazione predefinita, i valori dell'indicizzatore sono tipizzati utilizzando le caratteristiche dell'oggetto sottostante.  È possibile specificare il tipo dell'indice, se necessario.  Per informazioni dettagliate sugli indicizzatori, vedere <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName>.  
  
<a name="mixing"></a>   
### Sintassi miste  
 Tutte le sintassi illustrate in precedenza possono essere combinate.  Di seguito è riportato un esempio in cui viene creato un percorso di proprietà al colore in corrispondenza di un determinato punto x,y di una proprietà `ColorGrid` contenente una matrice griglia in pixel di oggetti <xref:System.Windows.Media.SolidColorBrush>:  
  
```  
<Rectangle Fill="{Binding ColorGrid[20,30].SolidColorBrushResult}" .../>  
```  
  
### Sequenze di escape per le stringhe di percorso delle proprietà  
 Per determinati oggetti business è possibile che si presenti un caso in cui la stringa di percorso della proprietà, per poter essere analizzata correttamente, richieda una sequenza di escape.  L'esigenza di utilizzare caratteri di escape deve essere rara, poiché molti di questi caratteri presentano problemi di denominazione\-interazione simili nei linguaggi che in genere vengono utilizzati per definire l'oggetto business.  
  
-   All'interno degli indicizzatori \(\[ \]\), l'accento circonflesso \(^\) funge da escape per il carattere successivo.  
  
-   È necessario utilizzare caratteri di escape \(con entità XML\) per alcuni caratteri specifici della definizione del linguaggio XML.  Utilizzare `&` come carattere di escape per il carattere "&".  Utilizzare `>` come carattere di escape per il tag di fine "\>".  
  
-   È necessario utilizzare un carattere di escape \(la barra rovesciata `\`\) per i caratteri specifici del comportamento del parser XAML di WPF relativo all'elaborazione di un'estensione di markup.  
  
    -   La stessa barra rovesciata \(`\`\) costituisce il carattere di escape.  
  
    -   Il segno di uguale \(`=`\) separa il nome della proprietà dal valore della proprietà.  
  
    -   Le proprietà vengono separate tramite virgola \(`,`\).  
  
    -   La parentesi graffa chiusa \(`}`\) rappresenta la fine di un'estensione di markup.  
  
> [!NOTE]
>  Tecnicamente, questi caratteri di escape funzionano anche per un percorso di proprietà di storyboard, ma in genere si attraversano modelli a oggetti per oggetti WPF esistenti e l'utilizzo di caratteri di escape non è necessario.  
  
<a name="databinding_sa"></a>   
## PropertyPath per le destinazioni di animazione  
 La proprietà di destinazione di un'animazione deve essere una [proprietà di dipendenza](GTMT) che accetta <xref:System.Windows.Freezable> o un tipo primitivo.  Possono tuttavia essere presenti su oggetti diversi la proprietà di destinazione su un tipo e la proprietà animata finale.  Per le animazioni, un percorso di proprietà viene utilizzato per definire la connessione tra la proprietà dell'oggetto di destinazione animato e la proprietà di animazione di destinazione prevista, attraverso le relazioni oggetto\-proprietà nei valori di proprietà.  
  
<a name="general"></a>   
### Considerazioni generali su oggetto\-proprietà per le animazioni  
 Per ulteriori informazioni sui concetti di animazione in generale, vedere [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md) e [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Il tipo di valore o la proprietà che verrà animata deve essere un tipo <xref:System.Windows.Freezable> o primitivo.  La proprietà che avvia il percorso deve essere risolta nel nome di una [proprietà di dipendenza](GTMT) esistente sul tipo <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> specificato.  
  
 Per supportare la duplicazione per l'animazione di un oggetto <xref:System.Windows.Freezable> già bloccato, l'oggetto specificato da <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> deve essere una classe derivata <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>.  
  
<a name="singlestepanim"></a>   
### Proprietà singola sull'oggetto di destinazione  
  
```  
<animation Storyboard.TargetProperty="propertyName" .../>  
```  
  
 `propertyName` deve essere risolto nel nome di una [proprietà di dipendenza](GTMT) esistente sul tipo <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> specificato.  
  
<a name="indirectanim"></a>   
### Impostazione indiretta delle destinazioni delle proprietà  
  
```  
<animation Storyboard.TargetProperty="propertyName.propertyName2" .../>  
```  
  
 `propertyName` deve essere una proprietà costituita da un tipo di valore <xref:System.Windows.Freezable> o primitivo, esistente sul tipo <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> specificato.  
  
 `propertyName2` deve essere il nome di una [proprietà di dipendenza](GTMT) esistente sull'oggetto che costituisce il valore di `propertyName`.  In altre parole, `propertyName2` deve esistente come proprietà di dipendenza sul tipo che costituisce `propertyName` <xref:System.Windows.DependencyProperty.PropertyType%2A>.  
  
 L'impostazione indiretta delle destinazioni delle animazioni è necessaria a causa degli stili e dei modelli applicati.  Per impostare la destinazione di un'animazione, è necessario <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> su un oggetto di destinazione e tale nome è stabilito da [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md) o <xref:System.Windows.FrameworkElement.Name%2A>.  Sebbene gli elementi di modello e stile possano avere nomi, tali nomi sono validi solo all'interno dell'ambito dei nomi dello stile e del modello.  Se modelli e stili non condividono gli ambiti dei nomi con il markup dell'applicazione, i nomi non possono essere univoci.  Stili e modelli sono condivisi letteralmente tra le istanze e trasmetterebbero nomi duplicati. Pertanto, se le singole proprietà di un elemento che si desidera animare provengono da uno stile o da un modello, è necessario iniziare con un'istanza di elemento denominato non proveniente da un modello di stile, quindi impostare la destinazione nella struttura ad albero visuale dello stile o del modello affinché arrivi alla proprietà che si desidera animare.  
  
 Ad esempio, la proprietà <xref:System.Windows.Controls.Panel.Background%2A> di un oggetto <xref:System.Windows.Controls.Panel> è un oggetto <xref:System.Windows.Media.Brush> completo \(ovvero un oggetto <xref:System.Windows.Media.SolidColorBrush>\) proveniente da un modello di tema.  Per animare completamente un oggetto <xref:System.Windows.Media.Brush>, sarebbe necessario BrushAnimation \(probabilmente uno per ogni tipo <xref:System.Windows.Media.Brush>\) e tale tipo non è presente.  Per animare un pennello, vengono invece animate le proprietà di un determinato tipo <xref:System.Windows.Media.Brush>.  È necessario ottenere da <xref:System.Windows.Media.SolidColorBrush> al relativo oggetto <xref:System.Windows.Media.SolidColorBrush.Color%2A> per applicarvi un oggetto <xref:System.Windows.Media.Animation.ColorAnimation>.  Il percorso della proprietà per questo esempio sarebbe `Background.Color`.  
  
<a name="attachedanim"></a>   
### Proprietà associate  
  
```  
<animation Storyboard.TargetProperty="(ownerType.propertyName)" .../>  
```  
  
 Le parentesi indicano che questa proprietà in un oggetto <xref:System.Windows.PropertyPath> deve essere costruita utilizzando una qualifica parziale.  È possibile utilizzare uno spazio dei nomi XML per trovare il tipo.  `ownerType` esegue la ricerca dei tipi a cui ha accesso un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], tramite le dichiarazioni <xref:System.Windows.Markup.XmlnsDefinitionAttribute> in ogni assembly.  Nella maggior parte delle applicazioni, lo spazio dei nomi XML predefinito è mappato allo spazio dei nomi [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)], pertanto un prefisso è in genere necessario solo per i tipi personalizzati o per i tipi che altrimenti sarebbero esterni allo spazio dei nomi.  `propertyName` deve essere risolto nel nome di una proprietà esistente nel parametro `ownerType`.  La proprietà specificata come `propertyName` deve essere <xref:System.Windows.DependencyProperty>.  Tutte le proprietà associate [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono implementate come proprietà di dipendenza, pertanto questo problema riguarda solo le proprietà associate personalizzate.  
  
<a name="indexanim"></a>   
### Indicizzatori  
  
```  
<animation Storyboard.TargetProperty="propertyName.propertyName2[index].propertyName3" .../>  
```  
  
 La maggior parte delle proprietà di dipendenza o i tipi <xref:System.Windows.Freezable> non supportano un indicizzatore.  Pertanto, l'unico utilizzo di un indicizzatore in un percorso di animazione è una posizione intermedia tra la proprietà che avvia la catena sulla destinazione denominata e la proprietà animata finale.  Nella sintassi fornita, si tratta di `propertyName2`.  Ad esempio, l'utilizzo di un indicizzatore può essere necessario se la proprietà intermedia è una raccolta quale <xref:System.Windows.Media.TransformGroup>, in un percorso di proprietà quale `RenderTransform.Children[1].Angle`.  
  
<a name="ppincode"></a>   
## PropertyPath nel codice  
 L'utilizzo del codice per <xref:System.Windows.PropertyPath>, inclusa la modalità di costruzione di <xref:System.Windows.PropertyPath>, è illustrato nell'argomento di riferimento relativo a <xref:System.Windows.PropertyPath>.  
  
 In genere, <xref:System.Windows.PropertyPath> è progettato per utilizzare due costruttori diversi, uno per gli utilizzi di associazione e di animazione più semplici e uno per gli utilizzi di animazione complessi.  Utilizzare la firma <xref:System.Windows.PropertyPath.%23ctor%28System.Object%29> per gli utilizzi di associazione, dove l'oggetto è una stringa.  Utilizzare la firma <xref:System.Windows.PropertyPath.%23ctor%28System.Object%29> per percorsi di animazione a un solo passaggio, dove l'oggetto è <xref:System.Windows.DependencyProperty>.  Utilizzare la firma [PropertyPath\(String, Object\<xref:System.Windows.PropertyPath.%23ctor%28System.String%2CSystem.Object%5B%5D%29> per le animazioni complesse.  Quest'ultimo costruttore utilizza una stringa token per il primo parametro e una matrice di oggetti che riempiono le posizioni nella stringa token per definire una relazione di percorso di proprietà.  
  
## Vedere anche  
 <xref:System.Windows.PropertyPath>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)