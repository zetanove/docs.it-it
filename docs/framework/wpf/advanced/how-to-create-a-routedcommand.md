---
title: "Procedura: creare un oggetto RoutedCommand | Microsoft Docs"
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
  - "classi, RoutedCommand, creazione"
  - "creazione, RoutedCommand (classe)"
  - "RoutedCommand (classe), creazione"
ms.assetid: aaf6979f-69ab-406f-979f-5766daa85fa0
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: creare un oggetto RoutedCommand
In questo esempio viene mostrato come creare un oggetto <xref:System.Windows.Input.RoutedCommand> personalizzato e come implementare il comando personalizzato creando gli oggetti <xref:System.Windows.Input.ExecutedRoutedEventHandler> e <xref:System.Windows.Input.CanExecuteRoutedEventHandler> e associandoli a un oggetto <xref:System.Windows.Input.CommandBinding>.  Per ulteriori informazioni sull'esecuzione di comandi, vedere [Cenni preliminari sull'esecuzione di comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md).  
  
## Esempio  
 Il primo passaggio della creazione di un oggetto <xref:System.Windows.Input.RoutedCommand> consiste nella definizione e nella creazione di un'istanza per il comando.  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommanddefinition)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommanddefinition)]  
  
 Per utilizzare il comando in un'applicazione, è necessario creare gestori eventi che definiscono le operazioni eseguite dal comando  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewExecuted](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewexecuted)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewExecuted](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewexecuted)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCanExecute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcanexecute)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCanExecute](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcanexecute)]  
  
 Successivamente, viene creato un oggetto <xref:System.Windows.Input.CommandBinding> che associa il comando ai gestori eventi.  L'oggetto <xref:System.Windows.Input.CommandBinding> viene creato in un oggetto specifico.  Questo oggetto definisce l'ambito dell'oggetto <xref:System.Windows.Input.CommandBinding> nella struttura ad albero dell'elemento  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewWindowCommandBindingXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewwindowcommandbindingxaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCustomCommandBindingCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcustomcommandbindingcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCustomCommandBindingCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcustomcommandbindingcodebehind)]  
  
 L'ultimo passaggio consiste nel richiamare il comando.  Un modo per richiamare un comando consiste nell'associarlo a un oggetto <xref:System.Windows.Input.ICommandSource>, ad esempio un oggetto <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewcustomcommandsourcexaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcustomcommandsourcecodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcustomcommandsourcecodebehind)]  
  
 Quando si fa clic sull'oggetto Button, viene chiamato il metodo <xref:System.Windows.Input.RoutedCommand.Execute%2A> sull'oggetto <xref:System.Windows.Input.RoutedCommand> personalizzato.  L'oggetto <xref:System.Windows.Input.RoutedCommand> genera gli eventi indirizzati <xref:System.Windows.Input.CommandManager.PreviewExecuted> e <xref:System.Windows.Input.CommandManager.Executed>.  Questi eventi attraversano la struttura ad albero dell'elemento alla ricerca di un oggetto <xref:System.Windows.Input.CommandBinding> per questo comando particolare.  Se viene individuato un oggetto <xref:System.Windows.Input.CommandBinding>, viene chiamato l'oggetto <xref:System.Windows.Input.ExecutedRoutedEventHandler> associato a <xref:System.Windows.Input.CommandBinding>.  
  
## Vedere anche  
 <xref:System.Windows.Input.RoutedCommand>   
 [Cenni preliminari sull'esecuzione di comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md)