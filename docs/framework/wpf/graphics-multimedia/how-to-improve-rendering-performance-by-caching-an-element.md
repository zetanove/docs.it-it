---
title: "Procedura: migliorare le prestazioni di rendering memorizzando nella cache un elemento | Microsoft Docs"
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
  - "BitmapCache [WPF], miglioramento delle prestazioni di rendering"
  - "CacheMode [WPF], miglioramento delle prestazioni di rendering"
  - "prestazioni [WPF], memorizzazione di un elemento nella cache"
  - "prestazioni di rendering [WPF], memorizzazione di un elemento nella cache"
  - "UIElement [WPF], memorizzazione nella cache"
ms.assetid: 4739c1fc-60ba-4c46-aba6-f6c1a2688f19
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: migliorare le prestazioni di rendering memorizzando nella cache un elemento
Utilizzare la classe <xref:System.Windows.Media.BitmapCache> per migliorare le prestazioni di rendering di un oggetto <xref:System.Windows.UIElement> complesso.  Per memorizzare un elemento nella cache, creare una nuova istanza della classe <xref:System.Windows.Media.BitmapCache> e assegnarla alla proprietà <xref:System.Windows.UIElement.CacheMode%2A> dell'elemento.  È possibile riutilizzare in modo efficiente un oggetto <xref:System.Windows.Media.BitmapCache> in un oggetto <xref:System.Windows.Media.BitmapCacheBrush>.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come creare un elemento complesso e memorizzarlo nella cache come bitmap. Questa operazione migliora le prestazioni quando l'elemento è animato.  L'elemento è un'area di disegno che contiene geometrie di forma con numerosi vertici.  Un oggetto <xref:System.Windows.Media.BitmapCache> con valori predefiniti è assegnato alla proprietà <xref:System.Windows.UIElement.CacheMode%2A> dell'area di disegno e un'animazione illustra il ridimensionamento uniforme della bitmap memorizzata nella cache.  
  
 [!code-xml[System.Windows.Media.BitmapCache#_BitmapCacheXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/system.windows.media.bitmapcache/cs/window1.xaml#_bitmapcachexaml)]  
  
## Vedere anche  
 <xref:System.Windows.Media.BitmapCache>   
 <xref:System.Windows.Media.BitmapCacheBrush>   
 <xref:System.Windows.UIElement.CacheMode%2A>   
 [Procedura: utilizzare un elemento memorizzato nella cache come pennello](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-a-cached-element-as-a-brush.md)