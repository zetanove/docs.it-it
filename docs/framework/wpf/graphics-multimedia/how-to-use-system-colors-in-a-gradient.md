---
title: "Procedura: utilizzare i colori di sistema in una sfumatura | Microsoft Docs"
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
  - "sfumature, colori di sistema"
  - "colori di sistema nelle sfumature"
ms.assetid: 11942e7e-6300-4b50-8ed1-f50e8d20e7d2
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: utilizzare i colori di sistema in una sfumatura
Per utilizzare un colore di sistema in una sfumatura, vengono utilizzate le proprietà statiche *\<ColoreSistema\>*Color e *\<ColoreSistema\>*ColorKey della classe <xref:System.Windows.SystemColors> per ottenere un riferimento al colore, dove *\<ColoreSistema\>* è il nome del colore di sistema desiderato.  Utilizzare le proprietà *\<ColoreSistema\>*ColorKey quando si desidera creare un riferimento dinamico che viene automaticamente aggiornato quando viene modificato il tema del sistema.  In caso contrario, utilizzare le proprietà *\<ColoreSistema\>*Color.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono utilizzate risorse di colore di sistema dinamiche per creare una sfumatura.  
  
 [!code-xml[brushsamples_snip#GraphicsMMDynamicSystemColorGradientExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemColorExample.xaml#graphicsmmdynamicsystemcolorgradientexamplewholepage)]  
  
 Nell'esempio successivo vengono utilizzate risorse di colore di sistema statiche per creare una sfumatura.  
  
 [!code-xml[brushsamples_snip#GraphicsMMStaticSystemColorGradientExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemColorExample.xaml#graphicsmmstaticsystemcolorgradientexamplewholepage)]  
  
## Vedere anche  
 <xref:System.Windows.SystemColors>   
 [Disegnare un'area con un pennello di sistema](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)