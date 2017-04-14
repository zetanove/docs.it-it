---
title: "Procedura: utilizzare le propriet&#224; SelectedValue, SelectedValuePath e SelectedItem | Microsoft Docs"
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
  - "Control (classe), SelectedItem (proprietà)"
  - "Control (classe), SelectedValue (proprietà)"
  - "Control (classe), SelectedValuePath (proprietà)"
  - "Control (classe), TreeView (proprietà)"
  - "SelectedValue, SelectedItem (proprietà)"
  - "SelectedValue, SelectedValuePath (proprietà)"
  - "TreeView (controllo), SelectedItem (proprietà)"
  - "TreeView (controllo), SelectedValue (proprietà)"
  - "TreeView (controllo), SelectedValuePath (proprietà)"
ms.assetid: 2fc92ad4-f02c-4f89-bbe9-d4978a7af0db
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: utilizzare le propriet&#224; SelectedValue, SelectedValuePath e SelectedItem
In questo esempio viene illustrato come utilizzare le proprietà <xref:System.Windows.Controls.TreeView.SelectedValue%2A> e <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> per specificare un valore per la proprietà <xref:System.Windows.Controls.TreeView.SelectedItem%2A> di un oggetto <xref:System.Windows.Controls.TreeView>.  
  
## Esempio  
 La proprietà <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> consente di specificare <xref:System.Windows.Controls.TreeView.SelectedValue%2A> per la proprietà <xref:System.Windows.Controls.TreeView.SelectedItem%2A> in un oggetto <xref:System.Windows.Controls.TreeView>.  <xref:System.Windows.Controls.TreeView.SelectedItem%2A> rappresenta un oggetto nella raccolta <xref:System.Windows.Controls.ItemsControl.Items%2A> e nell'oggetto <xref:System.Windows.Controls.TreeView> viene visualizzato il valore di una singola proprietà dell'elemento selezionato.  La proprietà <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> specifica il percorso della proprietà utilizzata per determinare il valore della proprietà <xref:System.Windows.Controls.TreeView.SelectedValue%2A>.  Negli esempi di questo argomento è illustrato questo concetto.  
  
 Nell'esempio riportato di seguito viene illustrato un oggetto <xref:System.Windows.Data.XmlDataProvider> che contiene informazioni sui dipendenti.  
  
 [!code-xml[TreeViewSelectedValue#XMLDataProvider](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#xmldataprovider)]  
  
 Nell'esempio riportato di seguito viene definito un oggetto <xref:System.Windows.HierarchicalDataTemplate> in cui vengono visualizzate le informazioni `EmployeeName` e `EmployeeWorkDay` del `Employee`.  Si noti che in <xref:System.Windows.HierarchicalDataTemplate> le informazioni `EmployeeNumber` non vengono specificate come parte del modello.  
  
 [!code-xml[TreeViewSelectedValue#HierarchicalDataTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#hierarchicaldatatemplate)]  
  
 Nell'esempio riportato di seguito viene illustrato un oggetto <xref:System.Windows.Controls.TreeView> che utilizza l'oggetto <xref:System.Windows.HierarchicalDataTemplate> definito in precedenza e che imposta la proprietà <xref:System.Windows.Controls.TreeView.SelectedValue%2A> su `EmployeeNumber`.  Quando si seleziona un `EmployeeName` nell'oggetto <xref:System.Windows.Controls.TreeView>, la proprietà <xref:System.Windows.Controls.TreeView.SelectedItem%2A> restituisce l'elemento di dati `EmployeeInfo` corrispondente all'elemento `EmployeeName` selezionato.  Tuttavia, poiché la proprietà <xref:System.Windows.Controls.TreeView.SelectedValuePath%2A> di questo oggetto <xref:System.Windows.Controls.TreeView> è impostata su `EmployeeNumber`, la proprietà <xref:System.Windows.Controls.TreeView.SelectedValue%2A> viene impostata su `EmployeeNumber`.  
  
 [!code-xml[TreeViewSelectedValue#SelectedValuePath](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSelectedValue/CS/Window1.xaml#selectedvaluepath)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.TreeView>   
 <xref:System.Windows.Controls.TreeViewItem>   
 [Cenni preliminari sul controllo TreeView](../../../../docs/framework/wpf/controls/treeview-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/treeview-how-to-topics.md)