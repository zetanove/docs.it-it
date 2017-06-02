---
title: "Procedura: fare in modo che un oggetto segua il puntatore del mouse | Microsoft Docs"
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
  - "cursore (puntatore del mouse), creazione di oggetti che seguono"
  - "che seguono il puntatore del mouse (cursore)"
  - "puntatore del mouse (cursore), creazione di oggetti che seguono"
ms.assetid: 50b20415-14bc-405c-baf3-2fb254fffde3
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: fare in modo che un oggetto segua il puntatore del mouse
In questo esempio viene illustrato come modificare le dimensioni di un oggetto quando il puntatore del mouse si sposta sullo schermo.  
  
 Nell'esempio è incluso un file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] che crea [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] e un file code\-behind che crea il gestore di eventi.  
  
## Esempio  
 Nel codice [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] riportato di seguito viene creato [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], costituito da <xref:System.Windows.Shapes.Ellipse> all’interno di <xref:System.Windows.Controls.StackPanel> e viene allegato il gestore eventi per l’evento <xref:System.Windows.UIElement.MouseMove>.  
  
 [!code-xml[mouseMoveWithPointer#MouseMoveWithPointerXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/mouseMoveWithPointer/CSharp/Window1.xaml#mousemovewithpointerxaml)]  
  
 Nell’esempio di code\-behind riportato di seguito viene creati il gestore eventi <xref:System.Windows.UIElement.MouseMove>.  Quando il puntatore del mouse si sposta, l'altezza e la larghezza di <xref:System.Windows.Shapes.Ellipse> vengono aumentate e ridotte.  
  
 [!code-csharp[mouseMoveWithPointer#MouseMovePointerGetPosition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/mouseMoveWithPointer/CSharp/Window1.xaml.cs#mousemovepointergetposition)]
 [!code-vb[mouseMoveWithPointer#MouseMovePointerGetPosition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/mouseMoveWithPointer/VisualBasic/Window1.xaml.vb#mousemovepointergetposition)]  
  
## Vedere anche  
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)