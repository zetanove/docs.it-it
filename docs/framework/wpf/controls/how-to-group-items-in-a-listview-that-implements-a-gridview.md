---
title: "Procedura: raggruppare gli elementi di un controllo ListView che implementa una GridView | Microsoft Docs"
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
  - "GridView (controlli), raggruppamento di elementi"
  - "raggruppamento di elementi in ListView che implementano GridView"
  - "ListView (controlli), raggruppamento di elementi con GridViews"
ms.assetid: eebef25b-ddc6-424e-a66d-ea228d1bf33d
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: raggruppare gli elementi di un controllo ListView che implementa una GridView
In questo esempio viene illustrato come visualizzare gruppi di elementi nella modalità di visualizzazione <xref:System.Windows.Controls.GridView> di un controllo <xref:System.Windows.Controls.ListView>.  
  
## Esempio  
 Per visualizzare gruppi di elementi in un controllo <xref:System.Windows.Controls.ListView>, definire un oggetto <xref:System.Windows.Data.CollectionViewSource>.  Nell'esempio seguente viene illustrato un oggetto <xref:System.Windows.Data.CollectionViewSource> che raggruppa elementi dei dati in base al valore del campo dati `Catalog`.  
  
 [!code-xml[GridViewWithGroups#GroupingCollectionViewSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#groupingcollectionviewsource)]  
  
 Nell'esempio seguente viene impostata la proprietà <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> per <xref:System.Windows.Controls.ListView> sull'oggetto <xref:System.Windows.Data.CollectionViewSource> definito nell'esempio precedente.  Viene inoltre definita una proprietà <xref:System.Windows.Controls.ItemsControl.GroupStyle%2A> che implementa un controllo <xref:System.Windows.Controls.Expander>.  
  
 [!code-xml[GridViewWithGroups#ListViewGroups](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#listviewgroups)]  
[!code-xml[GridViewWithGroups#ListViewEnd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewWithGroups/CS/Window1.xaml#listviewend)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [Procedure relative](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)