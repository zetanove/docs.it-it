---
title: "Cenni preliminari sul controllo TreeView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Control (classe), TreeView"
  - "nodo di espansione"
  - "TreeView (controllo), informazioni sul controllo TreeView"
ms.assetid: 62212512-5a5c-4864-949e-b6a6a3a52c02
caps.latest.revision: 33
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 32
---
# Cenni preliminari sul controllo TreeView
Il controllo <xref:System.Windows.Controls.TreeView> consente di visualizzare informazioni in una struttura gerarchica tramite l'utilizzo di nodi comprimibili.  In questo argomento vengono illustrati i controlli <xref:System.Windows.Controls.TreeView> e <xref:System.Windows.Controls.TreeViewItem> con alcuni semplici esempi del loro utilizzo.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="Simple_TreeView_Control"></a>   
## Definizione di TreeView  
 <xref:System.Windows.Controls.TreeView> è un oggetto <xref:System.Windows.Controls.ItemsControl> che consente di annidare gli elementi utilizzando i controlli <xref:System.Windows.Controls.TreeViewItem>.  Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Windows.Controls.TreeView>.  
  
 [!code-xml[TreeViewSnips#EmbeddedTVIs](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#embeddedtvis)]  
  
<a name="Creating_a_TreeView"></a>   
## Creazione di un controllo TreeView  
 Nel controllo <xref:System.Windows.Controls.TreeView> è contenuta una gerarchia dei controlli <xref:System.Windows.Controls.TreeViewItem>.  <xref:System.Windows.Controls.TreeViewItem> è un controllo <xref:System.Windows.Controls.HeaderedItemsControl> contenente una raccolta di <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> e di <xref:System.Windows.Controls.ItemsControl.Items%2A>.  
  
 Se un controllo <xref:System.Windows.Controls.TreeView> viene definito tramite [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], è possibile definire in modo esplicito il contenuto della proprietà <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> di un controllo <xref:System.Windows.Controls.TreeViewItem> e gli elementi che ne compongono la raccolta.  Nell'illustrazione precedente viene dimostrato questo metodo.  
  
 È inoltre possibile specificare una proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> come origine dati, quindi specificare le proprietà <xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A> e <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> per definire il contenuto dell'oggetto <xref:System.Windows.Controls.TreeViewItem>.  
  
 Per definire il layout di un controllo <xref:System.Windows.Controls.TreeViewItem>, è inoltre possibile utilizzare gli oggetti <xref:System.Windows.HierarchicalDataTemplate>.  Per ulteriori informazioni e un esempio, vedere [Utilizzare gli oggetti SelectedValue, SelectedValuePath e SelectedItem](../../../../docs/framework/wpf/controls/how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md).  
  
 Se un elemento non è un controllo <xref:System.Windows.Controls.TreeViewItem>, viene automaticamente racchiuso da un controllo <xref:System.Windows.Controls.TreeViewItem> quando viene visualizzato il controllo <xref:System.Windows.Controls.TreeView>.  
  
<a name="Expanding_and_Collapsing_a_TreeViewItem"></a>   
## Espansione e compressione di un controllo TreeViewItem  
 Se l'utente espande un controllo <xref:System.Windows.Controls.TreeViewItem>, la proprietà <xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A> viene impostata su `true`.  Un controllo <xref:System.Windows.Controls.TreeViewItem> può inoltre essere espanso o compresso senza un'azione diretta dell'utente impostando la proprietà <xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A> su `true` \(espansione\) o su `false` \(compressione\).  Quando questa proprietà viene modificata, si verifica un evento <xref:System.Windows.Controls.TreeViewItem.Expanded> o <xref:System.Windows.Controls.TreeViewItem.Collapsed>.  
  
 Quando il metodo <xref:System.Windows.FrameworkElement.BringIntoView%2A> viene chiamato su un controllo <xref:System.Windows.Controls.TreeViewItem>, il controllo <xref:System.Windows.Controls.TreeViewItem> e i relativi controlli <xref:System.Windows.Controls.TreeViewItem> padre vengono espansi.  Se un oggetto <xref:System.Windows.Controls.TreeViewItem> non è visibile o è visibile solo in parte, il controllo <xref:System.Windows.Controls.TreeView> scorre per visualizzarlo interamente.  
  
<a name="TreeViewItem_Selection"></a>   
## Selezione del controllo TreeViewItem  
 Quando un utente fa clic su un controllo <xref:System.Windows.Controls.TreeViewItem> per selezionarlo, si verifica l'evento <xref:System.Windows.Controls.TreeViewItem.Selected> e la relativa proprietà <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> viene impostata su `true`.  L'oggetto <xref:System.Windows.Controls.TreeViewItem> diventa anche la proprietà <xref:System.Windows.Controls.TreeView.SelectedItem%2A> del controllo <xref:System.Windows.Controls.TreeView>.  Al contrario, quando la selezione cambia da un controllo <xref:System.Windows.Controls.TreeViewItem>, si verifica l'evento <xref:System.Windows.Controls.TreeViewItem.Unselected> e la relativa proprietà <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> viene impostata su `false`.  
  
 La proprietà <xref:System.Windows.Controls.TreeView.SelectedItem%2A> del controllo <xref:System.Windows.Controls.TreeView> è di sola lettura, pertanto non è possibile impostarla in modo esplicito.  La proprietà <xref:System.Windows.Controls.TreeView.SelectedItem%2A> viene impostata se l'utente fa clic su un controllo <xref:System.Windows.Controls.TreeViewItem> o se la proprietà <xref:System.Windows.Controls.TreeViewItem.IsSelected%2A> viene impostata su `true` per il controllo <xref:System.Windows.Controls.TreeViewItem>.  
  
 Utilizzare la proprietà <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> per specificare un valore <xref:System.Windows.Controls.TreeView.SelectedValue%2A> di una proprietà <xref:System.Windows.Controls.TreeView.SelectedItem%2A>.  Per ulteriori informazioni, vedere [Utilizzare gli oggetti SelectedValue, SelectedValuePath e SelectedItem](../../../../docs/framework/wpf/controls/how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md).  
  
 È possibile registrare un gestore eventi sull'evento <xref:System.Windows.Controls.TreeView.SelectedItemChanged> per determinare quando cambia un oggetto <xref:System.Windows.Controls.TreeViewItem> selezionato.  L'oggetto <xref:System.Windows.RoutedPropertyChangedEventArgs%601> fornito al gestore eventi consente di specificare la proprietà <xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A>, ovvero la selezione precedente, e la proprietà <xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A>, ovvero la selezione corrente.  Entrambi i valori possono essere `null` se l'applicazione o l'utente non ha effettuato alcuna selezione precedente o corrente.  
  
<a name="TreeView_Style"></a>   
## Stile del controllo TreeView  
 In base allo stile predefinito, il controllo <xref:System.Windows.Controls.TreeView> viene inserito in un oggetto <xref:System.Windows.Controls.StackPanel> contenente un controllo <xref:System.Windows.Controls.ScrollViewer>.  Quando si impostano le proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> di un controllo <xref:System.Windows.Controls.TreeView>, questi valori vengono utilizzati per ridimensionare l'oggetto <xref:System.Windows.Controls.StackPanel> in cui viene visualizzato il controllo <xref:System.Windows.Controls.TreeView>.  Se il contenuto da visualizzare è più grande dell'area di visualizzazione, viene automaticamente visualizzato un oggetto <xref:System.Windows.Controls.ScrollViewer> che consente all'utente di scorrere il contenuto dell'oggetto <xref:System.Windows.Controls.TreeView>.  
  
 Per personalizzare l'aspetto di un controllo <xref:System.Windows.Controls.TreeViewItem>, impostare la proprietà <xref:System.Windows.FrameworkElement.Style%2A> su un oggetto <xref:System.Windows.Style> personalizzato.  
  
 Nell'esempio riportato di seguito viene illustrato come impostare i valori delle proprietà <xref:System.Windows.Controls.Control.Foreground%2A> e <xref:System.Windows.Controls.Control.FontSize%2A> per un controllo <xref:System.Windows.Controls.TreeViewItem> utilizzando una proprietà <xref:System.Windows.FrameworkElement.Style%2A>.  
  
 [!code-xml[TreeViewSimple#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#8)]  
  
<a name="Adding_Images_and_oOther_Content_to_TreeView_Items"></a>   
## Aggiunta di immagini e altro contenuto a elementi TreeView  
 È possibile includere più di un oggetto nel contenuto della proprietà <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> di un oggetto <xref:System.Windows.Controls.TreeViewItem>.  Per includere più oggetti nel contenuto della proprietà <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>, racchiudere gli oggetti in un controllo layout, ad esempio un oggetto <xref:System.Windows.Controls.Panel> o <xref:System.Windows.Controls.StackPanel>.  
  
 Nell'esempio riportato di seguito viene illustrato come definire la proprietà <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> di un oggetto <xref:System.Windows.Controls.TreeViewItem> come oggetti <xref:System.Windows.Controls.CheckBox> e <xref:System.Windows.Controls.TextBlock>, entrambi racchiusi in un controllo <xref:System.Windows.Controls.DockPanel>.  
  
 [!code-xml[TreeViewSnips#TVIHeader](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#tviheader)]  
  
 Nell'esempio riportato di seguito viene illustrato come definire un oggetto <xref:System.Windows.DataTemplate> contenente un oggetto <xref:System.Windows.Controls.Image> e un oggetto <xref:System.Windows.Controls.TextBlock> racchiusi in un controllo <xref:System.Windows.Controls.DockPanel>.  È possibile utilizzare un oggetto <xref:System.Windows.DataTemplate> per impostare la proprietà <xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A> o <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> per un oggetto <xref:System.Windows.Controls.TreeViewItem>.  
  
 [!code-xml[TreeViewDataBinding#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewDataBinding/CSharp/Window1.xaml#6)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.TreeView>   
 <xref:System.Windows.Controls.TreeViewItem>   
 [Procedure relative](../../../../docs/framework/wpf/controls/treeview-how-to-topics.md)   
 [Modello di contenuto WPF](../../../../docs/framework/wpf/controls/wpf-content-model.md)