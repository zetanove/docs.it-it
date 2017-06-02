---
title: "Cenni preliminari sugli eventi associati | Microsoft Docs"
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
  - "eventi associati [WPF], definizione"
  - "eventi associati [WPF], scenari"
  - "eventi associati ed eventi indirizzati [WPF]"
  - "supporto di eventi associati a eventi indirizzati [WPF]"
  - "definizione di eventi associati come eventi indirizzati [WPF]"
  - "gestione di eventi associati [WPF]"
ms.assetid: 2c40eae3-80e4-4a45-ae09-df6c9ab4d91e
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sugli eventi associati
[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] definisce un componente del linguaggio e un tipo di evento noto come *evento associato*.  Il concetto di evento associato consente di aggiungere un gestore per un determinato evento a un elemento arbitrario, anziché a un elemento che definisce o eredita effettivamente l'evento.  In questo caso, né l'oggetto che genera potenzialmente l'evento, né l'istanza di gestione di destinazione definisce o possiede in altro modo l'evento.  
  
   
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si presuppone la lettura di [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md) e [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md).  
  
<a name="Syntax"></a>   
## Sintassi dell'evento associato  
 Per supportare l'utilizzo degli eventi associati, è necessario che il codice sottostante utilizzi una sintassi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e un modello di codifica specifici di tali eventi.  
  
 Nella sintassi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], l'evento associato non è specificato solo dal nome di evento, ma dal tipo proprietario e dal nome di evento, separati da un punto \(.\).  Poiché il nome di evento è qualificato con il nome del tipo proprietario, la sintassi dell'evento associato consente l'associazione di tale evento a qualsiasi elemento di cui è possibile creare un'istanza.  
  
 Ad esempio, di seguito viene illustrata la sintassi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] per collegare un gestore per un evento associato `NeedsCleaning` personalizzato:  
  
 [!code-xml[WPFAquariumSln#AE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquarium/Window1.xaml#ae)]  
  
 Si noti il prefisso `aqua:`, necessario in questo caso poiché l'evento associato è un evento personalizzato tratto da un xmlns mappato personalizzato.  
  
<a name="WPFImplements"></a>   
## Modalità di implementazione degli eventi associati in WPF  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], gli eventi associati sono supportati da un campo <xref:System.Windows.RoutedEvent> e sono indirizzati attraverso la struttura ad albero dopo essere stati generati.  In genere, l'origine dell'evento associato \(oggetto che genera l'evento\) è un'origine di sistema o servizio e l'oggetto che esegue il codice che genera l'evento non è pertanto parte diretta della struttura ad albero dell'elemento.  
  
<a name="Scenarios"></a>   
## Scenari per gli eventi associati  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], gli eventi associati sono presenti in alcune aree di funzionalità in cui vi è astrazione del livello di servizio, ad esempio per gli eventi abilitati dalla classe <xref:System.Windows.Input.Mouse> statica o dalla classe <xref:System.Windows.Controls.Validation>.  Le classi che interagiscono con il servizio o lo utilizzano possono utilizzare l'evento nella sintassi dell'evento associato o scegliere di utilizzarlo come un evento indirizzato che fa parte del modo in cui la classe integra le funzionalità del servizio.  
  
 Anche se in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono definiti vari eventi associati, gli scenari in cui si utilizza o si gestisce direttamente l'evento associato sono molto limitati.  Generalmente, l'evento associato assolve uno scopo nell'architettura, ma viene inoltrato a un evento indirizzato non associato \(supportato da un wrapper di eventi [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]\).  
  
 Ad esempio, l'evento associato sottostante <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=fullName> può essere gestito più facilmente su qualsiasi <xref:System.Windows.UIElement> specificato utilizzando <xref:System.Windows.UIElement.MouseDown> su tale <xref:System.Windows.UIElement>, anziché utilizzare la sintassi dell'evento associato in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] o nel codice.  L'evento associato assolve a uno scopo nell'architettura poiché consente l'espansione futura dei dispositivi di input.  Sarebbe sufficiente che il dispositivo ipotetico generasse <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=fullName> per simulare l'input del mouse, senza la necessità di derivare da <xref:System.Windows.Input.Mouse> a tale scopo.  Questo scenario comporta tuttavia la gestione di codice degli eventi e la gestione di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] dell'evento associato non è attinente a questo scenario.  
  
<a name="Handling"></a>   
## Gestione di un evento associato in WPF  
 Il processo di gestione di un evento associato e il codice del gestore che verrà scritto è fondamentalmente lo stesso necessario per un evento indirizzato.  
  
 In genere, un evento associato [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]non è molto diverso da un evento indirizzato [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Le differenze sono date dalla modalità di origine dell'evento e della relativa esposizione da parte di una classe come membro, operazione che ha anche effetto sulla sintassi del gestore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 Tuttavia, come indicato in precedenza, gli eventi associati [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] esistenti non sono destinati in modo particolare alla gestione in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Più spesso, lo scopo dell'evento è quello di consentire la segnalazione di uno stato da parte di un elemento composto a un elemento padre nella composizione, nel qual caso l'evento viene in genere generato nel codice e si basa inoltre sulla gestione della classe nella classe padre rilevante.  Ad esempio, è previsto che elementi all'interno di <xref:System.Windows.Controls.Primitives.Selector> generino l'evento <xref:System.Windows.Controls.Primitives.Selector.Selected> associato, che viene quindi gestito dalla classe <xref:System.Windows.Controls.Primitives.Selector> e potenzialmente convertito dalla classe <xref:System.Windows.Controls.Primitives.Selector> in un evento indirizzato diverso, <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged>.  Per ulteriori informazioni sugli eventi indirizzati e sulla gestione delle classi, vedere [Contrassegno degli eventi indirizzati come gestiti e gestione delle classi](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md).  
  
<a name="Custom"></a>   
## Definizione di eventi associati personalizzati come eventi indirizzati  
 Se si deriva da classi di base [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] comuni, è possibile implementare eventi associati personalizzati mediante l'inclusione di alcuni metodi del modello nella classe e l'utilizzo di metodi dell'utilità già presenti sulle classi di base.  
  
 Il modello è il seguente:  
  
-   Un metodo `Add*Handler` con due parametri.  Il primo parametro deve identificare l'evento, il quale deve corrispondere ai nomi con il segno \* nel nome del metodo.  Il secondo parametro è il gestore da aggiungere.  Il metodo deve essere pubblico e statico, senza valore restituito.  
  
-   Un metodo `Remove*Handler` con due parametri.  Il primo parametro deve identificare l'evento, il quale deve corrispondere ai nomi con il segno \* nel nome del metodo.  Il secondo parametro è il gestore da rimuovere.  Il metodo deve essere pubblico e statico, senza valore restituito.  
  
 Il metodo della funzione di accesso `Add*Handler` facilita l'elaborazione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] quando su un elemento vengono dichiarati attributi del gestore dell'evento associato.  I metodi `Add*Handler` e `Remove*Handler` abilitano inoltre l'accesso del codice all'archivio del gestore eventi per l'evento associato.  
  
 Questo modello generale non è ancora sufficientemente preciso per l'implementazione pratica in un framework, poiché qualsiasi implementazione del lettore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] specificata può avere schemi diversi per l'identificazione di eventi sottostanti nel linguaggio e nell'architettura di supporto.  Questo è uno dei motivi per cui in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] gli eventi associati vengono implementati come eventi indirizzati. L'identificatore da utilizzare per un evento \(<xref:System.Windows.RoutedEvent>\) è già definito dal sistema di eventi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Il routing di un evento, inoltre, è una naturale estensione dell'implementazione nel concetto di evento associato al livello di linguaggio [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 L'implementazione `Add*Handler` per un evento associato [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è costituita dalla chiamata a <xref:System.Windows.UIElement.AddHandler%2A> con l'evento indirizzato e il gestore come argomenti.  
  
 Questa strategia di implementazione e il sistema degli eventi indirizzati limitano in genere la gestione degli eventi associati alle classi derivate da <xref:System.Windows.UIElement> o da <xref:System.Windows.ContentElement>, poiché solo tali classi dispongono di implementazioni di <xref:System.Windows.UIElement.AddHandler%2A>.  
  
 Ad esempio, nel codice riportato di seguito viene definito l'evento associato `NeedsCleaning` sulla classe del proprietario `Aquarium`, utilizzando la strategia [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] di dichiarazione dell'evento associato come evento indirizzato.  
  
 [!code-csharp[WPFAquariumSln#AECode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#aecode)]
 [!code-vb[WPFAquariumSln#AECode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#aecode)]  
  
 Si noti che il metodo utilizzato per definire il campo identificatore dell'evento associato, <xref:System.Windows.EventManager.RegisterRoutedEvent%2A>è in realtà lo stesso metodo utilizzato per registrare un evento indirizzato non associato.  Eventi associati ed eventi indirizzati vengono registrati in un archivio interno centralizzato.  Questa implementazione dell'archivio degli eventi consente la considerazione del concetto di "eventi come interfaccia" presentata in [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
<a name="Raising"></a>   
## Generazione di un evento associato WPF  
 Non è in genere necessario generare dal codice eventi associati esistenti definiti in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Questi eventi rispettano il modello basilare generale di "servizio" e le classi di servizio, come <xref:System.Windows.Input.InputManager>, sono responsabili della generazione degli eventi.  
  
 Tuttavia, nella definizione di un evento associato personalizzato basato sul modello [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per il quale gli eventi associati sono basati su <xref:System.Windows.RoutedEvent>, è possibile utilizzare <xref:System.Windows.UIElement.RaiseEvent%2A> per generare un evento associato da qualsiasi <xref:System.Windows.UIElement> o <xref:System.Windows.ContentElement>.  La generazione di un evento indirizzato \(associato o meno\) richiede la dichiarazione di un determinato elemento nella struttura ad albero dell'elemento come origine evento. Tale origine è riportata come chiamante di <xref:System.Windows.UIElement.RaiseEvent%2A>.  È responsabilità del servizio determinare quale elemento viene riportato come origine nella struttura ad albero.  
  
## Vedere anche  
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)   
 [Classi XAML e personalizzate per WPF](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)