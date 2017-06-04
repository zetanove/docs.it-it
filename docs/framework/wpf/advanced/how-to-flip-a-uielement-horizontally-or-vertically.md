---
title: "Procedura: capovolgere un oggetto UIElement orizzontalmente o verticalmente | Microsoft Docs"
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
  - "capovolgimento di UIElement"
  - "UIElement, capovolgimento"
ms.assetid: 02c6730f-65c0-40d5-a553-4cb663721882
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: capovolgere un oggetto UIElement orizzontalmente o verticalmente
In questo esempio viene illustrato come utilizzare <xref:System.Windows.Media.ScaleTransform> per capovolgere <xref:System.Windows.UIElement> orizzontalmente o verticalmente.  In questo esempio un controllo <xref:System.Windows.Controls.Button> \(un tipo di <xref:System.Windows.UIElement>\) viene capovolto mediante l'applicazione di <xref:System.Windows.Media.ScaleTransform> alla relativa proprietà <xref:System.Windows.UIElement.RenderTransform%2A>.  
  
## Esempio  
 Nella figura riportata di seguito viene illustrato il pulsante da capovolgere.  
  
 ![Pulsante senza trasformazioni](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonflipbeforeflip.png "graphicsmm\_buttonflipbeforeflip")  
UIElement da capovolgere  
  
 Di seguito viene illustrato il codice tramite cui viene creato il pulsante.  
  
 [!code-xml[Transforms_snip#GraphicsMMButtonWithoutFlip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmbuttonwithoutflip)]  
  
## Esempio  
 Per capovolgere il pulsante orizzontalmente, creare <xref:System.Windows.Media.ScaleTransform> e impostarne la proprietà <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> su \-1.  Applicare <xref:System.Windows.Media.ScaleTransform> alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> del pulsante.  
  
 [!code-xml[Transforms_snip#GraphicsMMFlipButtonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample1)]  
  
 ![Pulsante capovolto orizzontalmente rispetto a &#40;0,0&#41;](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonfliphorizontalflip-displaced.png "graphicsmm\_buttonfliphorizontalflip\_displaced")  
Pulsante dopo l'applicazione di ScaleTransform  
  
## Esempio  
 Nella figura precedente si nota che il pulsante è stato capovolto, ma anche spostato.  Questo risultato è dovuto al fatto che il pulsante è stato capovolto dall'angolo superiore sinistro.  Per capovolgere il pulsante senza spostarlo, applicare <xref:System.Windows.Media.ScaleTransform> al centro, non all'angolo.  Un modo semplice per applicare <xref:System.Windows.Media.ScaleTransform> al centro del pulsante consiste nell'impostare la proprietà <xref:System.Windows.UIElement.RenderTransformOrigin%2A> del pulsante su 0.5, 0.5.  
  
 [!code-xml[Transforms_snip#GraphicsMMFlipButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample2)]  
  
 ![Pulsante capovolto orizzontalmente rispetto al proprio centro](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonfliphorizontalflip-inplace.png "graphicsmm\_buttonfliphorizontalflip\_inplace")  
Pulsante con proprietà RenderTransformOrigin di 0.5, 0.5  
  
## Esempio  
 Per capovolgere il pulsante verticalmente, impostare la proprietà <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> dell'oggetto <xref:System.Windows.Media.ScaleTransform>, anziché la proprietà <xref:System.Windows.Media.ScaleTransform.ScaleX%2A>.  
  
 [!code-xml[Transforms_snip#GraphicsMMVerticalFlipButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmverticalflipbuttonexample2)]  
  
 ![Pulsante capovolto verticalmente rispetto al proprio centro](../../../../docs/framework/wpf/advanced/media/graphicsmm-buttonflipverticalflip-inplace.png "graphicsmm\_buttonflipverticalflip\_inplace")  
Pulsante capovolto verticalmente  
  
## Vedere anche  
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)