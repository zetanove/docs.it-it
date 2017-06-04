---
title: "Procedura: associare un comando a un controllo con supporto del comando | Microsoft Docs"
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
  - "Classe di controllo, collegamento di un RoutedCommand"
  - "classi, controllo, collegamento di un RoutedCommand"
  - "RoutedCommand (classe), collegamento a un controllo"
  - "classi, RoutedCommand, collegamento a un controllo"
ms.assetid: 8d8592ae-0c91-469e-a1cd-d179c4544548
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: associare un comando a un controllo con supporto del comando
Nell'esempio seguente viene illustrato come associare un <xref:System.Windows.Input.RoutedCommand> per un <xref:System.Windows.Controls.Control> che dispone del supporto per il comando incorporato.  Per un esempio completo in cui i comandi in più origini, vedere il [Create a Custom RoutedCommand Sample](http://go.microsoft.com/fwlink/?LinkID=159980) esempio.  
  
## <a name="example"></a>Esempio  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]fornisce una libreria di comandi comuni regolarmente riscontrati dai programmatori di applicazioni.  Le classi che costituiscono la libreria del comando sono: <xref:System.Windows.Input.ApplicationCommands>, <xref:System.Windows.Input.ComponentCommands>, <xref:System.Windows.Input.NavigationCommands>, <xref:System.Windows.Input.MediaCommands>, e <xref:System.Windows.Documents.EditingCommands>.  
  
 Il metodo statico <xref:System.Windows.Input.RoutedCommand> gli oggetti che compongono queste classi forniscono la logica di comando.  La logica per il comando è associata al comando con un <xref:System.Windows.Input.CommandBinding>.  Alcuni controlli dispongono del CommandBindings incorporato per determinati comandi.  Questo meccanismo consente di modifica la semantica di rimangono invariati, mentre l'implementazione effettiva di un comando.  Oggetto <xref:System.Windows.Controls.TextBox>, ad esempio, gestisce il <xref:System.Windows.Input.ApplicationCommands.Paste%2A> comando in modo diverso rispetto a un controllo progettato per supportare immagini, ma l'idea di cosa significhi Incolla base rimane la stessa.  La logica di comando non può essere fornita dal comando, ma piuttosto deve essere fornita dal controllo o l'applicazione.  
  
 Tuttavia, molti controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dispongono del supporto per alcuni dei comandi nella libreria del comando incorporato.  <xref:System.Windows.Controls.TextBox>, ad esempio, supporta molti dei comandi di modifica dell'applicazione, ad esempio <xref:System.Windows.Input.ApplicationCommands.Paste%2A>, <xref:System.Windows.Input.ApplicationCommands.Copy%2A>, <xref:System.Windows.Input.ApplicationCommands.Cut%2A>, <xref:System.Windows.Input.ApplicationCommands.Redo%2A>, e <xref:System.Windows.Input.ApplicationCommands.Undo%2A>.  Lo sviluppatore dell'applicazione non deve eseguire alcuna operazione particolare per ottenere i comandi seguenti per utilizzare questi controlli.  Se il <xref:System.Windows.Controls.TextBox> è la destinazione del comando quando viene eseguito il comando, quest ' ultima gestirà il comando usando il <xref:System.Windows.Input.CommandBinding> che viene incorporato nel controllo.  
  
 Di seguito viene mostrato come utilizzare un <xref:System.Windows.Controls.MenuItem> come origine comando per il <xref:System.Windows.Input.ApplicationCommands.Paste%2A> comando, in cui un <xref:System.Windows.Controls.TextBox> è la destinazione del comando.  Tutta la logica che definisce come il <xref:System.Windows.Controls.TextBox> esegue Incolla è incorporata il <xref:System.Windows.Controls.TextBox> controllo.  
  
 Oggetto <xref:System.Windows.Controls.MenuItem> viene creato ed è <xref:System.Windows.Controls.MenuItem.Command%2A> è impostata sul <xref:System.Windows.Input.ApplicationCommands.Paste%2A> comando.  Il <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> non è impostata in modo esplicito la <xref:System.Windows.Controls.TextBox> oggetto.  Quando il <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> non è impostata, la destinazione del comando è l'elemento che lo stato attivo.  Se l'elemento che lo stato attivo non supporta il <xref:System.Windows.Input.ApplicationCommands.Paste%2A> comando o attualmente non è possibile eseguire il comando Incolla (ad esempio, negli Appunti sono vuoto,), la <xref:System.Windows.Controls.MenuItem> verrebbe visualizzato in grigio.  
  
 [!code-xml[MenuItemCommandTask_XAML#MenuItemCommanding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask_XAML/CS/Window1.xaml#menuitemcommanding)]  
  
 [!code-csharp[MenuItemCommandTask#MenuItemCommandingCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask/CSharp/Window1.xaml.cs#menuitemcommandingcodebehind)]
 [!code-vb[MenuItemCommandTask#MenuItemCommandingCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MenuItemCommandTask/VisualBasic/Window1.xaml.vb#menuitemcommandingcodebehind)]  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica dei comandi](../../../../docs/framework/wpf/advanced/commanding-overview.md)   
 [Associare un comando a un controllo senza supporto del comando](../../../../docs/framework/wpf/advanced/how-to-hook-up-a-command-to-a-control-with-no-command-support.md)