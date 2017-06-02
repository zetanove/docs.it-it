---
title: "Procedura: associare una visualizzazione struttura ad albero a dati di profondit&#224; non determinabile | Microsoft Docs"
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
  - "TreeView (controllo) [WPF], associazione a dati di profondità indeterminata"
ms.assetid: daddcd74-1b0f-4ffd-baeb-ec934c5e0f53
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: associare una visualizzazione struttura ad albero a dati di profondit&#224; non determinabile
Possono verificarsi condizioni in cui è necessario eseguire l'associazione di un oggetto <xref:System.Windows.Controls.TreeView> a un un'origine dati di cui non è nota la profondità.  Questa situazione può verificarsi quando i dati sono ricorsivi, ad esempio un file system, dove le cartelle possono contenere cartelle, o una struttura organizzativa di una società, dove i dipendenti dispongono di altri dipendenti come referenti diretti.  
  
 L'origine dati deve disporre di un modello a oggetti gerarchico.  Ad esempio, una classe `Employee` potrebbe contenere una raccolta di oggetti Employee che sono i referenti diretti di un dipendente.  Se i dati vengono rappresentati in un modo non gerarchico, è necessario compilare una rappresentazione gerarchica dei dati.  
  
 Se si imposta la proprietà <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A?displayProperty=fullName> e se <xref:System.Windows.Controls.ItemsControl> genera un oggetto <xref:System.Windows.Controls.ItemsControl> per ogni elemento figlio, l'oggetto <xref:System.Windows.Controls.ItemsControl> figlio utilizzerà lo stesso oggetto <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> dell'oggetto padre.  Ad esempio, se si imposta la proprietà <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> su un oggetto <xref:System.Windows.Controls.TreeView> con associazione a dati, ogni oggetto <xref:System.Windows.Controls.TreeViewItem> generato utilizza l'oggetto <xref:System.Windows.DataTemplate> assegnato alla proprietà <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> dell'oggetto <xref:System.Windows.Controls.TreeView>.  
  
 <xref:System.Windows.HierarchicalDataTemplate> consente di specificare l'oggetto <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> per un oggetto <xref:System.Windows.Controls.TreeViewItem> o per qualsiasi oggetto <xref:System.Windows.Controls.HeaderedItemsControl> nel modello di dati.  Quando si imposta la proprietà <xref:System.Windows.HierarchicalDataTemplate.ItemsSource%2A?displayProperty=fullName>, tale valore viene utilizzato quando viene applicato l'oggetto <xref:System.Windows.HierarchicalDataTemplate>.  Utilizzando un oggetto <xref:System.Windows.HierarchicalDataTemplate>, è possibile impostare in modo ricorsivo l'oggetto <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> per ogni oggetto <xref:System.Windows.Controls.TreeViewItem> nell'oggetto <xref:System.Windows.Controls.TreeView>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come eseguire l'associazione di un oggetto <xref:System.Windows.Controls.TreeView> ai dati gerarchici e utilizzare un oggetto <xref:System.Windows.HierarchicalDataTemplate> per specificare l'oggetto <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> per ogni oggetto <xref:System.Windows.Controls.TreeViewItem>.  L'oggetto <xref:System.Windows.Controls.TreeView> esegue l'associazione ai dati XML che rappresentano i dipendenti di una società.  Ogni elemento `Employee` può contenere altri elementi `Employee` per indicare la struttura gerarchica.  Poiché i dati sono ricorsivi, <xref:System.Windows.HierarchicalDataTemplate> può essere applicato a ogni livello.  
  
 [!code-xml[TreeViewWithUnknownDepth#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewWithUnknownDepth/CS/Window1.xaml#1)]  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md)