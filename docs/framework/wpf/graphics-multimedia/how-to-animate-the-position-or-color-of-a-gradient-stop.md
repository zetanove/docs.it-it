---
title: "Procedura: animare la posizione o il colore di un cursore sfumatura | Microsoft Docs"
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
  - "animazione, colore degli oggetti GradientStop"
  - "animazione, posizione degli oggetti GradientStop"
  - "colori, animazione"
  - "GradientStop (oggetti), animazione del colore"
  - "GradientStop (oggetti), animazione della posizione"
  - "posizione, animazione"
ms.assetid: 6f5b8b47-6c32-4b8e-98ee-fdf6515ec843
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: animare la posizione o il colore di un cursore sfumatura
In questo esempio viene illustrato come aggiungere un'animazione alle proprietà <xref:System.Windows.Media.GradientStop.Color%2A> e <xref:System.Windows.Media.GradientStop.Offset%2A> degli oggetti <xref:System.Windows.Media.GradientStop>.  
  
## Esempio  
 Nell'esempio seguente viene aggiunta un'animazione a tre cursori sfumatura all'interno di un oggetto <xref:System.Windows.Media.LinearGradientBrush>.  Nell'esempio sono utilizzate tre animazioni, ognuna delle quali aggiunge un'animazione a un cursore sfumatura diverso:  
  
-   La prima animazione, <xref:System.Windows.Media.Animation.DoubleAnimation>, anima la proprietà <xref:System.Windows.Media.GradientStop.Offset%2A> del primo cursore facendola passare da 0.0 a 1.0 e nuovamente a 0.0.  Di conseguenza, il primo colore nella sfumatura si sposta dalla parte sinistra del rettangolo alla parte destra e quindi nuovamente a sinistra.  
  
-   La seconda animazione, <xref:System.Windows.Media.Animation.ColorAnimation>, anima la proprietà <xref:System.Windows.Media.GradientStop.Color%2A> del secondo cursore sfumatura, facendola passare da <xref:System.Windows.Media.Colors.Purple%2A> a <xref:System.Windows.Media.Colors.Yellow%2A> e quindi nuovamente a <xref:System.Windows.Media.Colors.Purple%2A>.  Di conseguenza, il colore centrale nella sfumatura cambia da viola a giallo e di nuovo a viola.  
  
-   La terza animazione, un altro oggetto <xref:System.Windows.Media.Animation.ColorAnimation>, anima l'opacità della proprietà <xref:System.Windows.Media.GradientStop.Color%2A> del terzo cursore sfumatura di un valore pari a \-1 per poi tornare al valore iniziale.  Di conseguenza, il terzo colore nella sfumatura si dissolve e successivamente diviene nuovamente opaco.  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/GradientStopAnimationExample.cs#graphicsmmgradientanimationexampleswholepage)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/gradientstopanimationexample.vb#graphicsmmgradientanimationexampleswholepage)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMGradientAnimationExamplesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/GradientStopAnimationExample.xaml#graphicsmmgradientanimationexampleswholepage)]  
  
 Sebbene in questo esempio si utilizzi un oggetto <xref:System.Windows.Media.LinearGradientBrush>, il processo è lo stesso anche quando si aggiunge un'animazione agli oggetti <xref:System.Windows.Media.GradientStop> in un <xref:System.Windows.Media.RadialGradientBrush>.  
  
 Per ulteriori esempi, vedere [Esempio Brush](http://go.microsoft.com/fwlink/?LinkID=159973) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.GradientStop>   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)