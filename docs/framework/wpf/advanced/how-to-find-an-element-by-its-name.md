---
title: "Procedura: individuare un elemento in base al nome | Microsoft Docs"
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
  - "elementi, ricerca per nome"
  - "FindName (metodo)"
ms.assetid: cfa7cf35-8aa2-4060-9454-872ed4af3f0e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: individuare un elemento in base al nome
In questo esempio viene descritto l'utilizzo del metodo <xref:System.Windows.FrameworkElement.FindName%2A> per individuare un elemento in base al relativo valore di <xref:System.Windows.FrameworkElement.Name%2A>.  
  
## Esempio  
 In questo esempio, il metodo per individuare un determinato elemento in base al nome viene scritto come gestore eventi di un pulsante.  `stackPanel` rappresenta la proprietà <xref:System.Windows.FrameworkElement.Name%2A> dell'oggetto <xref:System.Windows.FrameworkElement> radice di cui si esegue la ricerca e il metodo dell'esempio indica quindi visivamente l'elemento trovato eseguendone il cast come <xref:System.Windows.Controls.TextBlock> e modificando una delle proprietà <xref:System.Windows.Controls.TextBlock> visibili dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)].  
  
 [!code-csharp[FEFindName#Find](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEFindName/CSharp/default.xaml.cs#find)]
 [!code-vb[FEFindName#Find](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FEFindName/VisualBasic/default.xaml.vb#find)]