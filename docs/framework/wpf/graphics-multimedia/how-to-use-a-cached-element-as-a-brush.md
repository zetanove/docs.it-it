---
title: "Procedura: utilizzare un elemento memorizzato nella cache come pennello | Microsoft Docs"
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
  - "BitmapCache [WPF], utilizzo"
  - "BitmapCacheBrush [WPF], utilizzo"
  - "elemento memorizzato nella cache [WPF], utilizzo come pennello"
  - "CacheMode [WPF], utilizzo"
ms.assetid: d36e944a-866e-4baf-98c4-fd6a75f6fdd0
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: utilizzare un elemento memorizzato nella cache come pennello
Utilizzare la classe <xref:System.Windows.Media.BitmapCacheBrush> per riutilizzare in modo efficiente un elemento memorizzato nella cache.  Per memorizzare un elemento nella cache, creare una nuova istanza della classe <xref:System.Windows.Media.BitmapCache> e assegnarla alla proprietà <xref:System.Windows.UIElement.CacheMode%2A> dell'elemento.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come riutilizzare un elemento memorizzato nella cache.  L'elemento memorizzato nella cache è un controllo <xref:System.Windows.Controls.Image> in cui è visualizzata un'immagine di grandi dimensioni.  Il controllo <xref:System.Windows.Controls.Image> viene memorizzato nella cache come bitmap utilizzando la classe <xref:System.Windows.Media.BitmapCache> e la cache viene riutilizzata assegnandola a un oggetto <xref:System.Windows.Media.BitmapCacheBrush>.  Il pennello viene assegnato allo sfondo di venticinque pulsanti per illustrare come riutilizzarlo in modo efficiente.  
  
 [!code-xml[System.Windows.Media.BitmapCacheBrush#_BitmapCacheBrushXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcachebrush/cs/window1.xaml#_bitmapcachebrushxaml)]  
  
## Vedere anche  
 <xref:System.Windows.Media.BitmapCache>   
 <xref:System.Windows.Media.BitmapCacheBrush>   
 <xref:System.Windows.UIElement.CacheMode%2A>   
 [Procedura: migliorare le prestazioni di rendering memorizzando nella cache un elemento](../../../../docs/framework/wpf/graphics-multimedia/how-to-improve-rendering-performance-by-caching-an-element.md)