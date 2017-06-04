---
title: "Procedura: scegliere tra StackPanel e DockPanel | Microsoft Docs"
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
  - "controlli [WPF], DockPanel"
  - "controlli [WPF], StackPanel"
  - "DockPanel (controllo), StackPanel (confronto del controllo)"
  - "StackPanel (controllo), DockPanel (confronto del controllo)"
ms.assetid: f9239086-451f-42e6-81f7-ef89ef349742
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: scegliere tra StackPanel e DockPanel
In questo esempio viene illustrato come scegliere se utilizzare un oggetto <xref:System.Windows.Controls.StackPanel> o un oggetto <xref:System.Windows.Controls.DockPanel> per lo stack del contenuto in un oggetto <xref:System.Windows.Controls.Panel>.  
  
## Esempio  
 Anche se è possibile utilizzare <xref:System.Windows.Controls.DockPanel> o <xref:System.Windows.Controls.StackPanel> per lo stack degli elementi figlio, i due controlli non sempre producono gli stessi risultati.  Ad esempio, l'ordine in cui si posizionano gli elementi figlio può influire sulle relative dimensioni in un oggetto <xref:System.Windows.Controls.DockPanel> ma non in un  oggetto <xref:System.Windows.Controls.StackPanel>.  Questo comportamento diverso si verifica perché l'oggetto <xref:System.Windows.Controls.StackPanel> misura la direzione dello stack in corrispondenza di <xref:System.Double>.<xref:System.Double.PositiveInfinity>, mentre l'oggetto <xref:System.Windows.Controls.DockPanel> misura solo le dimensioni disponibili.  
  
 Nell'esempio seguente viene illustrata questa differenza fondamentale tra <xref:System.Windows.Controls.DockPanel> e <xref:System.Windows.Controls.StackPanel>.  
  
 [!code-cpp[StackPanelOvw4#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xml[StackPanelOvw4#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.StackPanel>   
 <xref:System.Windows.Controls.DockPanel>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)