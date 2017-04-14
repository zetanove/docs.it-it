---
title: "Cenni preliminari sugli elementi di base | Microsoft Docs"
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
  - "elementi di base"
ms.assetid: 2c997092-72c6-4767-bc84-74267f4eee72
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Cenni preliminari sugli elementi di base
Una percentuale elevata di classi in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] deriva da quattro classi alle quali viene comunemente fatto riferimento nella documentazione [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] come classi degli elementi di base.  Queste classi sono <xref:System.Windows.UIElement>, <xref:System.Windows.FrameworkElement>, <xref:System.Windows.ContentElement> e <xref:System.Windows.FrameworkContentElement>.  La classe <xref:System.Windows.DependencyObject> è correlata in quanto si tratta di una classe di base comune di <xref:System.Windows.UIElement> e <xref:System.Windows.ContentElement>  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="base_apis"></a>   
## API degli elementi di base nelle classi WPF  
 <xref:System.Windows.UIElement> e <xref:System.Windows.ContentElement> derivano da <xref:System.Windows.DependencyObject>, attraverso percorsi diversi.  La differenza a questo livello è relativa alla modalità di utilizzo di <xref:System.Windows.UIElement> o <xref:System.Windows.ContentElement> in un'interfaccia utente e allo scopo che tali oggetti assolvono in un'applicazione.  <xref:System.Windows.UIElement> dispone anche di <xref:System.Windows.Media.Visual> nella propria gerarchia di classi, una classe che espone il supporto di grafica di basso livello sottostante a [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  <xref:System.Windows.Media.Visual> fornisce un framework di rendering mediante la definizione di aree rettangolari indipendenti sullo schermo.  In pratica, <xref:System.Windows.UIElement> è destinato a elementi per i quali è previsto il supporto di un modello a oggetti più grande, il rendering e il layout in aree che è possibile descrivere come aree dello schermo rettangolari e un modello di contenuto più aperto, per consentire combinazioni diverse di elementi.  <xref:System.Windows.ContentElement> non deriva da <xref:System.Windows.Media.Visual>, ma è basato su un modello che prevede l'utilizzo di <xref:System.Windows.ContentElement> da parte di altri elementi, quali un lettore o un visualizzatore destinati a interpretare gli elementi e produrre l'oggetto <xref:System.Windows.Media.Visual> completo da utilizzare in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Alcune classi <xref:System.Windows.UIElement> sono destinate a essere host di contenuto. Forniscono funzionalità di hosting e rendering per una o più classi <xref:System.Windows.ContentElement> \(<xref:System.Windows.Controls.DocumentViewer> è un esempio di tale classe\).  <xref:System.Windows.ContentElement> è utilizzato come classe di base per gli elementi con modelli a oggetti più piccoli e più indirizzati a contenuto tipo testo, informazioni o documenti che possono essere ospitati in un oggetto <xref:System.Windows.UIElement>.  
  
### Livello di framework e livello principale  
 <xref:System.Windows.UIElement> funge da classe di base per le classi <xref:System.Windows.FrameworkElement> e <xref:System.Windows.ContentElement> funge da classe di base per <xref:System.Windows.FrameworkContentElement>.  Il motivo per questo livello successivo di classi è il supporto di un [livello principale WPF](GTMT) separato da un [livello di framework WPF](GTMT), una divisione che esiste anche nella modalità in cui vengono suddivise le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] tra gli assembly PresentationCore e PresentationFramework.  Il [livello di framework WPF](GTMT) offre una soluzione più completa per le necessità di base delle applicazioni, inclusa l'implementazione del gestore di layout per le presentazioni.  Il [livello principale WPF](GTMT) è una modalità di utilizzare in modo esteso [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] senza l'overhead di assembly aggiuntivo.  La distinzione tra questi livelli raramente è importante nella maggior parte degli scenari di sviluppo delle applicazioni tipici e, in genere, occorre considerare le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] come un tutto, senza preoccuparsi della differenza tra [livello di framework WPF](GTMT) e [livello principale WPF](GTMT).  Può essere necessario conoscere le distinzioni tra i livelli se in un progetto di applicazione si decide di sostituire quantità significative di funzionalità del [livello di framework WPF](GTMT), ad esempio se la soluzione complessiva dispone già di implementazioni personalizzate per la composizione e il layout dell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  
  
<a name="subclassing_elements"></a>   
## Scelta dell'elemento da cui derivare  
 Il modo ottimale per creare una classe personalizzata che estende [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consiste nel derivare da una delle classi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] mediante cui si ottiene la massima funzionalità desiderata tramite la gerarchia di classi esistente.  In questa sezione vengono elencate le funzionalità fornite da tre delle più importanti classi di elementi che consentono di decidere da quale classe ereditare.  
  
 Per l'implementazione di un controllo, uno dei motivi più comuni per derivare da una classe [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è probabile che si desideri derivare da una classe che è un controllo pratico, una classe di base della famiglia dei controlli o almeno dalla classe di base <xref:System.Windows.Controls.Control>.  Per istruzioni ed esempi pratici, vedere [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
 Se non si crea un controllo e si desidera derivare da una classe più elevata nella gerarchia, nelle sezioni seguenti vengono fornite informazioni sulle caratteristiche definite in ogni classe degli elementi di base.  
  
 Se si crea una classe che deriva da <xref:System.Windows.DependencyObject>, si ereditano le funzionalità seguenti:  
  
-   Supporto di <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A> e supporto del sistema delle proprietà generale.  
  
-   Possibilità di utilizzare le [proprietà di dipendenza](GTMT) e le [proprietà associate](GTMT) implementate come [proprietà di dipendenza](GTMT).  
  
 Se si crea una classe che deriva da <xref:System.Windows.UIElement>, si ereditano le funzionalità seguenti oltre a quelle fornite da <xref:System.Windows.DependencyObject>:  
  
-   Supporto di base per i valori delle proprietà animate.  Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
-   Supporto dell'evento di input di base e supporto di controllo.  Per ulteriori informazioni, vedere [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md) e [Cenni preliminari sull'esecuzione di comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md).  
  
-   È possibile eseguire l'override dei metodi virtuali per fornire informazioni a un sistema di layout.  
  
 Se si crea una classe che deriva da <xref:System.Windows.FrameworkElement>, si ereditano le funzionalità seguenti oltre a quelle fornite da <xref:System.Windows.UIElement>:  
  
-   Supporto per l'utilizzo di stili e storyboard.  Per ulteriori informazioni, vedere <xref:System.Windows.Style> e [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
-   Supporto per l'associazione dati  Per ulteriori informazioni, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
-   Supporto per i riferimenti di risorse dinamiche.  Per ulteriori informazioni, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
-   Supporto dell'ereditarietà dei valori di proprietà e altri flag nei metadati che agevolano la segnalazione di condizioni relative alle proprietà ai servizi del framework, ad esempio associazione dati, stili o implementazione del layout nel framework.  Per ulteriori informazioni, vedere [Metadati delle proprietà del framework](../../../../docs/framework/wpf/advanced/framework-property-metadata.md).  
  
-   Concetto di [albero logico](GTMT).  Per ulteriori informazioni, vedere [Strutture ad albero in WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md).  
  
-   Supporto per l'implementazione pratica del sistema di layout al [livello di framework WPF](GTMT), incluso un override di <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> per rilevare le modifiche alle proprietà che hanno effetto sul layout.  
  
 Se si crea una classe che deriva da <xref:System.Windows.ContentElement>, si ereditano le funzionalità seguenti oltre a quelle fornite da <xref:System.Windows.DependencyObject>:  
  
-   Supporto per le animazioni.  Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
-   Supporto dell'evento di input di base e supporto di controllo.  Per ulteriori informazioni, vedere [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md) e [Cenni preliminari sull'esecuzione di comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md).  
  
 Se si crea una classe che deriva da <xref:System.Windows.FrameworkContentElement>, si ottengono le funzionalità seguenti oltre a quelle fornite da <xref:System.Windows.ContentElement>:  
  
-   Supporto per l'utilizzo di stili e storyboard.  Per ulteriori informazioni, vedere <xref:System.Windows.Style> e [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
-   Supporto per l'associazione dati  Per ulteriori informazioni, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
-   Supporto per i riferimenti di risorse dinamiche.  Per ulteriori informazioni, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
-   Supporto dell'ereditarietà dei valori di proprietà e altri flag nei metadati che agevolano la segnalazione di condizioni relative alle proprietà ai servizi del framework, come associazione dati, stili o implementazione del layout nel framework.  Per ulteriori informazioni, vedere [Metadati delle proprietà del framework](../../../../docs/framework/wpf/advanced/framework-property-metadata.md).  
  
-   Non si eredita l'accesso alle modifiche del sistema di layout \(ad esempio <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>\).  Le implementazioni del sistema di layout sono disponibili solo in <xref:System.Windows.FrameworkElement>.  Tuttavia, viene ereditato un override di <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> per rilevare le modifiche alle proprietà che hanno effetto sul layout e segnalarle a qualsiasi host del contenuto.  
  
 I modelli di contenuto sono documentati per una varietà di classi.  Il modello di contenuto per una classe è un fattore possibile da considerare per trovare una classe adatta da cui derivare.  Per ulteriori informazioni, vedere [Modello di contenuto WPF](../../../../docs/framework/wpf/controls/wpf-content-model.md).  
  
<a name="other_base_classes"></a>   
## Altre classi di base  
  
### DispatcherObject  
 <xref:System.Windows.Threading.DispatcherObject> fornisce supporto per il modello di threading [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e consente l'associazione di tutti gli oggetti creati per le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] a <xref:System.Windows.Threading.Dispatcher>.  Anche se non si deriva da <xref:System.Windows.UIElement>, <xref:System.Windows.DependencyObject> o <xref:System.Windows.Media.Visual>, è necessario considerare la possibilità di derivare da <xref:System.Windows.Threading.DispatcherObject> per ottenere il supporto del modello di threading.  Per ulteriori informazioni, vedere [Modello di threading](../../../../docs/framework/wpf/advanced/threading-model.md).  
  
### Visual  
 <xref:System.Windows.Media.Visual> implementa il concetto di un oggetto 2D che generalmente richiede la presentazione visiva in un'area approssimativamente rettangolare.  Il rendering effettivo di <xref:System.Windows.Media.Visual> viene effettuato in altre classi \(non è autonomo\), ma la classe <xref:System.Windows.Media.Visual> fornisce un tipo noto utilizzato dai processi di rendering a vari livelli.  <xref:System.Windows.Media.Visual> implementa l'hit testing, ma non espone eventi che segnalano valori positivi di hit testing, disponibili in <xref:System.Windows.UIElement>\).  Per ulteriori informazioni, vedere [Programmazione a livello visivo](../../../../docs/framework/wpf/graphics-multimedia/visual-layer-programming.md).  
  
### Oggetto Freezable  
 <xref:System.Windows.Freezable> simula la non modificabilità in un oggetto modificabile fornendo i mezzi per generare copie dell'oggetto quando per motivi di prestazioni è necessario o utile un oggetto non modificabile.  Il tipo <xref:System.Windows.Freezable> fornisce una base comune per alcuni elementi grafici, ad esempio geometrie, pennelli e animazioni.  <xref:System.Windows.Freezable> non è un oggetto <xref:System.Windows.Media.Visual>. Può contenere proprietà che diventano sottoproprietà quando <xref:System.Windows.Freezable> viene applicato per riempire un valore di proprietà di un altro oggetto e tali sottoproprietà possono influire sul rendering.  Per ulteriori informazioni, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
 <xref:System.Windows.Media.Animation.Animatable>  
  
 <xref:System.Windows.Media.Animation.Animatable> è una classe derivata da <xref:System.Windows.Freezable> che specificamente aggiunge il livello di controllo animazione e alcuni membri dell'utilità per consentire di distinguere le proprietà attualmente animate da quelle non animate.  
  
### Controllo  
 <xref:System.Windows.Controls.Control> è la classe di base destinata al tipo di oggetto noto come controllo o componente, a seconda della tecnologia.  In genere, le classi di controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono classi che rappresentano direttamente un controllo dell'interfaccia utente o sono parte della composizione di tale controllo.  La funzionalità principale abilitata da <xref:System.Windows.Controls.Control> è l'applicazione di modelli di controllo.  
  
## Vedere anche  
 <xref:System.Windows.Controls.Control>   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [Architettura WPF](../../../../docs/framework/wpf/advanced/wpf-architecture.md)