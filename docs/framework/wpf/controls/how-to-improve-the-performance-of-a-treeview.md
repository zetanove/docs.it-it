---
title: "Procedura: migliorare le prestazioni di un controllo TreeView | Microsoft Docs"
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
  - "TreeView (controllo) [WPF], miglioramento delle prestazioni"
ms.assetid: b792c740-cf2b-4da8-8ba8-3d2e5a821874
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: migliorare le prestazioni di un controllo TreeView
Se un controllo <xref:System.Windows.Controls.TreeView> contiene molti elementi, il tempo necessario perché venga caricato può comportare un notevole ritardo nell'interfaccia utente.  Per migliorare i tempi di caricamento, impostare la proprietà associata <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=fullName> su `true`.  Sono inoltre possibili lentezze dell'interfaccia utente quando un utente scorre il controllo <xref:System.Windows.Controls.TreeView> agendo sulla rotellina del mouse o trascinando il cursore di una barra di scorrimento.  È possibile migliorare le prestazioni di <xref:System.Windows.Controls.TreeView> quando l'utente scorre la visualizzazione impostando la proprietà associata <xref:System.Windows.Controls.VirtualizingStackPanel.VirtualizationMode%2A?displayProperty=fullName> su <xref:System.Windows.Controls.VirtualizationMode>.  
  
## Esempio  
  
## Descrizione  
 Nell'esempio seguente viene creato un controllo <xref:System.Windows.Controls.TreeView> in cui la proprietà <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=fullName> viene impostata su true e la proprietà <xref:System.Windows.Controls.VirtualizingStackPanel.VirtualizationMode%2A?displayProperty=fullName> su <xref:System.Windows.Controls.VirtualizationMode> per ottimizzare le prestazioni.  
  
## Codice  
 [!code-xml[RecycleItemContainerShippets#VirtualizingTreeView](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizingtreeview)]  
  
 Nell'esempio seguente vengono illustrati i dati utilizzati nell'esempio precedente.  
  
 [!code-csharp[RecycleItemContainerShippets#TreeViewData](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#treeviewdata)]
 [!code-vb[RecycleItemContainerShippets#TreeViewData](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#treeviewdata)]  
  
## Vedere anche  
 [Controlli](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)