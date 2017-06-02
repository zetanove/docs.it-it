---
title: "Procedura: attivare un comando | Microsoft Docs"
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
  - "CommandBindings"
  - "esecuzione di comandi"
ms.assetid: d8016266-58d9-48f7-8298-a86b7ed49fbd
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: attivare un comando
Nell'esempio seguente viene illustrato l'utilizzo dei comandi in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Nell'esempio viene mostrato come associare un oggetto <xref:System.Windows.Input.RoutedCommand> a uno <xref:System.Windows.Controls.Button>, creare un oggetto <xref:System.Windows.Input.CommandBinding> e creare i gestori eventi che implementano <xref:System.Windows.Input.RoutedCommand>.  Per ulteriori informazioni sull'esecuzione di comandi, vedere [Cenni preliminari sull'esecuzione di comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md).  
  
## Esempio  
 La prima sezione di codice crea l'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)], costituita da un oggetto <xref:System.Windows.Controls.Button> e da un oggetto <xref:System.Windows.Controls.StackPanel>; inoltre crea un oggetto <xref:System.Windows.Input.CommandBinding> che associa i gestori dei comandi all'oggetto <xref:System.Windows.Input.RoutedCommand>.  
  
 La proprietà <xref:System.Windows.Input.ICommandSource.Command%2A> dell'oggetto <xref:System.Windows.Controls.Button> è associata al comando <xref:System.Windows.Input.ApplicationCommands.Close%2A>.  
  
 L'oggetto <xref:System.Windows.Input.CommandBinding> viene aggiunto all'oggetto <xref:System.Windows.Input.CommandBindingCollection> dell'oggetto <xref:System.Windows.Window> radice.  I gestori eventi <xref:System.Windows.Input.CommandBinding.Executed> e <xref:System.Windows.Input.CommandBinding.CanExecute> sono associati a questa associazione e al comando <xref:System.Windows.Input.ApplicationCommands.Close%2A>.  
  
 Senza <xref:System.Windows.Input.CommandBinding> non è possibile determinare una logica di comando, ma solo un meccanismo per richiamare il comando.  Facendo clic su <xref:System.Windows.Controls.Button> viene generato l'evento <xref:System.Windows.Input.CommandManager.PreviewExecuted> <xref:System.Windows.RoutedEvent> nella destinazione comando, seguito dall'evento <xref:System.Windows.Input.CommandManager.Executed> <xref:System.Windows.RoutedEvent>.  Questi eventi attraversano la struttura ad albero dell'elemento alla ricerca di un oggetto <xref:System.Windows.Input.CommandBinding> per quel determinato comando.  È necessario prestare attenzione alla posizione in cui viene inserito <xref:System.Windows.Input.CommandBinding>, dal momento che <xref:System.Windows.RoutedEvent> esegue il tunneling e il bubbling attraverso la struttura ad albero dell'elemento.  Se l'oggetto <xref:System.Windows.Input.CommandBinding> si trova in un elemento di pari livello della destinazione comando o in un altro nodo che non appartiene alla route dell'oggetto <xref:System.Windows.RoutedEvent>, non sarà possibile accedere all'oggetto <xref:System.Windows.Input.CommandBinding>.  
  
 [!code-xml[EnableCloseCommand#CloseCommandBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml#closecommandbinding)]  
  
 [!code-csharp[EnableCloseCommand#CloseCommandBindingCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandbindingcodebehind)]
 [!code-vb[EnableCloseCommand#CloseCommandBindingCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandbindingcodebehind)]  
  
 La successiva sezione di codice implementa i gestori eventi <xref:System.Windows.Input.CommandManager.Executed> e <xref:System.Windows.Input.CommandBinding.CanExecute>.  
  
 Il gestore <xref:System.Windows.Input.CommandManager.Executed> chiama un metodo per chiudere il file aperto.  Il gestore <xref:System.Windows.Input.CommandBinding.CanExecute> chiama un metodo per determinare se un file è aperto.  Se un file risulta aperto, la proprietà <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> è impostata su `true`; in caso contrario, sarà impostata su `false`.  
  
 [!code-csharp[EnableCloseCommand#CloseCommandHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandhandler)]
 [!code-vb[EnableCloseCommand#CloseCommandHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandhandler)]  
  
## Vedere anche  
 [Cenni preliminari sull'esecuzione di comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md)