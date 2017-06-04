---
title: "Procedura: aggiungere un&#39;animazione al colore o all’opacit&#224; di un oggetto SolidColorBrush | Microsoft Docs"
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
  - "animazione, colore di SolidColorBrush"
  - "animazione, opacità di SolidColorBrush"
  - "colori, animazione"
  - "opacità, animazione"
  - "SolidColorBrush, animazione del colore"
  - "SolidColorBrush, animazione dell'opacità"
ms.assetid: d9154354-843f-4713-bad1-35bb0ba6eaeb
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: aggiungere un&#39;animazione al colore o all’opacit&#224; di un oggetto SolidColorBrush
In questo esempio viene illustrato come aggiungere un'animazione alle proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> e <xref:System.Windows.Media.Brush.Opacity%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush>.  
  
## Esempio  
 Nell'esempio seguente vengono utilizzate tre animazioni per animare le proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> e <xref:System.Windows.Media.Brush.Opacity%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush>.  
  
-   La prima animazione, un oggetto <xref:System.Windows.Media.Animation.ColorAnimation>, cambia il colore del pennello in <xref:System.Windows.Media.Colors.Gray%2A> quando si sposta il mouse sul rettangolo.  
  
-   La successiva animazione, un altro oggetto <xref:System.Windows.Media.Animation.ColorAnimation>, cambia il colore del pennello in <xref:System.Windows.Media.Colors.Orange%2A> quando si allontana il mouse dal rettangolo.  
  
-   L'ultima animazione, un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation>, cambia l'opacità del pennello in 0,0 quando si preme il pulsante sinistro del mouse.  
  
 [!code-csharp[brushanimations_snip#SolidColorBrushAnimationExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushanimations_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushanimationexample)]  
  
 Per un esempio più completo, in cui venga illustrata l'aggiunta di animazioni a diversi tipi di pennelli, vedere [Esempio Brush](http://go.microsoft.com/fwlink/?LinkID=159973) \(la pagina potrebbe essere in inglese\).  Per ulteriori informazioni sull'animazione, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Per mantenere una coerenza con altri esempi di animazione, nelle versioni del codice di questo esempio viene utilizzato un oggetto <xref:System.Windows.Media.Animation.Storyboard> per applicare le animazioni.  Tuttavia, quando si applica una sola animazione nel codice, è più conveniente utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> anziché un oggetto <xref:System.Windows.Media.Animation.Storyboard>.  Per un esempio, vedere [Animare una proprietà senza utilizzare uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [Esempio Brush](http://go.microsoft.com/fwlink/?LinkID=159973)