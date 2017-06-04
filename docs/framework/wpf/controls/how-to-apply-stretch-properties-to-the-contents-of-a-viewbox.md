---
title: "Procedura: applicare le propriet&#224; Stretch al contenuto di un Viewbox | Microsoft Docs"
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
  - "controlli, Viewbox"
  - "Stretch (proprietà)"
  - "StretchDirection (proprietà)"
  - "Viewbox (controllo)"
ms.assetid: b9c22ef4-bce4-4300-9e0c-8260b7db83cc
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: applicare le propriet&#224; Stretch al contenuto di un Viewbox
## Esempio  
 In questo esempio viene illustrato come modificare il valore delle proprietà <xref:System.Windows.Controls.Viewbox.StretchDirection%2A> e <xref:System.Windows.Controls.Viewbox.Stretch%2A> di un oggetto <xref:System.Windows.Controls.Viewbox>.  
  
 Nel primo esempio viene utilizzato [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] per definire un elemento <xref:System.Windows.Controls.Viewbox>.  Alle proprietà <xref:System.Windows.FrameworkElement.MaxWidth%2A> e <xref:System.Windows.FrameworkElement.MaxHeight%2A> viene assegnato il valore 400.  Nell'esempio, un elemento <xref:System.Windows.Controls.Image> viene annidato all'interno dell'oggetto <xref:System.Windows.Controls.Viewbox>.  Gli elementi <xref:System.Windows.Controls.Button> che corrispondono ai valori di proprietà per le enumerazioni <xref:System.Windows.Controls.Viewbox.Stretch%2A> e <xref:System.Windows.Controls.StretchDirection> modificano il comportamento di adattamento dell'oggetto <xref:System.Windows.Controls.Image> annidato.  
  
 [!code-xml[viewboxStretchLayoutSamp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml#1)]  
  
 Il file code\-behind seguente gestisce gli eventi <xref:System.Windows.Controls.Button><xref:System.Windows.Controls.Primitives.ButtonBase.Click> definiti nell'esempio [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] precedente.  
  
 [!code-csharp[viewboxStretchLayoutSamp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml.cs#2)]
 [!code-vb[viewboxStretchLayoutSamp#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/viewboxStretchLayoutSamp/VisualBasic/Window1.xaml.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Viewbox>   
 <xref:System.Windows.Media.Stretch>   
 <xref:System.Windows.Controls.StretchDirection>