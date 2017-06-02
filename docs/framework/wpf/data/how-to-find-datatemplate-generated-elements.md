---
title: "Procedura: trovare elementi generati da un oggetto DataTemplate | Microsoft Docs"
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
  - "DataTemplate"
  - "ricerca di elementi DataTemplate"
ms.assetid: bfcd564e-5e9e-451e-8641-a9b5c3cfac90
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: trovare elementi generati da un oggetto DataTemplate
In questo esempio viene illustrato come trovare elementi generati da <xref:System.Windows.DataTemplate>.  
  
## Esempio  
 Nell'esempio, è presente un oggetto <xref:System.Windows.Controls.ListBox> associato ad alcuni dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]:  
  
 [!code-xml[FindGeneratedItems#LB](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#lb)]  
  
 <xref:System.Windows.Controls.ListBox> utilizza il seguente oggetto <xref:System.Windows.DataTemplate>:  
  
 [!code-xml[FindGeneratedItems#DT](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#dt)]  
  
 Per recuperare l'elemento <xref:System.Windows.Controls.TextBlock> generato dall'oggetto <xref:System.Windows.DataTemplate> di un determinato oggetto <xref:System.Windows.Controls.ListBoxItem>, è necessario ottenere l'oggetto <xref:System.Windows.Controls.ListBoxItem>, trovare <xref:System.Windows.Controls.ContentPresenter> all'interno dello stesso oggetto <xref:System.Windows.Controls.ListBoxItem> e chiamare <xref:System.Windows.FrameworkTemplate.FindName%2A> sull'oggetto <xref:System.Windows.DataTemplate> impostato su tale <xref:System.Windows.Controls.ContentPresenter>.  Nell'esempio riportato di seguito viene illustrata la modalità di esecuzione di questa procedura.  Viene creata, a scopo dimostrativo, una finestra di messaggio in cui è visualizzato il contenuto di testo del blocco di testo generato da <xref:System.Windows.DataTemplate>.  
  
 [!code-csharp[FindGeneratedItems#DTFindElement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#dtfindelement)]
 [!code-vb[FindGeneratedItems#DTFindElement](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#dtfindelement)]  
  
 Di seguito viene mostrata l'implementazione di `FindVisualChild`, che utilizza i metodi <xref:System.Windows.Media.VisualTreeHelper>:  
  
 [!code-csharp[FindGeneratedItems#FVC](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#fvc)]
 [!code-vb[FindGeneratedItems#FVC](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#fvc)]  
  
## Vedere anche  
 [Procedura: trovare elementi generati da un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/how-to-find-controltemplate-generated-elements.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [NameScope XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md)   
 [Strutture ad albero in WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)