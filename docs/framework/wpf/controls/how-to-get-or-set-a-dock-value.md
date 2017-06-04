---
title: "Procedura: ottenere o impostare un valore Dock | Microsoft Docs"
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
  - "Dock (valori), recupero"
  - "Dock (valori), impostazione"
ms.assetid: fcf4ab8a-c7cd-4835-8d04-de1c999ab4a8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: ottenere o impostare un valore Dock
Nell'esempio seguente viene illustrato come assegnare un valore <xref:System.Windows.Controls.Dock> per un oggetto.  Vengono utilizzati i metodi <xref:System.Windows.Controls.DockPanel.GetDock%2A> e <xref:System.Windows.Controls.DockPanel.SetDock%2A> dell'oggetto <xref:System.Windows.Controls.DockPanel>.  
  
## Esempio  
 In questo esempio viene creata un'istanza dell'elemento <xref:System.Windows.Controls.TextBlock>, `txt1`, e viene assegnato il valore `Top` all'enumerazione <xref:System.Windows.Controls.Dock> utilizzando il metodo <xref:System.Windows.Controls.DockPanel.SetDock%2A> dell'oggetto <xref:System.Windows.Controls.DockPanel>.  Viene quindi aggiunto il valore della proprietà dell'enumerazione <xref:System.Windows.Controls.Dock> alla proprietà <xref:System.Windows.Controls.TextBlock.Text%2A> dell'elemento <xref:System.Windows.Controls.TextBlock> utilizzando il metodo <xref:System.Windows.Controls.DockPanel.GetDock%2A>.  Infine, viene aggiunto l'elemento <xref:System.Windows.Controls.TextBlock> all'elemento padre dell'oggetto <xref:System.Windows.Controls.DockPanel>, `dp1`.  
  
 [!code-csharp[DockPanelSetDock#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DockPanelSetDock/CSharp/DockPanel_SetDock.cs#1)]
 [!code-vb[DockPanelSetDock#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelSetDock/VisualBasic/DockPanel_SetDock.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.DockPanel>   
 <xref:System.Windows.Controls.DockPanel.GetDock%2A>   
 <xref:System.Windows.Controls.DockPanel.SetDock%2A>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)