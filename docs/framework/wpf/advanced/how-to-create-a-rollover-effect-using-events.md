---
title: "Procedura: creare un effetto di attivazione utilizzando gli eventi | Microsoft Docs"
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
  - "colori di elementi, modifica"
  - "elementi (colori), modifica"
  - "effetto di attivazione"
ms.assetid: 3b20d028-6f1c-4b25-95d2-fa68cefbdb4c
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: creare un effetto di attivazione utilizzando gli eventi
In questo esempio viene illustrato come modificare il colore di un elemento quando il puntatore del mouse entra o esce dall’area occupata dall'elemento.  
  
 In questo esempio sono presenti un file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e un file code\-behind.  
  
> [!NOTE]
>  In questo esempio viene illustrato come utilizzare gli eventi, ma la modalità consigliata per ottenere lo stesso effetto è utilizzare <xref:System.Windows.Trigger> in un stile.  Per ulteriori informazioni, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
## Esempio  
 Nel [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] riportato di seguito viene creata l’interfaccia utente, composta da <xref:System.Windows.Controls.Border> intorno a <xref:System.Windows.Controls.TextBlock> e vengono collegati i gestori eventi <xref:System.Windows.Input.Mouse.MouseEnter> e <xref:System.Windows.UIElement.MouseLeave> a <xref:System.Windows.Controls.Border>.  
  
 [!code-xml[mouseenterMouseleave#MouseEnterLeaveSampleXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/mouseenterMouseleave/CSharp/Window1.xaml#mouseenterleavesamplexaml)]  
  
 Nell’esempio di code\-behind riportato di seguito vengono creati i gestori eventi <xref:System.Windows.UIElement.MouseEnter> e <xref:System.Windows.UIElement.MouseLeave>.  Quando il puntatore del mouse entra in <xref:System.Windows.Controls.Border>, lo sfondo di <xref:System.Windows.Controls.Border> diventa rosso.  Quando il puntatore del mouse esce da <xref:System.Windows.Controls.Border>, lo sfondo di <xref:System.Windows.Controls.Border> ritorna bianco.  
  
 [!code-csharp[mouseenterMouseleave#MouseEnterLeaveSampleEventHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/mouseenterMouseleave/CSharp/Window1.xaml.cs#mouseenterleavesampleeventhandlers)]
 [!code-vb[mouseenterMouseleave#MouseEnterLeaveSampleEventHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/mouseenterMouseleave/VisualBasic/Window1.xaml.vb#mouseenterleavesampleeventhandlers)]