---
title: "Procedura: ottenere un oggetto ListBoxItem | Microsoft Docs"
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
  - "ListBox (controlli), recupero di un elemento ListBoxItem"
  - "ListBoxItem"
ms.assetid: da877c6f-5fd8-40cb-8909-225cbfd99aa5
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: ottenere un oggetto ListBoxItem
Per ottenere un oggetto <xref:System.Windows.Controls.ListBoxItem> specifico in un particolare indice in <xref:System.Windows.Controls.ListBox>, è possibile utilizzare <xref:System.Windows.Controls.ItemContainerGenerator>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato <xref:System.Windows.Controls.ListBox> con i relativi elementi.  
  
 [!code-xml[ListBoxItems#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml#1)]  
  
 Nell'esempio riportato di seguito viene illustrato come recuperare l'elemento specificandone l'indice nella proprietà <xref:System.Windows.Controls.ItemContainerGenerator.ContainerFromIndex%2A> di <xref:System.Windows.Controls.ItemContainerGenerator>.  
  
 [!code-csharp[ListBoxItems#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ListBoxItems#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxItems/VisualBasic/Window1.xaml.vb#2)]  
  
 Dopo avere recuperato l'elemento casella di riepilogo, è possibile visualizzarne il contenuto come illustrato nell'esempio che segue.  
  
 [!code-csharp[ListBoxItems#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxItems/CSharp/Window1.xaml.cs#3)]
 [!code-vb[ListBoxItems#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxItems/VisualBasic/Window1.xaml.vb#3)]