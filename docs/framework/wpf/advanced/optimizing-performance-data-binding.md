---
title: "Ottimizzazione delle prestazioni: associazione dati | Microsoft Docs"
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
  - "associazione dati, prestazioni"
  - "associazione dati, prestazioni"
ms.assetid: 1506a35d-c009-43db-9f1e-4e230ad5be73
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Ottimizzazione delle prestazioni: associazione dati
L'associazione dati [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] rappresenta per le applicazioni un modo semplice e coerente di presentare e interagire con i dati.  È possibile associare gli elementi a numerose origini dati sotto forma di oggetti [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] e [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)].  
  
 In questo argomento vengono forniti i requisiti relativi alle prestazioni dell'associazione dati.  
  
   
  
<a name="HowDataBindingReferencesAreResolved"></a>   
## Risoluzione dei riferimenti per l'associazione dati  
 Prima di trattare i problemi di prestazione legati all'associazione dati, è opportuno approfondire come i riferimenti agli oggetti per l'associazione dati vengano risolti dal motore di associazione dati di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] .  
  
 L'origine di un'associazione dati [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] può essere qualsiasi oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  È possibile stabilire associazioni a proprietà, proprietà secondarie o indici di un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  I riferimenti dell'associazione vengono risolti utilizzando la reflection di [!INCLUDE[TLA#tla_avalonwinfx](../../../../includes/tlasharptla-avalonwinfx-md.md)] o un oggetto <xref:System.ComponentModel.ICustomTypeDescriptor>.  Di seguito vengono descritti tre modi per risolvere riferimenti a oggetti per l'associazione.  
  
 Il primo metodo richiede l'utilizzo della reflection.  In questo caso, l'oggetto <xref:System.Reflection.PropertyInfo> viene utilizzato per individuare gli attributi della proprietà e per accedere ai metadati della proprietà.  Quando si utilizza l'interfaccia <xref:System.ComponentModel.ICustomTypeDescriptor>, il motore di associazione dati utilizza questa interfaccia per accedere ai valori della proprietà.  L'interfaccia <xref:System.ComponentModel.ICustomTypeDescriptor> è particolarmente utile nei casi in cui l'oggetto non dispone di un insieme statico di proprietà.  
  
 Le notifiche di modifica delle proprietà possono essere fornite implementando l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged> o utilizzando le notifiche di modifica associate all'oggetto <xref:System.ComponentModel.TypeDescriptor>.  La strategia da preferire per l'implementazione delle notifiche di modifica delle proprietà consiste tuttavia nell'utilizzare l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>.  
  
 Se l'oggetto di origine è un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] e la proprietà di origine è una proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], il motore di associazione dati di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] deve innanzitutto utilizzare la reflection sull'oggetto di origine per ottenere l'oggetto <xref:System.ComponentModel.TypeDescriptor> e quindi eseguire una query per un oggetto <xref:System.ComponentModel.PropertyDescriptor>.  Questa sequenza di operazioni di reflection richiede potenzialmente molto tempo da un punto di vista delle prestazioni.  
  
 Il secondo metodo di risoluzione dei riferimenti agli oggetti richiede un oggetto di origine [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] che implementa l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged> e una proprietà di origine che è una proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  In questo caso, il motore di associazione dati utilizza direttamente la reflection sul tipo di origine e ottiene la proprietà necessaria.  Sebbene presenti requisiti del working set inferiori rispetto al primo metodo, non si tratta ancora del metodo ottimale.  
  
 Il terzo metodo di risoluzione dei riferimenti agli oggetti richiede un oggetto di origine <xref:System.Windows.DependencyObject> e una proprietà di origine <xref:System.Windows.DependencyProperty>.  In questo caso, non è richiesto l'utilizzo della reflection da parte del motore di associazione dati.  Il motore della proprietà e il motore di associazione dati risolvono il riferimento alla proprietà in modo indipendente.  Si tratta del metodo ottimale per la risoluzione dei riferimenti agli oggetti utilizzati per l'associazione dati.  
  
 Nella tabella riportata di seguito viene confrontata la velocità di associazione dati della proprietà <xref:System.Windows.Controls.TextBlock.Text%2A> di milli elementi <xref:System.Windows.Controls.TextBlock> utilizzando questi tre metodi.  
  
|**Associazione della proprietà Text di un TextBlock**|**Tempo di associazione \(ms\)**|**Tempo di rendering – include l'associazione \(ms\)**|  
|-----------------------------------------------------------|--------------------------------------|------------------------------------------------------------|  
|A una proprietà di un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]|115|314|  
|A una proprietà di un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] che implementa <xref:System.ComponentModel.INotifyPropertyChanged>|115|305|  
|A una proprietà <xref:System.Windows.DependencyProperty> di un oggetto <xref:System.Windows.DependencyObject>.|90|263|  
  
<a name="Binding_to_Large_CLR_Objects"></a>   
## Associazione a oggetti CLR di grandi dimensioni  
 Quando si stabilisce un'associazione dati a un singolo oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] con migliaia di proprietà, l'impatto sulle prestazioni è notevole.  È possibile limitare questo impatto dividendo il singolo oggetto in più oggetti [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] con un numero inferiore di proprietà.  Nella tabella vengono elencati i tempi di associazione e rendering per l'associazione dati a un singolo oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] di grandi dimensioni rispetto a più oggetti di dimensioni inferiori.  
  
|**Associazione dati di 1000 oggetti TextBlock**|**Tempo di associazione \(ms\)**|**Tempo di rendering – include l'associazione \(ms\)**|  
|-----------------------------------------------------|--------------------------------------|------------------------------------------------------------|  
|A un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] con 1000 proprietà|950|1200|  
|A 1000 oggetti [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] con una proprietà|115|314|  
  
<a name="Binding_to_an_ItemsSource"></a>   
## Associazione a una proprietà ItemsSource  
 Si consideri uno scenario in cui un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> contiene un elenco di dipendenti da visualizzare in un controllo <xref:System.Windows.Controls.ListBox>.  Per creare una corrispondenza tra questi due oggetti, è necessario associare l'elenco dei dipendenti alla proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> del controllo <xref:System.Windows.Controls.ListBox>.  Si supponga ora che un nuovo dipendente si unisca al gruppo.  Si potrebbe pensare che per inserire questo nuovo dipendente nei valori <xref:System.Windows.Controls.ListBox> associati, sia semplicemente necessario aggiungerlo all'elenco dei dipendenti e attendere che tale modifica venga riconosciuta automaticamente dal motore di associazione dati.  Tale ipotesi finirebbe per rivelarsi falsa; in realtà, la modifica non verrà riflessa automaticamente nel controllo <xref:System.Windows.Controls.ListBox>.  L'oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]<xref:System.Collections.Generic.List%601>, infatti, non genera automaticamente un evento di modifica della raccolta.  Affinché l'oggetto <xref:System.Windows.Controls.ListBox> rilevi automaticamente le modifiche, è necessario ricreare l'elenco dei dipendenti e collegarlo nuovamente alla proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> del controllo <xref:System.Windows.Controls.ListBox>.  Questa soluzione funziona, ma produce un notevole impatto sulle prestazioni.  Ogni volta che la proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> del controllo <xref:System.Windows.Controls.ListBox> viene riassegnata a un nuovo oggetto, il controllo <xref:System.Windows.Controls.ListBox> elimina gli elementi precedenti e rigenera l'intero elenco.  L'impatto sulle prestazioni risulta maggiore se il controllo <xref:System.Windows.Controls.ListBox> viene mappato a un oggetto <xref:System.Windows.DataTemplate> complesso.  
  
 Una soluzione molto efficace a questo problema consiste nell'impostare l'elenco dei dipendenti come <xref:System.Collections.ObjectModel.ObservableCollection%601>.  Un oggetto <xref:System.Collections.ObjectModel.ObservableCollection%601> genera una notifica di modifica che il motore di associazione dati può ricevere.  L'evento aggiunge o rimuove un elemento da <xref:System.Windows.Controls.ItemsControl> senza la necessità che l'intero elenco venga rigenerato.  
  
 Nella tabella riportata di seguito è indicato il tempo necessario per l'aggiornamento del controllo <xref:System.Windows.Controls.ListBox> \(con la virtualizzazione dell'interfaccia utente disattivata\) quando viene aggiunto un elemento.  Il numero nella prima riga rappresenta il tempo trascorso quando l'oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]<xref:System.Collections.Generic.List%601> viene associato alla proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>dell'elemento <xref:System.Windows.Controls.ListBox>.  Il numero nella seconda riga rappresenta il tempo trascorso quando un oggetto <xref:System.Collections.ObjectModel.ObservableCollection%601> viene associato alla proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> dell'elemento <xref:System.Windows.Controls.ListBox>.  Si noti il notevole risparmio di tempo se si utilizza la strategia di associazione dati dell'oggetto <xref:System.Collections.ObjectModel.ObservableCollection%601>.  
  
|**Associazione dati della proprietà ItemsSource**|**Tempo di aggiornamento per 1 elemento \(ms\)**|  
|-------------------------------------------------------|------------------------------------------------------|  
|A un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601>|1656|  
|A un oggetto <xref:System.Collections.ObjectModel.ObservableCollection%601>|20|  
  
<a name="Binding_IList_to_ItemsControl_not_IEnumerable"></a>   
## Associare IList a un oggetto ItemsControl, non IEnumerable  
 Se è possibile scegliere tra l'associazione di un oggetto <xref:System.Collections.Generic.IList%601> o di un oggetto <xref:System.Collections.IEnumerable> a un oggetto <xref:System.Windows.Controls.ItemsControl>, scegliere <xref:System.Collections.Generic.IList%601>.  L'associazione di <xref:System.Collections.IEnumerable> a <xref:System.Windows.Controls.ItemsControl> impone in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la creazione di un oggetto <xref:System.Collections.Generic.IList%601> wrapper, con conseguente calo delle prestazioni dovuto al sovraccarico non necessario di un secondo oggetto.  
  
<a name="Do_not_Convert_CLR_objects_to_Xml_Just_For_Data_Binding"></a>   
## Non convertire oggetti CLR in XML solo per l'associazione dati.  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consente di eseguire l'associazione dati a contenuto [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)]. L'associazione dati a contenuto [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] è tuttavia più lenta rispetto all'associazione dati a oggetti [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Non convertire dati di oggetti [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] a XML se l'unico scopo è l'associazione dati.  
  
## Vedere anche  
 [Ottimizzazione delle prestazioni di applicazioni WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [Pianificazione delle prestazioni dell'applicazione](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [Sfruttare appieno l'hardware](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Comportamento dell'oggetto](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Risorse delle applicazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedura dettagliata: memorizzazione dei dati di un'applicazione nella cache di un'applicazione WPF](../../../../docs/framework/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)