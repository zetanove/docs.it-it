---
title: "Procedura: creare controlli TreeView semplici o complessi | Microsoft Docs"
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
  - "Control (classe), TreeView, creazione"
  - "TreeView (controllo), creazione"
ms.assetid: 1defbb78-b8e7-4c0e-b650-576453ac828d
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: creare controlli TreeView semplici o complessi
In questo esempio viene illustrato come creare controlli <xref:System.Windows.Controls.TreeView> semplici o complessi.  
  
 Un controllo <xref:System.Windows.Controls.TreeView> è costituito da una gerarchia di controlli <xref:System.Windows.Controls.TreeViewItem> che possono contenere semplici stringhe di testo e anche contenuto più complesso, ad esempio controlli <xref:System.Windows.Controls.Button> o <xref:System.Windows.Controls.StackPanel> con contenuto incorporato.  È possibile definire il contenuto di <xref:System.Windows.Controls.TreeView> in modo esplicito o fornirlo tramite un'origine dati.  In questo argomento vengono forniti esempi di questi concetti.  
  
## Esempio  
 La proprietà <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> dell'oggetto <xref:System.Windows.Controls.TreeViewItem> contiene il contenuto visualizzato dall'oggetto <xref:System.Windows.Controls.TreeView> per tale elemento.  Un controllo <xref:System.Windows.Controls.TreeViewItem> può inoltre disporre di controlli <xref:System.Windows.Controls.TreeViewItem> come elementi figlio, i quali possono essere definiti utilizzando la proprietà <xref:System.Windows.Controls.ItemsControl.Items%2A>.  
  
 Nell'esempio riportato di seguito viene illustrato come definire in modo esplicito il contenuto di <xref:System.Windows.Controls.TreeViewItem> impostando la proprietà <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> su una stringa di testo.  
  
 [!code-xml[TreeViewSimple#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#1)]  
  
 Nell'esempio riportato di seguito viene illustrato come definire elementi figlio di un controllo <xref:System.Windows.Controls.TreeViewItem> mediante la definizione di proprietà <xref:System.Windows.Controls.ItemsControl.Items%2A> che corrispondono a controlli <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[TreeViewSimple#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#3)]  
  
 Nell'esempio riportato di seguito viene illustrato come creare un controllo <xref:System.Windows.Controls.TreeView> in cui un oggetto <xref:System.Windows.Data.XmlDataProvider> fornisce contenuto di <xref:System.Windows.Controls.TreeViewItem> e un oggetto <xref:System.Windows.HierarchicalDataTemplate> definisce l'aspetto del contenuto.  
  
 [!code-xml[TreeViewSimple#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#6)]  
  
 [!code-xml[TreeViewSimple#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#7)]  
  
 [!code-xml[TreeViewSimple#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#5)]  
  
 Nell'esempio riportato di seguito viene illustrato come creare un controllo <xref:System.Windows.Controls.TreeView> in cui il contenuto dell'oggetto <xref:System.Windows.Controls.TreeViewItem> contiene controlli <xref:System.Windows.Controls.DockPanel> con contenuto incorporato.  
  
 [!code-xml[TreeViewSimple#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#9)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.TreeView>   
 <xref:System.Windows.Controls.TreeViewItem>   
 [Cenni preliminari sul controllo TreeView](../../../../docs/framework/wpf/controls/treeview-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/treeview-how-to-topics.md)