---
title: "Procedura: aggiungere un&#39;animazione alle dimensioni di un oggetto FrameworkElement | Microsoft Docs"
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
  - "animazione, FrameworkElement (dimensione)"
  - "FrameworkElement, animazione della dimensione"
ms.assetid: d4cd5a13-c20d-4a6f-a2ba-14f2c9ce4cef
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: aggiungere un&#39;animazione alle dimensioni di un oggetto FrameworkElement
Per animare le dimensioni di un oggetto <xref:System.Windows.FrameworkElement>, è possibile aggiungere un'animazione alle proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> oppure utilizzare un oggetto <xref:System.Windows.Media.ScaleTransform> animato.  
  
 Nell'esempio seguente, le dimensioni di due pulsanti sono state animate utilizzando queste due procedure.  Un pulsante viene ridimensionato aggiungendo un'animazione alla proprietà <xref:System.Windows.FrameworkElement.Width%2A>, mentre l'altro viene ridimensionato aggiungendo l'animazione a un oggetto <xref:System.Windows.Media.ScaleTransform> applicato alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A>.  Ciascun pulsante contiene del testo.  Inizialmente, il testo visualizzato è uguale in entrambi pulsanti, ma quando questi vengono ridimensionati, il testo del secondo pulsante viene distorto.  
  
## Esempio  
 [!code-xml[transformanimations_snip#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/transformanimations_snip/XAML/AnimatingSizeExample.xaml#1)]  
  
 Quando si trasforma un elemento, vengono modificati l'intero elemento e il relativo contenuto.  Quando si altera direttamente la dimensione di un elemento, come nel caso del primo pulsante, il contenuto dell'elemento non viene ridimensionato, a meno che la dimensione e la posizione non dipendano dalle dimensioni dell'elemento padre.  
  
 L'animazione delle dimensioni di un elemento tramite l'applicazione di una trasformazione animata alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> produce risultati migliori rispetto all'animazione diretta delle proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A>, in quanto la proprietà <xref:System.Windows.UIElement.RenderTransform%2A> non attiva un passaggio del layout.  
  
 Per ulteriori informazioni sull'animazione di proprietà, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  Per ulteriori informazioni sulle trasformazioni, vedere [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md).