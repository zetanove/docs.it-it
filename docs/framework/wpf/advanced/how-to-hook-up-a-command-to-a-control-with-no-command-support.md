---
title: "Procedura: associare un comando a un controllo senza supporto del comando | Microsoft Docs"
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
  - "classi, Controllo, collegamento di un RoutedCommand"
  - "classi, RoutedCommand, collegamento a un controllo"
  - "Control (classe), collegamento di un RoutedCommand"
  - "RoutedCommand (classe), collegamento a un controllo"
ms.assetid: dad08f64-700b-46fb-ad3f-fbfee95f0dfe
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: associare un comando a un controllo senza supporto del comando
Nell'esempio seguente viene mostrato come associare un oggetto <xref:System.Windows.Input.RoutedCommand> a un oggetto <xref:System.Windows.Controls.Control> che non dispone di un supporto incorporato per il comando.  Per un esempio completo in cui i comandi vengono associati a più origini vedere l'[esempio di creazione di un RoutedCommand personalizzato](http://go.microsoft.com/fwlink/?LinkID=159980) \(la pagina potrebbe essere in inglese\).  
  
## Esempio  
 In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] viene fornita una libreria dei comandi comuni regolarmente riscontrati dai programmatori di applicazioni.  La libreria dei comandi include le classi seguenti: <xref:System.Windows.Input.ApplicationCommands>, <xref:System.Windows.Input.ComponentCommands>, <xref:System.Windows.Input.NavigationCommands>, <xref:System.Windows.Input.MediaCommands> e <xref:System.Windows.Documents.EditingCommands>.  
  
 Gli oggetti <xref:System.Windows.Input.RoutedCommand> statici che compongono queste classi non forniscono la logica di comando.  Quest'ultima viene associata al comando con un oggetto <xref:System.Windows.Input.CommandBinding>.  Molti controlli di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dispongono del supporto incorporato di alcuni dei comandi della relativa libreria.  <xref:System.Windows.Controls.TextBox>, ad esempio, supporta molti dei comandi di modifica dell'applicazione, ad esempio <xref:System.Windows.Input.ApplicationCommands.Paste%2A>, <xref:System.Windows.Input.ApplicationCommands.Copy%2A>, <xref:System.Windows.Input.ApplicationCommands.Cut%2A>, <xref:System.Windows.Input.ApplicationCommands.Redo%2A> e <xref:System.Windows.Input.ApplicationCommands.Undo%2A>.  Lo sviluppatore di applicazioni non deve eseguire alcuna operazione particolare affinché questi comandi funzionino con tali controlli.  Se quando il comando viene eseguito la destinazione comando è <xref:System.Windows.Controls.TextBox>, quest'ultima gestirà il comando utilizzando l'oggetto <xref:System.Windows.Input.CommandBinding> incorporato nel controllo.  
  
 Nell'esempio seguente viene mostrato l'utilizzo di un oggetto <xref:System.Windows.Controls.Button> come origine comando per il comando <xref:System.Windows.Input.ApplicationCommands.Open%2A>.  Viene creato un oggetto <xref:System.Windows.Input.CommandBinding> che associa l'oggetto <xref:System.Windows.Input.CanExecuteRoutedEventHandler> specificato e <xref:System.Windows.Input.CanExecuteRoutedEventHandler> all'oggetto <xref:System.Windows.Input.RoutedCommand>.  
  
 Innanzi tutto viene creata l'origine comando.  Come origine comando viene utilizzato un oggetto <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[commandWithHandler#CommandHandlerCommandSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandsource)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerButtonCommandSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbuttoncommandsource)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerButtonCommandSource](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbuttoncommandsource)]  
  
 Vengono creati quindi gli oggetti <xref:System.Windows.Input.ExecutedRoutedEventHandler> e <xref:System.Windows.Input.CanExecuteRoutedEventHandler>.  L'oggetto <xref:System.Windows.Input.ExecutedRoutedEventHandler> consente di visualizzare un oggetto <xref:System.Windows.MessageBox> per indicare che il comando è stato eseguito.  L'oggetto <xref:System.Windows.Input.CanExecuteRoutedEventHandler> imposta la proprietà <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> su `true`.  In genere, il gestore di CanExecute effettua dei controlli più accurati per verificare se è possibile eseguire il comando sulla destinazione comando corrente.  
  
 [!code-csharp[commandWithHandler#CommandHandlerBothHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlerbothhandlers)]
 [!code-vb[commandWithHandler#CommandHandlerBothHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlerbothhandlers)]  
  
 Infine, viene creato un oggetto <xref:System.Windows.Input.CommandBinding> nell'oggetto <xref:System.Windows.Window> radice dell'applicazione che associa i gestori degli eventi indirizzati al comando <xref:System.Windows.Input.ApplicationCommands.Open%2A>.  
  
 [!code-xml[commandWithHandler#CommandHandlerCommandBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandbinding)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerBindingInit](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbindinginit)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerBindingInit](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbindinginit)]  
  
## Vedere anche  
 [Cenni preliminari sull'esecuzione di comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md)   
 [Associare un comando a un controllo con supporto dei comandi](../../../../docs/framework/wpf/advanced/how-to-hook-up-a-command-to-a-control-with-command-support.md)