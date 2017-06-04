---
title: "Procedura: animare un controllo Popup | Microsoft Docs"
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
  - "animazione, Popup (controlli)"
  - "Popup (controllo), animazione"
ms.assetid: acaa2a0a-6137-4efd-9cd1-75ece222e390
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: animare un controllo Popup
In questo esempio vengono mostrati due metodi per animare un controllo <xref:System.Windows.Controls.Primitives.Popup>.  
  
## Esempio  
 Nell'esempio seguente, la proprietà <xref:System.Windows.Controls.Primitives.PopupAnimation> viene impostata su un valore <xref:System.Windows.Controls.Primitives.PopupAnimation>, che determina lo scorrimento del controllo <xref:System.Windows.Controls.Primitives.Popup> nel momento in cui viene visualizzato.  
  
 Per ruotare il controllo <xref:System.Windows.Controls.Primitives.Popup>, nell'esempio viene assegnato un oggetto <xref:System.Windows.Media.RotateTransform> alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> relativa all'oggetto <xref:System.Windows.Controls.Canvas>, ovvero l'elemento figlio di <xref:System.Windows.Controls.Primitives.Popup>.  
  
 Affinché la trasformazione sia eseguita correttamente, la proprietà <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> dell'esempio deve essere impostata su `true`.  Inoltre, l'oggetto <xref:System.Windows.FrameworkElement.Margin%2A> applicato a <xref:System.Windows.Controls.Canvas> deve specificare uno spazio sufficiente per la rotazione di <xref:System.Windows.Controls.Primitives.Popup>.  
  
 [!code-xml[AnimatedPopup#RotateTransform2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimatedPopup/CS/Window1.xaml#rotatetransform2)]  
  
 Nell'esempio seguente viene mostrato come un evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click>, che si verifica quando si fa clic su un oggetto <xref:System.Windows.Controls.Button>, attivi l'oggetto <xref:System.Windows.Media.Animation.Storyboard> che avvia l'animazione.  
  
 [!code-xml[AnimatedPopup#RotateTransform1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimatedPopup/CS/Window1.xaml#rotatetransform1)]  
  
## Vedere anche  
 <xref:System.Windows.UIElement.RenderTransform%2A>   
 <xref:System.Windows.Controls.Primitives.BulletDecorator>   
 <xref:System.Windows.Media.RotateTransform>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 <xref:System.Windows.Controls.Primitives.Popup>   
 [Procedure relative](../../../../docs/framework/wpf/controls/popup-how-to-topics.md)   
 [Cenni preliminari sul controllo Popup](../../../../docs/framework/wpf/controls/popup-overview.md)