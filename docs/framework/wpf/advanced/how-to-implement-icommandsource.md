---
title: "Procedura: implementare ICommandSource | Microsoft Docs"
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
  - "ICommandSource (interfacce), implementazione"
  - "interfacce, ICommandSource, implementazione"
ms.assetid: 7452dd39-6e11-44bf-806a-31d87f3772ac
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: implementare ICommandSource
In questo esempio viene mostrato come creare un'origine comando implementando <xref:System.Windows.Input.ICommandSource>.  Un'origine comando è un oggetto in grado di richiamare un comando.  L'interfaccia <xref:System.Windows.Input.ICommandSource> espone tre membri: <xref:System.Windows.Input.ICommandSource.Command%2A>, <xref:System.Windows.Input.ICommandSource.CommandParameter%2A> e <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>.  <xref:System.Windows.Input.ICommandSource.Command%2A> è il comando che verrà richiamato.  <xref:System.Windows.Input.ICommandSource.CommandParameter%2A> è un tipo di dati definito dall'utente che viene passato dall'origine comando al metodo che gestisce il comando.  <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> è l'oggetto su cui si sta eseguendo il comando.  
  
 In questo esempio, viene generata una classe che crea una sottoclasse del controllo <xref:System.Windows.Controls.Slider> e implementa <xref:System.Windows.Input.ICommandSource>.  
  
## Esempio  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono fornite varie classi che implementano <xref:System.Windows.Input.ICommandSource>, ad esempio <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.MenuItem> e <xref:System.Windows.Controls.ListBoxItem>.  Un'origine comando definisce il modo in cui richiama un comando.  Le classi <xref:System.Windows.Controls.Button> e <xref:System.Windows.Controls.MenuItem> richiamano un comando quando vengono selezionate.  La classe <xref:System.Windows.Controls.ListBoxItem> richiama un comando quando viene selezionato con un doppio clic.  Queste classi diventano un'origine comando solo quando viene impostata la proprietà <xref:System.Windows.Input.ICommandSource.Command%2A>.  
  
 In questo esempio, il comando viene richiamato quando il dispositivo di scorrimento viene spostato, o più precisamente, quando la proprietà <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> viene modificata.  
  
 Di seguito viene riportata la definizione di classe.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceClassDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourceclassdefinition)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceClassDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourceclassdefinition)]  
  
 Il passaggio successivo consiste nell'implementazione dei membri <xref:System.Windows.Input.ICommandSource>.  In questo esempio, le proprietà vengono implementate come oggetti <xref:System.Windows.DependencyProperty>.  Tale operazione consente alle proprietà di utilizzare l'associazione dati.  Per ulteriori informazioni sulla classe <xref:System.Windows.DependencyProperty>, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  Per ulteriori informazioni sull'associazione dati, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
 Di seguito viene riportata solo la proprietà <xref:System.Windows.Input.ICommandSource.Command%2A>.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandpropertydefinition)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandpropertydefinition)]  
  
 Di seguito viene riportato il callback di modifica <xref:System.Windows.DependencyProperty>.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandChanged](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandchanged)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceCommandChanged](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandchanged)]  
  
 Il passaggio successivo consiste nell'aggiunta e nella rimozione del comando associato all'origine comando.  La proprietà <xref:System.Windows.Input.ICommandSource.Command%2A> non può semplicemente essere sovrascritta quando si aggiunge un nuovo comando, poiché è necessario innanzitutto rimuovere i gestori eventi associati al comando precedente, se presente.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcehookunhookcommands)]
 [!code-vb[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcehookunhookcommands)]  
  
 L'ultimo passaggio consiste nella creazione della logica per il gestore <xref:System.Windows.Input.ICommand.CanExecuteChanged> e il metodo <xref:System.Windows.Input.ICommand.Execute%2A>.  
  
 L'evento <xref:System.Windows.Input.ICommand.CanExecuteChanged> notifica all'origine comando la probabile modifica della capacità del comando di essere eseguito nella destinazione comando corrente.  Quando un'origine comando riceve questo evento, in genere chiama il metodo <xref:System.Windows.Input.ICommand.CanExecute%2A> del comando.  Se non è possibile eseguire il comando nella destinazione comando corrente, l'origine comando in genere si disabilita.  Se è possibile eseguire il comando nella destinazione comando corrente, l'origine comando in genere si attiva.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandCanExecuteChanged](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandcanexecutechanged)]
 [!code-vb[ImplementICommandSource#ImplementICommandCanExecuteChanged](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandcanexecutechanged)]  
  
 L'ultimo passaggio è rappresentato dal metodo <xref:System.Windows.Input.ICommand.Execute%2A>.  Se il comando è <xref:System.Windows.Input.RoutedCommand>, viene chiamato il metodo <xref:System.Windows.Input.RoutedCommand.Execute%2A> di <xref:System.Windows.Input.RoutedCommand>; in caso contrario, viene chiamato il metodo <xref:System.Windows.Input.ICommand.Execute%2A> di <xref:System.Windows.Input.ICommand>.  
  
 [!code-csharp[ImplementICommandSource#ImplementICommandExecute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandexecute)]
 [!code-vb[ImplementICommandSource#ImplementICommandExecute](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandexecute)]  
  
## Vedere anche  
 <xref:System.Windows.Input.ICommandSource>   
 <xref:System.Windows.Input.ICommand>   
 <xref:System.Windows.Input.RoutedCommand>   
 [Cenni preliminari sull'esecuzione di comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md)