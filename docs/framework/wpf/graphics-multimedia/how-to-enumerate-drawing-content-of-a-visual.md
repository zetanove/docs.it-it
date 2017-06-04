---
title: "Procedura: enumerare il contenuto del disegno di un oggetto Visual | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "enumerazione del contenuto di un oggetto Visual [WPF]"
  - "recupero del valore DrawingGroup di un oggetto Visual [WPF]"
ms.assetid: 2974ddb3-2997-4713-8fd2-e93d549c58a8
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# Procedura: enumerare il contenuto del disegno di un oggetto Visual
L'oggetto <xref:System.Windows.Media.Drawing> fornisce un modello a oggetti per l'enumerazione del contenuto di <xref:System.Windows.Media.Visual>.  
  
## Esempio  
 Nell’esempio riportato di seguito viene utilizzato il metodo <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> per recuperare il valore <xref:System.Windows.Media.DrawingGroup> di un oggetto <xref:System.Windows.Media.Visual> e per enumerarlo.  
  
> [!NOTE]
>  Quando viene enumerato il contenuto dell'oggetto visivo, vengono recuperati oggetti <xref:System.Windows.Media.Drawing> e non la rappresentazione sottostante dei dati di rendering come elenco di istruzioni della grafica vettoriale.  Per ulteriori informazioni, vedere [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md).  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
## Vedere anche  
 <xref:System.Windows.Media.Drawing>   
 <xref:System.Windows.Media.DrawingGroup>   
 <xref:System.Windows.Media.VisualTreeHelper>   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)