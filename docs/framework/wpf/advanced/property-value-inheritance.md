---
title: "Ereditariet&#224; del valore della propriet&#224; | Microsoft Docs"
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
  - "ereditarietà, valori delle proprietà"
  - "proprietà, ereditarietà dei valori"
  - "ereditarietà dei valori"
ms.assetid: d7c338f9-f2bf-48ed-832c-7be58ac390e4
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Ereditariet&#224; del valore della propriet&#224;
L'ereditarietà del valore della proprietà è una funzionalità del sistema di proprietà [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  L'ereditarietà del valore della proprietà consente agli elementi figlio in una struttura ad albero di elementi di ottenere il valore di una determinata proprietà dagli elementi padre, ereditando tale valore con le impostazioni specificate in un punto qualsiasi dell'elemento padre più vicino.  Anche l'elemento padre potrebbe aver ottenuto il valore tramite l'ereditarietà del valore della proprietà; pertanto il sistema potrebbe procedere in modo ricorsivo fino alla radice della pagina.  L'ereditarietà del valore della proprietà non è il comportamento predefinito del sistema di proprietà; è necessario stabilire una particolare impostazione dei metadati di una proprietà affinché quest'ultima attivi l'ereditarietà del valore per gli elementi figlio.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="Property_Value_Inheritance_is_Containment_Inheritance"></a>   
## L'ereditarietà del valore della proprietà è un'ereditarietà di contenimento  
 Il termine "ereditarietà" utilizzato in questa sede non coincide perfettamente con il concetto di ereditarietà nel contesto dei tipi e in generale della programmazione orientata a oggetti, in cui le classi derivate ereditano le definizioni dei membri dalle rispettive classi di base.  Tale significato di ereditarietà è valido anche in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]: le proprietà definite nelle varie classi di base sono esposte come attributi per le classi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] derivate, se utilizzate come elementi e come membri per il codice.  L'ereditarietà del valore della proprietà riguarda specificatamente il modo in cui i valori delle proprietà possono ereditare da un elemento a un altro in base alle relazioni padre\-figlio all'interno di una struttura ad albero di elementi.  Tale struttura ad albero di elementi è visibile più direttamente quando si annidano degli elementi all'interno di altri elementi in fase di definizione delle applicazioni nel markup [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Le strutture ad albero di oggetti possono essere create anche a livello di codice aggiungendo oggetti a raccolte designate di altri oggetti; in questo caso la modalità di funzionamento dell'ereditarietà del valore della proprietà sarà la stessa nella struttura ad albero completata in fase di esecuzione.  
  
<a name="Practical_Applications_of_Property_Value_Inheritance"></a>   
## Applicazioni pratiche dell'ereditarietà del valore della proprietà  
 Le [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] includono diverse proprietà per le quali è abilitata l'ereditarietà della proprietà.  In genere, lo scenario per queste proprietà prevede l'utilizzo di una proprietà dove possa essere impostata una sola volta per pagina, ma dove sia anche un membro di una delle classi dell'elemento di base e quindi esista anche nella maggior parte degli elementi figlio.  La proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A>, ad esempio, controlla la direzione in cui il contenuto passato deve essere presentato e disposto nella pagina.  Nella maggior parte dei casi si preferisce che il concetto di flusso del testo sia gestito coerentemente in tutti gli elementi figlio.  Se per qualche motivo la direzione del flusso è stata reimpostata in un livello della struttura ad albero dell'elemento da parte dell'utente o dell'ambiente, tale reimpostazione deve essere in genere eseguita per tutta la struttura.  Quando per la proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A> è abilitata l'ereditarietà, è necessario impostare o reimpostare il valore solo una volta al livello della struttura ad albero dell'elemento che include i requisiti di presentazione di ciascuna pagina dell'applicazione.  Anche il valore predefinito iniziale utilizzerà l'ereditarietà nello stesso modo.  Il modello di ereditarietà del valore della proprietà consente in ogni caso ai singoli elementi di reimpostare il valore nelle rare occasioni in cui si decide di disporre di una combinazione di direzioni di flusso.  
  
<a name="Making_a_Custom_Property_Inheritable"></a>   
## Rendere ereditabile una proprietà personalizzata  
 Modificando i metadati di una proprietà personalizzata è inoltre possibile rendere ereditabili le proprietà personalizzate.  Tuttavia, quando si definisce una proprietà come ereditabile, è necessario fare alcune considerazioni sulle prestazioni.  Nei casi in cui quella proprietà non disponga di un valore locale stabilito oppure di un valore ottenuto tramite stili, modelli o associazione dati, una proprietà ereditabile fornisce i relativi valori di proprietà assegnati a tutti gli elementi figlio dell'albero logico.  
  
 Per fare in modo che una proprietà partecipi all'ereditarietà del valore, creare una proprietà associata personalizzata, come descritto in [Registrare una proprietà associata](../../../../docs/framework/wpf/advanced/how-to-register-an-attached-property.md).  Registrare la proprietà con i metadati \(<xref:System.Windows.FrameworkPropertyMetadata>\) e specificare l'opzione "Inherits" nelle impostazioni relative alle opzioni all'interno dei metadati stessi.  Verificare quindi che la proprietà disponga di un valore predefinito stabilito, perché tale valore sarà ereditato.  Sebbene la proprietà sia stata registrata come associata, può essere necessario creare un "wrapper" della proprietà per ottenere o impostare l'accesso sul tipo di proprietario, come accade per una [proprietà di dipendenza](GTMT) non associata.  Una volta eseguita questa operazione, la proprietà ereditabile può essere impostata utilizzando il wrapper della proprietà diretto nel tipo di proprietario o nei tipi derivati oppure utilizzando la sintassi della proprietà associata in qualsiasi oggetto <xref:System.Windows.DependencyObject>.  
  
 Dal punto di vista concettuale le proprietà associate sono simili alle proprietà globali; è possibile verificare il valore in qualsiasi <xref:System.Windows.DependencyObject> e ottenere un risultato valido.  Lo scenario tipico delle proprietà associate prevede l'impostazione dei valori di proprietà negli elementi figlio e tale scenario sarà più efficace se la proprietà in questione è una proprietà associata sempre presente in modo implicito come proprietà associata in ciascun elemento \(<xref:System.Windows.DependencyObject>\) della struttura ad albero.  
  
> [!NOTE]
>  Sebbene possa sembrare che l'ereditarietà del valore della proprietà funzioni per le proprietà di dipendenza non associate, il comportamento di ereditarietà per una proprietà non associata attraverso determinati limiti di elementi nella struttura ad albero runtime non è definito.  Utilizzare sempre <xref:System.Windows.DependencyProperty.RegisterAttached%2A> per registrare le proprietà per le quali si specifica <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A> nei metadati.  
  
<a name="InheritanceContext"></a>   
## Eredità dei valori di proprietà attraverso i limiti della struttura ad albero  
 L'ereditarietà delle proprietà funziona mediante il passaggio attraverso una struttura ad albero di elementi.  Questa struttura ad albero spesso è parallela all'albero logico.  Tuttavia, quando si include un oggetto di [livello di base WPF](GTMT) nel markup che definisce una struttura ad albero dell'elemento, ad esempio un oggetto <xref:System.Windows.Media.Brush>, viene creato un albero logico discontinuo.  Un vero albero logico non si estende a livello concettuale all'interno di <xref:System.Windows.Media.Brush>, poiché il concetto di albero logico è un concetto a [livello framework WPF](GTMT).  Ciò può essere osservato nei risultati dell'utilizzo dei metodi di <xref:System.Windows.LogicalTreeHelper>.  Tuttavia, l'ereditarietà del valore di proprietà può colmare questa discontinuità nell'albero logico e continuare a far passare i valori ereditati, se la proprietà ereditabile è stata registrata come proprietà associata e se non viene rilevato alcun limite di blocco dell'ereditarietà impostato intenzionalmente \(ad esempio <xref:System.Windows.Controls.Frame>\).  
  
## Vedere anche  
 [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [Cenni preliminari sulle proprietà associate](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)   
 [Precedenza del valore della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)