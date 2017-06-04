---
title: "Procedura: allineare orizzontalmente o verticalmente il contenuto in un elemento StackPanel | Microsoft Docs"
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
  - "allineamento, contenuto"
  - "allineamento del contenuto"
  - "StackPanel (controllo), allineamento del contenuto"
ms.assetid: c1e8f962-72c8-4e7a-8670-7a2d7e021791
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: allineare orizzontalmente o verticalmente il contenuto in un elemento StackPanel
In questo esempio viene illustrato come regolare la proprietà <xref:System.Windows.Controls.StackPanel.Orientation%2A> del contenuto all'interno di un elemento <xref:System.Windows.Controls.StackPanel> e inoltre come regolare le proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> e <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> del contenuto figlio.  
  
## Esempio  
 Nell'esempio seguente vengono creati tre elementi <xref:System.Windows.Controls.ListBox> in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Ogni elemento <xref:System.Windows.Controls.ListBox> rappresenta i valori possibili delle proprietà <xref:System.Windows.Controls.StackPanel.Orientation%2A>, <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> e <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> di un elemento <xref:System.Windows.Controls.StackPanel>.  Quando un utente seleziona un valore in uno degli elementi <xref:System.Windows.Controls.ListBox>, la proprietà associata dell'elemento <xref:System.Windows.Controls.StackPanel> e dei relativi elementi <xref:System.Windows.Controls.Button> figlio viene modificata.  
  
 [!code-xml[StackPanelIntroSamp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanelIntroSamp/CSharp/Window1.xaml#1)]  
  
 Nel file code\-behind seguente sono definite le modifiche agli eventi associati alle modifiche della selezione degli elementi <xref:System.Windows.Controls.ListBox>.  L'elemento <xref:System.Windows.Controls.StackPanel> è identificato dal valore `sp1` della proprietà <xref:System.Windows.FrameworkElement.Name%2A>.  
  
 [!code-csharp[StackPanelIntroSamp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanelIntroSamp/CSharp/Window1.xaml.cs#2)]
 [!code-vb[StackPanelIntroSamp#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelIntroSamp/VisualBasic/Window1.xaml.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.StackPanel>   
 <xref:System.Windows.Controls.ListBox>   
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>   
 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)