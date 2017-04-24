---
title: "Cenni preliminari sulle propriet&#224; associate | Microsoft Docs"
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
  - "proprietà associate [Progettazione WPF]"
ms.assetid: 75928354-dc01-47e8-a018-8409aec1f32d
caps.latest.revision: 28
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 27
---
# Cenni preliminari sulle propriet&#224; associate
Una proprietà associata è un concetto definito da XAML.  Una proprietà associata deve essere utilizzata come un tipo di proprietà globale che è possibile impostare su qualsiasi oggetto.  in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], le proprietà associate sono in genere definito come un tipo specializzato di proprietà di dipendenza che non dispone della proprietà “wrapper„ convenzionale.  
  
   
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si presuppone la conoscenza delle proprietà di dipendenza dal punto di vista di un consumer delle proprietà di dipendenza esistenti nelle classi [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], nonché la lettura di [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  Per seguire gli esempi di questo argomento, è necessaria inoltre la comprensione di XAML e della modalità di scrittura [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applicazioni.  
  
<a name="attached_properties_usage"></a>   
## Vantaggi offerti dall'utilizzo delle proprietà associate  
 Una delle finalità di una proprietà associata consiste nel consentire a diversi elementi figlio di specificare valori univoci di una proprietà effettivamente definita in un elemento padre.  Un'applicazione specifica di questo scenario consente agli elementi figlio di notificare all'elemento padre la modalità con cui devono essere presentati nell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  Un esempio è rappresentato dalla proprietà <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>.  La proprietà <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> viene creata come proprietà associata perché è progettata in modo da essere impostata sugli elementi contenuti all'interno di un oggetto <xref:System.Windows.Controls.DockPanel>, anziché sull'oggetto <xref:System.Windows.Controls.DockPanel> stesso.  La classe <xref:System.Windows.Controls.DockPanel> definisce il campo <xref:System.Windows.DependencyProperty> statico denominato <xref:System.Windows.Controls.DockPanel.DockProperty> e fornisce quindi i metodi <xref:System.Windows.Controls.DockPanel.GetDock%2A> e <xref:System.Windows.Controls.DockPanel.SetDock%2A> come funzioni di accesso pubbliche per la [proprietà associata](GTMT).  
  
<a name="attached_properties_xaml"></a>   
## Proprietà associate in XAML  
 In XAML, è possibile impostare le proprietà associate utilizzando la sintassi *AttachedPropertyProvider*.*PropertyName*  
  
 Di seguito viene riportato un esempio della procedura di impostazione di <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> in XAML:  
  
 [!code-xml[PropertiesOvwSupport#APBasicUsage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml#apbasicusage)]  
  
 Notare che l'utilizzo è sotto certi aspetti simile a una proprietà statica; si fa sempre riferimento al tipo <xref:System.Windows.Controls.DockPanel> proprietario della [proprietà associata](GTMT) e in grado di registrarla, piuttosto che a qualsiasi istanza specificata per nome.  
  
 Inoltre, poiché una proprietà associata in XAML è un attributo che viene impostato nel markup, solo l'operazione di impostazione ha una certa rilevanza.  Non è possibile ottenere direttamente una proprietà in XAML, sebbene esistano alcuni meccanismi indiretti per confrontare i valori, ad esempio i trigger negli stili \(per informazioni dettagliate, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)\).  
  
### Implementazione delle proprietà associate in WPF  
 in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], la maggior parte delle proprietà associate esistenti in  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] i tipi correlati alla presentazione dell'interfaccia utente vengono implementate come proprietà di dipendenza.  le proprietà associate sono un concetto di XAML, mentre le proprietà di dipendenza sono a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] concetto.  Poiché [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] le proprietà associate sono proprietà di dipendenza, supportano concetti di proprietà di dipendenza come metadati delle proprietà e i valori predefiniti.  
  
<a name="howused"></a>   
## Utilizzo delle proprietà associate da parte del tipo proprietario  
 Anche se le proprietà associate possono essere impostate su qualsiasi oggetto, ciò non significa che l'impostazione della proprietà produce un risultato tangibile o che il valore sarà utilizzato da un altro oggetto.  In genere, le proprietà associate sono concepite in modo che gli oggetti provenienti da un'ampia varietà di possibili gerarchie di classi o di relazioni logiche possano ciascuno riportare informazioni comuni al tipo che definisce la proprietà associata.  Il tipo che definisce la proprietà associata si attiene di regola a uno di questi modelli:  
  
-   Il tipo che definisce la proprietà associata è progettato in modo da poter essere l'elemento padre degli elementi che imposteranno i valori per la proprietà associata.  Il tipo scorre quindi gli oggetti figlio attraverso la logica interna in base a una struttura ad albero degli oggetti, ottiene i valori e agisce in qualche modo su tali valori.  
  
-   Il tipo che definisce la proprietà associata sarà utilizzato come elemento figlio per diversi elementi padre e modelli di contenuto possibili.  
  
-   Il tipo che definisce la proprietà associata rappresenta un servizio.  Gli altri tipi impostano i valori per la proprietà associata.  Pertanto, quando l'elemento che imposta la proprietà viene valutato nel contesto del servizio, i valori della proprietà associata vengono ottenuti tramite la logica interna della classe del servizio.  
  
### Esempio di proprietà associata definita dall'elemento padre  
 Lo scenario più tipico in cui [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] definisce una proprietà associata è quello in cui un elemento padre supporta una raccolta di elementi figlio e implementa inoltre un comportamento tale che le specifiche del comportamento vengono segnalate singolarmente per ogni elemento figlio.  
  
 L'oggetto <xref:System.Windows.Controls.DockPanel> definisce la proprietà associata <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> e l'oggetto <xref:System.Windows.Controls.DockPanel> dispone di un codice a livello di classe come parte della logica di rendering \(in particolare, gli oggetti <xref:System.Windows.Controls.DockPanel.MeasureOverride%2A> e <xref:System.Windows.Controls.DockPanel.ArrangeOverride%2A>\).  Un'istanza di <xref:System.Windows.Controls.DockPanel> verificherà sempre se uno dei relativi elementi figlio immediati ha impostato un valore per la proprietà <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>.  In questo caso, tali valori diventano l'input per la logica di rendering applicata a quel particolare elemento figlio.  Le istanze annidate di <xref:System.Windows.Controls.DockPanel> gestiscono ciascuna le proprie raccolte di elementi figlio immediati; tuttavia tale comportamento varia in base all'implementazione, a seconda del modo in cui <xref:System.Windows.Controls.DockPanel> elabora i valori <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>.  In teoria è possibile che alcune proprietà associate abbiano effetto su elementi più distanti dell'elemento padre immediato.  Se la proprietà associata <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> è impostata su un elemento sul quale non agisce alcun elemento padre <xref:System.Windows.Controls.DockPanel>, non verranno generati errori o eccezioni.  Ciò significa semplicemente che un valore della proprietà globale è stato impostato, ma al momento non è presente alcun elemento padre <xref:System.Windows.Controls.DockPanel> che possa utilizzare le informazioni.  
  
<a name="attached_properties_code"></a>   
## Proprietà associate nel codice  
 Le proprietà associate in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non dispongono dei tipici metodi "wrapper" [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] per ottenere o impostare facilmente l'accesso.  Ciò è dovuto al fatto che la proprietà associata non è necessariamente inclusa nello spazio dei nomi [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] per le istanze in cui la proprietà è impostata.  Tuttavia, un processore XAML deve essere in grado di impostare tali valori quando il codice XAML viene analizzato.  Per supportare un efficace utilizzo della proprietà associata, il tipo proprietario della proprietà associata deve implementare i metodi della funzione di accesso dedicati nel form `ottenere`*Nomeproprietà* e `set`*Nomeproprietà*.  Questi metodi della funzione di accesso dedicati sono anche utili per ottenere o impostare la proprietà associata nel codice.  Dal punto di vista del codice, una proprietà associata è simile a un campo di backup che dispone di funzioni di accesso ai metodi anziché di funzioni di accesso alle proprietà e tale campo di backup può trovarsi in qualsiasi oggetto senza che sia necessario definirlo in modo specifico.  
  
 Nell'esempio seguente viene illustrato come impostare una proprietà associata nel codice.  In questo esempio, `myCheckBox` è un'istanza della classe <xref:System.Windows.Controls.CheckBox>.  
  
 [!code-csharp[PropertiesOvwSupport#APCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#apcode)]
 [!code-vb[PropertiesOvwSupport#APCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#apcode)]  
  
 Analogamente al caso di XAML, se `myCheckBox` non è stato aggiunto come elemento figlio di  `myDockPanel` la terza riga di codice, la quarta riga di codice non questo un'eccezione, ma il valore della proprietà non potrebbe con un oggetto  <xref:System.Windows.Controls.DockPanel> il padre e non farebbe pertanto alcuna operazione.  Solo un valore di <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> impostato su un elemento figlio combinato con la presenza di un elemento padre <xref:System.Windows.Controls.DockPanel> produrrà un comportamento effettivo nell'applicazione sottoposta a rendering.  In questo caso, è possibile impostare la proprietà associata, quindi effettuare l'associazione alla struttura ad albero.  In alternativa, è possibile effettuare l'associazione alla struttura ad albero, quindi impostare la proprietà associata.  Qualunque sia l'ordine delle azioni, il risultato è il medesimo.  
  
<a name="attached_properties_metadata"></a>   
## Metadati della proprieta associata  
 Al momento della registrazione della proprietà, l'oggetto <xref:System.Windows.FrameworkPropertyMetadata> viene impostato in modo da specificare le caratteristiche della proprietà, ad esempio se la proprietà influisce sul rendering, sulla misurazione e così via.  In genere i metadati di una [proprietà associata](GTMT) non sono diversi rispetto a quelli presenti in una [proprietà di dipendenza](GTMT).  Se si specifica un valore predefinito in un override per i metadati di una proprietà associata, tale valore diviene il valore predefinito della proprietà associata implicita nelle istanze della classe che esegue l'override.  In particolare, il valore predefinito viene segnalato se un processo esegue una query per il valore di una proprietà associata tramite la funzione di accesso al metodo `Get` di quella proprietà, specificando un'istanza della classe in cui sono stati definiti i metadati e il valore per quella proprietà collegata non era stato diversamente impostato.  
  
 Se si desidera abilitare l'ereditarietà del valore di una proprietà, è necessario utilizzare le proprietà associate anziché le proprietà di dipendenza non associate.  Per informazioni dettagliate, vedere [Ereditarietà del valore della proprietà](../../../../docs/framework/wpf/advanced/property-value-inheritance.md).  
  
<a name="custom"></a>   
## Proprietà associate personalizzate  
  
<a name="create_attached_properties"></a>   
### Quando creare una proprietà associata  
 È possibile creare una [proprietà associata](GTMT) quando è necessario disporre di un meccanismo di impostazione delle proprietà per le classi diverse dalla classe di definizione.  In questo caso, lo scenario più comune è il layout.  Esempi di proprietà del layout esistenti possono essere <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>, <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=fullName> e <xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=fullName>.  Nello scenario abilitato in questo contesto, gli elementi che sono disponibili come elementi figlio degli elementi di controllo del layout sono in grado di indicare i requisiti del layout agli elementi padre del layout singolarmente, impostando ciascuno un valore della proprietà definito dall'elemento padre come proprietà associata.  
  
 Un altro scenario per l'utilizzo di una proprietà associata è quello in cui la classe rappresenta un servizio e si desidera che le classi siano in grado di integrare il servizio in modo più trasparente.  
  
 Infine, un ulteriore scenario prevede di ricevere un supporto [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)], ad esempio la modifica della finestra **Proprietà**.  Per ulteriori informazioni, vedere [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
 Come indicato in precedenza, è necessario eseguire la registrazione come proprietà associata se si desidera utilizzare l'ereditarietà del valore della proprietà.  
  
<a name="how_do_i_create_attached_properties"></a>   
### Come creare una proprietà associata  
 Se la classe definisce la [proprietà associata](GTMT) esclusivamente per l'utilizzo in altri tipi, non deve derivare da <xref:System.Windows.DependencyObject>.  Ma è necessario derivare da <xref:System.Windows.DependencyObject> se invece in generale  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] il modello di disporre della proprietà associata è anche una proprietà di dipendenza.  
  
 Definire la proprietà associata come proprietà di dipendenza dichiarando un campo `public` `static` `readonly` di tipo <xref:System.Windows.DependencyProperty>.  È possibile definire questo campo utilizzando il valore restituito dal metodo <xref:System.Windows.DependencyProperty.RegisterAttached%2A>.  Il nome del campo deve corrispondere al nome della proprietà associata, a cui viene aggiunta la stringa `Property`, secondo il modello [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] stabilito per la denominazione dei campi di identificazione in base alle proprietà che rappresentano.  Il provider della proprietà associata deve inoltre fornire statici `ottenere`*Nomeproprietà* e `set`*Nomeproprietà* metodi come funzioni di accesso per la proprietà associata; tale operazione non viene eseguita comporterà il sistema di proprietà non può utilizzare la proprietà associata.  
  
> [!NOTE]
>  Se si omette la funzione di accesso get della proprietà associata, l'associazione dati per la proprietà non funzionerà negli strumenti di progettazione, ad esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] e in Expression Blend.  
  
#### Funzione di accesso Get  
 la firma per `ottenere`*Nomeproprietà* la funzione di accesso deve essere:  
  
 `public static object Get` *PropertyName* `(object`  `target` `)`  
  
-   L'oggetto `target` può essere specificato nell'implementazione come tipo più specifico.  Ad esempio, il metodo <xref:System.Windows.Controls.DockPanel.GetDock%2A?displayProperty=fullName> immette il parametro come <xref:System.Windows.UIElement>, perché si presuppone che la proprietà associata sia impostata solo nelle istanze di <xref:System.Windows.UIElement>.  
  
-   Il valore restituito può essere specificato come tipo più specifico nell'implementazione.  Ad esempio, il metodo <xref:System.Windows.Controls.DockPanel.GetDock%2A> lo immette come <xref:System.Windows.Controls.Dock>, dal momento che è possibile impostare tale valore solo su quell'enumerazione.  
  
#### Funzione di accesso Set  
 la firma per `set`*Nomeproprietà* la funzione di accesso deve essere:  
  
 `public static void Set` *PropertyName* `(object`  `target` `, object`  `value` `)`  
  
-   L'oggetto `target` può essere specificato nell'implementazione come tipo più specifico.  Ad esempio, il metodo <xref:System.Windows.Controls.DockPanel.SetDock%2A> lo immette come <xref:System.Windows.UIElement>, perché si presuppone che la proprietà associata sia impostata solo nelle istanze di <xref:System.Windows.UIElement>.  
  
-   L'oggetto `value` può essere specificato nell'implementazione come tipo più specifico.  Ad esempio, il metodo <xref:System.Windows.Controls.DockPanel.SetDock%2A> lo immette come <xref:System.Windows.Controls.Dock>, dal momento che è possibile impostare tale valore solo su quell'enumerazione.  Tenere presente che il valore per questo metodo è l'input proveniente dal caricatore XAML quando rileva la proprietà associata in un utilizzo della proprietà associata nel markup.  Tale input è il valore specificato come valore di attributo XAML nel markup.  Pertanto, per il tipo utilizzato devono essere disponibili la conversione di tipo, il serializzatore del valore o un supporto per l'estensione di markup, in modo da poter creare il tipo appropriato in base al valore dell'attributo, rappresentato in pratica semplicemente da una stringa.  
  
 Nell'esempio seguente viene illustrata la registrazione della proprietà di dipendenza \(tramite il <xref:System.Windows.DependencyProperty.RegisterAttached%2A> metodo\) e `ottenere`*Nomeproprietà* e `set`*Nomeproprietà* funzioni di accesso.  Nell'esempio, la proprietà associata è denominata `IsBubbleSource`.  Pertanto, le funzioni di accesso devono essere chiamate `GetIsBubbleSource` e `SetIsBubbleSource`.  
  
 [!code-csharp[WPFAquariumSln#RegisterAttachedBubbler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerattachedbubbler)]
 [!code-vb[WPFAquariumSln#RegisterAttachedBubbler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerattachedbubbler)]  
  
#### Attributi di proprietà associate  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono definiti diversi [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)] allo scopo di fornire informazioni sulle proprietà associate ai processi di reflection e agli utenti tipici delle informazioni sulla reflection e sulle proprietà, ad esempio i progettisti.  Poiché le proprietà associate dispongono di un tipo di ambito illimitato, le finestre di progettazione sono necessari un modo per evitare che gli utenti dominante per con un elenco globale di tutte le proprietà associate definite in una particolare tecnologia che utilizza XAML.  Gli [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)] specificati in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per le proprietà associate possono essere utilizzati per definire l'ambito di situazioni in cui una certa proprietà associata deve essere visualizzata in una finestra delle proprietà.  È possibile applicare questi attributi anche per le proprietà associate personalizzate.  La funzione e la sintassi degli [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)] vengono descritti nelle relative pagine di riferimento:  
  
-   <xref:System.Windows.AttachedPropertyBrowsableAttribute>  
  
-   <xref:System.Windows.AttachedPropertyBrowsableForChildrenAttribute>  
  
-   <xref:System.Windows.AttachedPropertyBrowsableForTypeAttribute>  
  
-   <xref:System.Windows.AttachedPropertyBrowsableWhenAttributePresentAttribute>  
  
<a name="more"></a>   
## Ulteriori informazioni sulle proprietà associate  
  
-   Per ulteriori informazioni sulla creazione di una proprietà associata, vedere [Registrare una proprietà associata](../../../../docs/framework/wpf/advanced/how-to-register-an-attached-property.md).  
  
-   Per scenari di utilizzo più avanzati delle proprietà di dipendenza e delle proprietà associate, vedere [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  
  
-   È inoltre possibile registrare una proprietà come proprietà associata e proprietà di dipendenza, ma continuare a esporre le implementazioni del "wrapper".  In questo caso, la proprietà può essere impostata in tale elemento, o in qualsiasi elemento tramite la sintassi della proprietà associata XAML.  Un esempio di proprietà con uno scenario adatto sia agli utilizzi standard, sia agli utilizzi come proprietà associata è <xref:System.Windows.FrameworkElement.FlowDirection%2A?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.DependencyProperty>   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Registrare una proprietà associata](../../../../docs/framework/wpf/advanced/how-to-register-an-attached-property.md)