---
title: "Procedura: rendere trasparente o semitrasparente un oggetto UIElement | Microsoft Docs"
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
  - "opacità, di UIElement"
  - "trasparenza di UIElement"
  - "UIElement, opacità"
  - "UIElement, trasparenza"
ms.assetid: a49fc8d6-7b32-4f28-9122-39b632a19b4b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: rendere trasparente o semitrasparente un oggetto UIElement
In questo esempio viene mostrato come rendere trasparente o semitrasparente un oggetto <xref:System.Windows.UIElement>.  Per rendere trasparente o semitrasparente un elemento, è necessario impostarne la proprietà <xref:System.Windows.UIElement.Opacity%2A>.  Un valore pari a `0.0` rende completamente trasparente l'elemento, mentre un valore pari a `1.0` lo rende completamente opaco.  Un valore pari a `0.5` rende opaco l'elemento al 50% e così via.  La proprietà <xref:System.Windows.UIElement.Opacity%2A> di un elemento è impostata in modo predefinito su `1.0`.  
  
## Esempio  
 Nell'esempio seguente, l'oggetto <xref:System.Windows.UIElement.Opacity%2A> di un pulsante viene impostato su `0.25`, rendendo opaco l'oggetto e il relativo contenuto \(in questo caso, il testo del pulsante\) al 25%.  
  
 [!code-xml[brushsamples_snip#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#2)]  
  
 [!code-csharp[brushsamples_procedural_snip#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#2)]  
  
 Se il contenuto di un elemento dispone delle proprie impostazioni <xref:System.Windows.UIElement.Opacity%2A>, quei valori vengono moltiplicati per la proprietà <xref:System.Windows.UIElement.Opacity%2A> degli elementi contenitore.  
  
 Nell'esempio seguente, la proprietà <xref:System.Windows.UIElement.Opacity%2A> di un pulsante viene impostata su `0.25` e la proprietà <xref:System.Windows.UIElement.Opacity%2A> di un controllo <xref:System.Windows.Controls.Image> contenuto all'interno del pulsante su `0.5`.  Di conseguenza, l'immagine appare opaca al 12,5%: 0,25 \* 0,5 \= 0,125.  
  
 [!code-xml[brushsamples_snip#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#3)]  
  
 [!code-csharp[brushsamples_procedural_snip#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#3)]  
  
 Un altro modo per controllare l'opacità di un elemento consiste nell'impostare l'opacità dell'oggetto <xref:System.Windows.Media.Brush> che disegna l'elemento.  Questo approccio consente di modificare in modo selettivo l'opacità di alcune parti di un elemento e offre vantaggi in termini di prestazioni rispetto all'utilizzo della proprietà <xref:System.Windows.UIElement.Opacity%2A> dell'elemento.  Nell'esempio seguente, la proprietà <xref:System.Windows.Media.Brush.Opacity%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush> utilizzato per disegnare l'oggetto <xref:System.Windows.Controls.Control.Background%2A> del pulsante viene impostata su `0.25`.  Di conseguenza, lo sfondo del pennello risulta opaco al 25%, mentre il contenuto \(il testo del pulsante\) rimane opaco al 100%.  
  
 [!code-xml[brushsamples_snip#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#4)]  
  
 [!code-csharp[brushsamples_procedural_snip#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#4)]  
  
 È inoltre possibile controllare l'opacità di singoli colori all'interno di un pennello.  Per ulteriori informazioni sui colori e sui pennelli, vedere [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).  Per un esempio in cui viene mostrato come aggiungere un'animazione all'opacità di un elemento, vedere [Animare l'opacità di un elemento o un pennello](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-the-opacity-of-an-element-or-brush.md).