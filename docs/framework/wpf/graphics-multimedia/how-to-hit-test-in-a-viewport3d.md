---
title: "Procedura: eseguire un hit test in un oggetto Viewport3D | Microsoft Docs"
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
  - "3D (elementi visivi), hit-testing"
  - "hit test, per elementi visivi 3D"
  - "Viewport3D"
ms.assetid: 42bfbd99-c7c6-43f1-940b-90448faa412e
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: eseguire un hit test in un oggetto Viewport3D
In questo esempio viene illustrato come eseguire un hit test per elementi visivi tridimensionali in un oggetto <xref:System.Windows.Controls.Viewport3D>.  
  
 Poiché <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> restituisce informazioni bidimensionali e tridimensionali, è possibile scorrere i risultati del test per leggere solo quelli tridimensionali.  
  
 [!code-csharp[HitTest3D#HitTest3D3DN4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml.cs#hittest3d3dn4)]
 [!code-vb[HitTest3D#HitTest3D3DN4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HitTest3D/visualbasic/window1.xaml.vb#hittest3d3dn4)]  
  
 Nel codice <xref:System.Windows.Media.HitTestResultBehavior> determina la modalità di elaborazione dei risultati dell'hit test.  `UpdateResultInfo` e `UpdateMaterial` sono metodi definiti localmente.  
  
 [!code-csharp[HitTest3D#HitTest3D3DN5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml.cs#hittest3d3dn5)]
 [!code-vb[HitTest3D#HitTest3D3DN5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HitTest3D/visualbasic/window1.xaml.vb#hittest3d3dn5)]  
  
## Vedere anche  
 [Esempio di hit testing 3D](http://go.microsoft.com/fwlink/?LinkID=159959)