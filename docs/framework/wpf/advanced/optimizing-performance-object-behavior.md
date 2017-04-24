---
title: "Ottimizzazione delle prestazioni: comportamento degli oggetti | Microsoft Docs"
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
  - "proprietà di dipendenza, prestazioni"
  - "gestori eventi [WPF]"
  - "Freezable (oggetti), prestazioni"
  - "prestazioni degli oggetti (considerazioni)"
  - "virtualizzazione dell'interfaccia utente"
ms.assetid: 73aa2f47-1d73-439a-be1f-78dc4ba2b5bd
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Ottimizzazione delle prestazioni: comportamento degli oggetti
La comprensione del comportamento intrinseco degli oggetti [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] facilita l'individuazione del compromesso ideale tra funzionalità e prestazioni.  
  
   
  
<a name="Not_Removing_Event_Handlers"></a>   
## La mancata rimozione dei gestori eventi dagli oggetti può mantenere gli oggetti attivi  
 Il delegato passato da un oggeto al relativo evento è un riferimento effettivo a tale oggetto.  Di conseguenza, i gestori eventi possono mantenere gli oggetti attivi più a lungo del previsto.  Quando si esegue la pulitura di un oggetto registrato per restare in ascolto di un evento dell'oggetto, è essenziale rimuovere tale delegato prima di rilasciare l'oggetto.  Mantenere attivi oggetti non necessari aumenta l'utilizzo di memoria dell'applicazione.  Questa situazione si verifica soprattutto quando l'oggetto è la radice di un [albero logico](GTMT) o di una [struttura ad albero visuale](GTMT).  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene introdotto un modello di listener di eventi debole per eventi che possono rivelarsi utili in situazioni in cui è difficile tenere traccia delle relazioni di durata degli oggetti tra origine e listener.  Alcuni eventi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] esistenti utilizzano questo modello.  Questo modello può essere utile per implementare oggetti con eventi personalizzati.  Per informazioni dettagliate, vedere [Modelli di eventi deboli](../../../../docs/framework/wpf/advanced/weak-event-patterns.md).  
  
 Sono disponibili vari strumenti, ad esempio il profiler CLR Profiler e il visualizzatore del working set, in grado di fornire informazioni sull'utilizzo della memoria di un determinato processo.  Il profiler CLR include numerose visualizzazioni del profilo di allocazione utili, tra cui un istogramma dei tipi allocati, grafici delle allocazioni e delle chiamate, una cronologia che mostra le operazioni di Garbage Collection di varie generazioni e lo stato dell'heap gestito che ne deriva e una struttura ad albero delle chiamate che mostra le allocazioni per metodo e i caricamenti degli assembly.  Per ulteriori informazioni, visitare il sito [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=117435) \(informazioni in lingua inglese\).  
  
<a name="DPs_and_Objects"></a>   
## Proprietà e oggetti di dipendenza  
 In genere, l'accesso a una [proprietà di dipendeza](GTMT) di un oggetto <xref:System.Windows.DependencyObject> non è più lento dell'accesso a una proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Sebbene vi sia un leggero sovraccarico delle prestazioni per l'impostazione del valore di una proprietà, ottenere un valore è rapido quanto ottenere il valore da una proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Il sovraccarico delle prestazioni è tuttavia compensato dal fatto che le [proprietà di dipendenza](GTMT) supportano funzionalità efficienti, quali l'associazione ai dati, l'animazione, l'ereditarietà e l'applicazione di stili.  Per ulteriori informazioni, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
### Ottimizzazioni di DependencyProperty  
 È necessario definire con grande attenzione le [proprietà di dipendenza](GTMT) nell'applicazione.  Se un oggetto <xref:System.Windows.DependencyProperty> influisce solo su opzioni di metadati di tipo rendering, anziché su altre opzioni di metadati come <xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>, è necessario contrassegnarlo come tale eseguendo l'override dei metadati.  Per ulteriori informazioni sull'override o su come ottenere i metadati delle proprietà, vedere [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
 Nel caso in cui non tutte le modifiche delle proprietà influiscono effettivamente sulla misura, la disposizione e il rendering, può essere più efficace disporre di un gestore delle modifiche delle proprietà che invalidi la misura, la disposizione e i passaggi di rendering manualmente.  Ad esempio, è possibile decidere di eseguire nuovamente il rendering di uno sfondo solo quando un valore è superiore a un limite impostato.  In questo caso, il rendering verrebbe invalidato dal gestore delle modifiche delle proprietà solo quando il valore supera il limite impostato.  
  
### Problemi legati alla possibilità di rendere ereditabile un oggetto DependencyProperty  
 Per impostazione predefinita, le [proprietà di dipendenza](GTMT) registrate non sono ereditabili.  Tuttavia, è possibile rendere ereditabile qualsiasi proprietà in modo esplicito.  Sebbene si tratti di una funzionalità utile, la conversione di una proprietà per renderla ereditabile ha un impatto sulle prestazioni poiché aumenta la durata dell'annullamento della convalida della proprietà.  
  
### Utilizzo di RegisterClassHandler  
 Mentre la chiamata a <xref:System.Windows.EventManager.RegisterClassHandler%2A> consente di salvare lo stato dell'istanza, è importante sapere che il gestore viene chiamato per tutte le istanze, con conseguenti problemi di prestazioni.  Utilizzare <xref:System.Windows.EventManager.RegisterClassHandler%2A> solo quando l'applicazione richiede il salvataggio dello stato dell'istanza.  
  
### Impostazione del valore predefinito di un oggetto DependencyProperty durante le registrazione  
 Quando si crea un oggetto <xref:System.Windows.DependencyProperty> che richiede un valore predefinito, impostare il valore utilizzando i metadati predefiniti passati come parametro al metodo <xref:System.Windows.DependencyProperty.Register%2A> di <xref:System.Windows.DependencyProperty>.  Utilizzare questa tecnica anziché l'impostazione del valore della proprietà in un costruttore o su ciascuna istanza di un elemento.  
  
### Impostazione del valore di PropertyMetadata utilizzando Register  
 Quando si crea un oggetto <xref:System.Windows.DependencyProperty>, è possibile impostare <xref:System.Windows.PropertyMetadata> utilizzando i metodi <xref:System.Windows.DependencyProperty.Register%2A> o <xref:System.Windows.DependencyProperty.OverrideMetadata%2A>.  Sebbene l'oggetto possa disporre di un costruttore statico per chiamare <xref:System.Windows.DependencyProperty.OverrideMetadata%2A>, non si tratta della soluzione ottimale a causa dell'impatto sulle prestazioni.  Per garantire prestazioni ottimali, impostare <xref:System.Windows.PropertyMetadata> durante la chiamata a <xref:System.Windows.DependencyProperty.Register%2A>.  
  
<a name="Freezable_Objects"></a>   
## Oggetti Freezable  
 <xref:System.Windows.Freezable> è un tipo di oggetto speciale con due stati: non bloccato e bloccato.  Bloccare gli oggetti ogni volta che è possibile migliora le prestazioni dell'applicazione e ne riduce il working set.  Per ulteriori informazioni, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
 Ogni oggetto <xref:System.Windows.Freezable> presenta un evento <xref:System.Windows.Freezable.Changed> che viene generato a ogni modifica dell'oggetto.  Tuttavia, le notifiche delle modifiche sono dispendiose in termini di prestazioni dell'applicazione.  
  
 Nell'esempio riportato di seguito ogni <xref:System.Windows.Shapes.Rectangle> utilizza lo stesso oggetto <xref:System.Windows.Media.Brush>:  
  
 [!code-csharp[Performance#PerformanceSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet2)]
 [!code-vb[Performance#PerformanceSnippet2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet2)]  
  
 Per impostazione predefinita, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce un gestore eventi per l'evento <xref:System.Windows.Freezable.Changed> dell'oggetto <xref:System.Windows.Media.SolidColorBrush> per invalidare la proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> dell'oggetto <xref:System.Windows.Shapes.Rectangle>.  In questo caso, ogni volta che l'evento <xref:System.Windows.Freezable.Changed> deve essere generato da <xref:System.Windows.Media.SolidColorBrush>, è necessario richiamare la funzione di callback per ogni <xref:System.Windows.Shapes.Rectangle>. L'accumulo di queste chiamate alla funzione di callback causa una riduzione significativa delle prestazioni.  Inoltre, aggiungere e rimuovere i gestori a questo punto è molto dispendioso in termini di prestazioni poiché per eseguire tali operazioni l'applicazione deve scorrere tutto l'elenco.  Se lo scenario dell'applicazione non modifica mai l'oggetto <xref:System.Windows.Media.SolidColorBrush>, sulle prestazioni influirà il fatto di conservare gestori per eventi <xref:System.Windows.Freezable.Changed> non necessari.  
  
 Il blocco di un oggetto <xref:System.Windows.Freezable> consente di migliorarne le prestazioni poiché evita di dover impiegare risorse nella conservazione delle notifiche delle modifiche.  Nella tabella riportata di seguito vengono illustrate le dimensioni di un semplice oggetto <xref:System.Windows.Media.SolidColorBrush> quando la relativa proprietà <xref:System.Windows.Freezable.IsFrozen%2A> è impostata su `true`, rispetto a quando non lo è.  Si presuppone l'applicazione di un pennello alla proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> di dieci <xref:System.Windows.Shapes.Rectangle>.  
  
|**Stato**|**Dimensione**|  
|---------------|--------------------|  
|Oggetto <xref:System.Windows.Media.SolidColorBrush> bloccato|212 byte|  
|Oggetto <xref:System.Windows.Media.SolidColorBrush> non bloccato|972 byte|  
  
 Nell'esempio di codice riportato di seguito viene illustrato questo concetto:  
  
 [!code-csharp[Performance#PerformanceSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet3)]
 [!code-vb[Performance#PerformanceSnippet3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet3)]  
  
### I gestori modificati su oggetti Freezable non bloccati può mantenere gli oggetti attivi  
 Il delegato passato da un oggetto all'evento <xref:System.Windows.Freezable.Changed> di un oggetto <xref:System.Windows.Freezable> è un riferimento effettivo a tale oggetto.  Di conseguenza, i gestori di eventi <xref:System.Windows.Freezable.Changed> possono mantenere gli oggetti attivi più a lungo del previsto.  Quando si esegue la pulitura di un oggetto registrato per restare in ascolto di un evento <xref:System.Windows.Freezable.Changed> dell'oggetto <xref:System.Windows.Freezable>, è essenziale rimuovere tale delegato prima di rilasciare l'oggetto.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] esegue anche l'associazione di eventi <xref:System.Windows.Freezable.Changed> internamente.  Ad esempio, tutte le [proprietà di dipendenza](GTMT) che accettano <xref:System.Windows.Freezable> come valore rimangono automaticamente in ascolto di eventi <xref:System.Windows.Freezable.Changed>.  Questo concetto viene illustrato dalla proprietà <xref:System.Windows.Shapes.Shape.Fill%2A>, che accetta <xref:System.Windows.Media.Brush>.  
  
 [!code-csharp[Performance#PerformanceSnippet4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet4)]
 [!code-vb[Performance#PerformanceSnippet4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet4)]  
  
 Al momento dell'assegnazione di `myBrush` a `myRectangle.Fill`, un delegato che punta all'oggetto <xref:System.Windows.Shapes.Rectangle> viene aggiunto all'evento <xref:System.Windows.Freezable.Changed> dell'oggetto <xref:System.Windows.Media.SolidColorBrush>.  Nel codice riportato di seguito, pertanto, `myRect` non viene effettivamente reso idoneo per Garbage Collection:  
  
 [!code-csharp[Performance#PerformanceSnippet5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet5)]
 [!code-vb[Performance#PerformanceSnippet5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet5)]  
  
 In questo caso `myBrush` mantiene `myRectangle` attivo e lo richiama al momento della generazione del relativo evento <xref:System.Windows.Freezable.Changed>.  Si noti che l'assegnazione di `myBrush` alla proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> di un nuovo oggetto <xref:System.Windows.Shapes.Rectangle> aggiunge semplicemente un altro gestore eventi a `myBrush`.  
  
 Per eseguire la pulitura di questi tipi di oggetti è consigliabile rimuovere <xref:System.Windows.Media.Brush> dalla proprietà <xref:System.Windows.Shapes.Shape.Fill%2A>, che a sua volta rimuove il gestore di eventi <xref:System.Windows.Freezable.Changed>.  
  
 [!code-csharp[Performance#PerformanceSnippet6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet6)]
 [!code-vb[Performance#PerformanceSnippet6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet6)]  
  
<a name="User_Interface_Virtualization"></a>   
## Virtualizzazione dell'interfaccia utente  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è disponibile anche una variante dell'elemento <xref:System.Windows.Controls.StackPanel> che "virtualizza" automaticamente il contenuto figlio con associazione a dati.  In questo contesto, il termine "virtualizzare" si riferisce a una tecnica grazie alla quale, a partire da un gran numero di elementi dei dati, viene generato un sottoinsieme di oggetti in base agli elementi visibili sullo schermo.  Generare un elevato numero di elementi dell'interfaccia utente, quando solo alcuni possono essere visualizzati sullo schermo in un dato momento, richiede un intenso consumo di risorse sia in termini di memoria che di processore.  <xref:System.Windows.Controls.VirtualizingStackPanel>, tramite le funzionalità disponibili in <xref:System.Windows.Controls.VirtualizingPanel>, calcola gli elementi visibili e utilizza l'elemento <xref:System.Windows.Controls.ItemContainerGenerator> di un oggetto <xref:System.Windows.Controls.ItemsControl> \(ad esempio <xref:System.Windows.Controls.ListBox> o <xref:System.Windows.Controls.ListView>\) per creare elementi solo per gli elementi visibili.  
  
 Per ottimizzare le prestazioni, gli oggetti visivi per questi elementi vengono generati o mantenuti attivi solo se sono visibili sullo schermo.  Quando non si trovano più nell'area visualizzabile del controllo, è possibile rimuovere gli oggetti visibili.  Questa operazione non deve essere confusa con la virtualizzazione dei dati, in cui gli oggetti dati non sono tutti presenti nella raccolta locale, ma inviati nel flusso in base alle esigenze.  
  
 Nella tabella riportata di seguito viene indicato il tempo trascorso per l'aggiunta e il rendering di 5000 elementi <xref:System.Windows.Controls.TextBlock> in un oggetto <xref:System.Windows.Controls.StackPanel> e in un oggetto <xref:System.Windows.Controls.VirtualizingStackPanel>.  In questo scenario, le misure rappresentano il tempo compreso tra il collegamento di una stringa di testo alla proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> di un oggetto <xref:System.Windows.Controls.ItemsControl> e il tempo in cui tale stringa di testo viene visualizzata nel riquadro.  
  
|**Riquadro host**|**Durata del rendering \(ms\)**|  
|-----------------------|-------------------------------------|  
|<xref:System.Windows.Controls.StackPanel>|3210|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|46|  
  
## Vedere anche  
 [Ottimizzazione delle prestazioni di applicazioni WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [Pianificazione delle prestazioni dell'applicazione](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [Sfruttare appieno l'hardware](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Risorse delle applicazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)