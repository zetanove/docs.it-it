---
title: "Procedura dettagliata: creazione della prima applicazione a tocco | Microsoft Docs"
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
  - "creazione di un'applicazione touchscreen [WPF]"
  - "creazione di un'applicazione sensibile al tocco [WPF]"
  - "applicazioni touchscreen [WPF], creazione"
  - "applicazioni sensibili al tocco [WPF], creazione"
ms.assetid: d69e602e-9a25-4e24-950b-e89eaa2a906b
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura dettagliata: creazione della prima applicazione a tocco
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consente alle applicazioni di rispondere al tocco.  È ad esempio possibile interagire con un'applicazione utilizzando uno o più dita su un dispositivo sensibile al tocco, ad esempio un touchscreen. In questa procedura dettagliata viene creata un'applicazione che consente all'utente di spostarsi, ridimensionare o ruotare un singolo oggetto tramite tocco.  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev10_ext](../../../../includes/vs-dev10-ext-md.md)].  
  
-   Windows 7.  
  
-   Un dispositivo in grado di accettare l'input tocco, ad esempio un touchscreen che supporta Windows Touch.  
  
 È inoltre necessario disporre di una conoscenza di base della modalità di creazione di un'applicazione in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], in particolare della modalità di sottoscrizione e di gestione di un evento.  Per ulteriori informazioni, vedere [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md).  
  
## Creazione dell'applicazione  
  
#### Per creare l'applicazione  
  
1.  Creare un nuovo progetto di applicazione WPF in Visual Basic o Visual C\# denominato `BasicManipulation`.  Per ulteriori informazioni, vedere [Procedura: creare un nuovo progetto di applicazione WPF](http://msdn.microsoft.com/it-it/1f6aea7a-33e1-4d3f-8555-1daa42e95d82).  
  
2.  Sostituire il contenuto di MainWindow.xaml con il codice XAML riportato di seguito.  
  
     Questo markup consente di creare un'applicazione semplice contenente un oggetto <xref:System.Windows.Shapes.Rectangle> di colore rosso su un oggetto <xref:System.Windows.Controls.Canvas>.  La proprietà <xref:System.Windows.UIElement.IsManipulationEnabled%2A> di <xref:System.Windows.Shapes.Rectangle> viene impostata su true in modo che possa ricevere gli eventi di modifica.  L'applicazione sottoscrive gli eventi <xref:System.Windows.UIElement.ManipulationStarting>, <xref:System.Windows.UIElement.ManipulationDelta> e <xref:System.Windows.UIElement.ManipulationInertiaStarting>.  Questi eventi contengono la logica per spostare <xref:System.Windows.Shapes.Rectangle> quando l'utente lo modifica.  
  
     [!code-xml[BasicManipulation#UI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml#ui)]  
  
3.  Se si utilizza Visual Basic, nella prima riga di MainWindow.xaml sostituire `x:Class="BasicManipulation.MainWindow"` con `x:Class="MainWindow"`.  
  
4.  Nella classe `MainWindow` aggiungere il gestore eventi <xref:System.Windows.UIElement.ManipulationStarting>.  
  
     L'evento <xref:System.Windows.UIElement.ManipulationStarting> si verifica quando [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] rileva l'inizio della modifica di un oggetto tramite input tocco.  Nel codice viene specificato che la posizione della modifica deve essere relativa a <xref:System.Windows.Window> impostando la proprietà <xref:System.Windows.Input.ManipulationStartingEventArgs.ManipulationContainer%2A>.  
  
     [!code-csharp[BasicManipulation#ManipulationStarting](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationstarting)]
     [!code-vb[BasicManipulation#ManipulationStarting](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationstarting)]  
  
5.  Nella classe `MainWindow` aggiungere il gestore eventi <xref:System.Windows.Input.ManipulationDelta>.  
  
     L'evento <xref:System.Windows.Input.ManipulationDelta> si verifica quando la posizione viene modificata tramite input tocco e può verificarsi più volte durante la modifica.  L'evento può inoltre verificarsi dopo il sollevamento di un dito.  Ad esempio, se l'utente sposta un dito su uno schermo, l'evento <xref:System.Windows.Input.ManipulationDelta> si verifica più volte durante lo spostamento del dito.  Quando l'utente solleva un dito dallo schermo, l'evento <xref:System.Windows.Input.ManipulationDelta> continua a verificarsi per simulare l'inerzia.  
  
     Nel codice viene applicata la proprietà <xref:System.Windows.Input.ManipulationDeltaEventArgs.DeltaManipulation%2A> alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> dell'oggetto <xref:System.Windows.Shapes.Rectangle> in modo da spostarlo mentre l'utente sposta l'input tocco.  Viene inoltre verificato se l'oggetto <xref:System.Windows.Shapes.Rectangle> si trova al di fuori dei limiti dell'oggetto <xref:System.Windows.Window> quando l'evento si verifica durante l'inerzia.  In caso affermativo, l'applicazione chiama il metodo <xref:System.Windows.Input.ManipulationDeltaEventArgs.Complete%2A?displayProperty=fullName> per terminare la modifica.  
  
     [!code-csharp[BasicManipulation#ManipulationDelta](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationdelta)]
     [!code-vb[BasicManipulation#ManipulationDelta](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationdelta)]  
  
6.  Nella classe `MainWindow` aggiungere il gestore eventi <xref:System.Windows.UIElement.ManipulationInertiaStarting>.  
  
     L'evento <xref:System.Windows.UIElement.ManipulationInertiaStarting> si verifica quando l'utente solleva tutte le dita dallo schermo.  Nel codice viene impostata la velocità iniziale e la decelerazione per il movimento, l'espansione e la rotazione del rettangolo.  
  
     [!code-csharp[BasicManipulation#ManipulationInertiaStarting](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationinertiastarting)]
     [!code-vb[BasicManipulation#ManipulationInertiaStarting](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationinertiastarting)]  
  
7.  Compilare ed eseguire il progetto.  
  
     Nella finestra verrà visualizzato un quadrato di colore rosso.  
  
## Verifica dell'applicazione  
 Per testare l'applicazione, provare a eseguire le modifiche che seguono.  Si noti che è possibile eseguire più modifiche contemporaneamente.  
  
-   Per spostare <xref:System.Windows.Shapes.Rectangle>, posizionare un dito su <xref:System.Windows.Shapes.Rectangle> e spostare il dito sullo schermo.  
  
-   Per ridimensionare <xref:System.Windows.Shapes.Rectangle>, posizionare due dita su <xref:System.Windows.Shapes.Rectangle> e aprire o chiudere le dita.  
  
-   Per ruotare <xref:System.Windows.Shapes.Rectangle>, posizionare due dita su <xref:System.Windows.Shapes.Rectangle> e ruotare un dito intorno all'altro.  
  
 Per causa l'inerzia, sollevare velocemente le dita dallo schermo durante l'esecuzione delle modifiche precedenti.  L'oggetto <xref:System.Windows.Shapes.Rectangle> continuerà a venire spostato, ridimensionato o ruotato per qualche secondo prima che si fermi.  
  
## Vedere anche  
 <xref:System.Windows.UIElement.ManipulationStarting?displayProperty=fullName>   
 <xref:System.Windows.UIElement.ManipulationDelta?displayProperty=fullName>   
 <xref:System.Windows.UIElement.ManipulationInertiaStarting?displayProperty=fullName>