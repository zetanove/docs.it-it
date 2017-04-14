---
title: "Procedura: impostare i margini di elementi e controlli | Microsoft Docs"
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
  - "Margin (proprietà), impostazione"
  - "proprietà, Margin (proprietà)"
  - "impostazione, Margin (proprietà)"
ms.assetid: 70ebee01-6f87-4352-8dd4-402c65eaaed6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: impostare i margini di elementi e controlli
In questo esempio viene illustrato come impostare la proprietà <xref:System.Windows.FrameworkElement.Margin%2A> mediante la modifica di un qualsiasi valore della proprietà esistente per il margine nel code\-behind.  <xref:System.Windows.FrameworkElement.Margin%2A> è una proprietà dell'elemento di base <xref:System.Windows.FrameworkElement>; pertanto viene ereditata da una serie di controlli e altri elementi.  
  
 Questo esempio è scritto in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], con un file code\-behind al quale [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] fa riferimento.  Il code\-behind viene mostrato in una versione [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] e in una versione [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)].  
  
## Esempio  
 [!code-xml[FEMarginProgrammatic#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[FEMarginProgrammatic#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml.cs#handler)]
 [!code-vb[FEMarginProgrammatic#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FEMarginProgrammatic/VisualBasic/default.xaml.vb#handler)]