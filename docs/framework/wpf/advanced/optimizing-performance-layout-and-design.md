---
title: "Ottimizzazione delle prestazioni: layout e progettazione | Microsoft Docs"
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
  - "considerazioni di progettazione"
  - "passaggio di layout"
  - "layout, ottimizzazione delle prestazioni"
ms.assetid: 005f4cda-a849-448b-916b-38d14d9a96fe
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Ottimizzazione delle prestazioni: layout e progettazione
La progettazione dell'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] può influire sulle relative prestazioni, poiché crea un sovraccarico non necessario durante il calcolo del layout e la convalida dei riferimenti agli oggetti.  La costruzione degli oggetti, in particolare in fase di esecuzione, può influire sulle caratteristiche di prestazione dell'applicazione.  
  
 In questo argomento vengono forniti i requisiti relativi alle prestazioni in queste aree.  
  
## Layout  
 Con il termine "passaggio di layout" si intende descrivere il processo di misurazione e disposizione dei membri di una raccolta di elementi figlio dell'oggetto derivato dall'oggetto <xref:System.Windows.Controls.Panel> e di disegno sullo schermo.  Il passaggio di layout è un processo molto complesso dal punto di vista matematico: più alto è il numero di elementi figlio presenti nella raccolta, maggiore è il numero di calcoli necessari.  Ad esempio, ogni volta che un oggetto <xref:System.Windows.UIElement> figlio della raccolta cambia posizione, il sistema di layout può eseguire un nuovo passaggio.  Data la stretta relazione tra caratteristiche dell'oggetto e comportamento del layout, è importante comprendere il tipo di eventi che possono richiamare il sistema di layout.  Le prestazioni dell'applicazione risulteranno migliori riducendo il più possibile le chiamate non necessarie al passaggio di layout.  
  
 Per ogni membro figlio di una raccolta vengono completati due passaggi, uno di misurazione e uno di disposizione.  Ogni oggetto figlio fornisce la propria implementazione sottoposta a override dei metodi <xref:System.Windows.UIElement.Measure%2A> e <xref:System.Windows.UIElement.Arrange%2A> per fornire uno specifico comportamento di layout.  Nella sua forma più semplice, il layout è un sistema ricorsivo di ridimensionamento, posizionamento e disegno sullo schermo di un elemento.  
  
-   Il processo di layout di un oggetto <xref:System.Windows.UIElement> figlio ha inizio con la fase di misurazione delle relative proprietà principali.  
  
-   Vengono valutate le proprietà <xref:System.Windows.FrameworkElement> dell'oggetto correlate alle dimensioni, ad esempio <xref:System.Windows.FrameworkElement.Width%2A>, <xref:System.Windows.FrameworkElement.Height%2A>e <xref:System.Windows.FrameworkElement.Margin%2A>.  
  
-   Viene applicata la logica specifica dell'oggetto <xref:System.Windows.Controls.Panel>, ad esempio la proprietà <xref:System.Windows.Controls.DockPanel.Dock%2A> di <xref:System.Windows.Controls.DockPanel> o la proprietà <xref:System.Windows.Controls.StackPanel.Orientation%2A> di <xref:System.Windows.Controls.StackPanel>.  
  
-   Il contenuto viene disposto, o posizionato, dopo la misurazione di tutti gli oggetti figlio.  
  
-   La raccolta di oggetti figlio viene disegnato sullo schermo.  
  
 Il passaggio di layout viene nuovamente richiamato qualora si verifichi una delle azioni elencate di seguito:  
  
-   Un oggetto figlio viene aggiunto alla raccolta.  
  
-   Viene applicata una proprietà <xref:System.Windows.FrameworkElement.LayoutTransform%2A> all'oggetto figlio.  
  
-   Viene chiamato il metodo <xref:System.Windows.UIElement.UpdateLayout%2A> per l'oggetto figlio.  
  
-   Quando viene apportata una modifica al valore di una [proprietà di dipendenza](GTMT) contrassegnata con metadati che influiscono sul passaggio di misurazione o disposizione.  
  
### Utilizzare il pannello più efficiente, se possibile  
 La complessità del processo di layout dipende direttamente dal comportamento di layout degli elementi derivati da <xref:System.Windows.Controls.Panel> utilizzati.  Un controllo <xref:System.Windows.Controls.Grid> o <xref:System.Windows.Controls.StackPanel>, ad esempio, fornisce un numero maggiore di funzionalità rispetto a un controllo <xref:System.Windows.Controls.Canvas>.  All'aumento delle funzionalità corrisponde, tuttavia, un maggiore dispendio in termini di prestazioni.  Pertanto, se le funzionalità fornite da un controllo <xref:System.Windows.Controls.Grid> non sono necessarie, è consigliabile utilizzare le alternative meno costose, ad esempio un oggetto <xref:System.Windows.Controls.Canvas> o un pannello personalizzato.  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md).  
  
### Aggiornare anziché sostituire una proprietà RenderTransform  
 È possibile aggiornare un oggetto <xref:System.Windows.Media.Transform> anziché sostituirlo come valore di una proprietà <xref:System.Windows.UIElement.RenderTransform%2A>.  Questa possibilità riguarda soprattutto gli scenari con animazione.  Aggiornando un oggetto <xref:System.Windows.Media.Transform> esistente si evita di dare inizio a un calcolo di layout non necessario.  
  
### Compilare la struttura ad albero dall'alto in basso  
 Quando si aggiunge o rimuove un nodo dall'[albero logico](GTMT), le convalide di proprietà vengono annullate sull'elemento padre e su tutti gli elementi figlio del nodo.  Di conseguenza, è consigliabile attenersi a un pattern di costruzione dall'alto in basso per evitare il costo di annullamenti di convalide non necessari su nodi che sono già stati convalidati.  Nella tabella riportata di seguito viene illustrata la differenza nella velocità di esecuzione che si riscontra compilando una struttura ad albero dall'alto in basso o dal basso in alto, dove la struttura ad albero presenta 150 livelli di profondità con un singolo oggetto <xref:System.Windows.Controls.TextBlock> e <xref:System.Windows.Controls.DockPanel> a ogni livello.  
  
|**Azione**|**Compilazione della struttura ad albero \(in ms\)**|**Rendering: include la compilazione della struttura ad albero \(in ms\)**|  
|----------------|----------------------------------------------------------|--------------------------------------------------------------------------------|  
|Dal basso in alto|366|454|  
|Dall'alto in basso|11|96|  
  
 Nell'esempio di codice riportato di seguito viene illustrato come creare una struttura ad albero dall'alto in basso.  
  
 [!code-csharp[Performance#PerformanceSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml.cs#performancesnippet1)]
 [!code-vb[Performance#PerformanceSnippet1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/window1.xaml.vb#performancesnippet1)]  
  
 Per ulteriori informazioni sull'albero logico, vedere [Strutture ad albero in WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md).  
  
## Vedere anche  
 [Ottimizzazione delle prestazioni di applicazioni WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [Pianificazione delle prestazioni dell'applicazione](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [Sfruttare appieno l'hardware](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Comportamento dell'oggetto](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Risorse delle applicazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)   
 [Layout](../../../../docs/framework/wpf/advanced/layout.md)