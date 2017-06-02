---
title: "Procedura: disegnare un&#39;area con un colore a tinta unita | Microsoft Docs"
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
  - "pennelli, disegno con tinte unite"
  - "disegno, tinte unite"
  - "tinte unite, disegno"
ms.assetid: 5d27d8a7-4bd7-4063-bdf3-2c5c0f19f9d3
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: disegnare un&#39;area con un colore a tinta unita
Per disegnare un'area con un colore a tinta unita è possibile utilizzare un pennello di sistema predefinito, ad esempio <xref:System.Windows.Media.Brushes.Red%2A> o <xref:System.Windows.Media.Brushes.Blue%2A>, oppure è possibile creare un nuovo oggetto <xref:System.Windows.Media.SolidColorBrush> e descrivere la relativa proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> utilizzando valori alfa, rossi, verdi e blu.  In XAML, è inoltre possibile disegnare un'area con un colore a tinta unita utilizzando la notazione esadecimale.  
  
 Negli esempi riportati di seguito viene utilizzata ognuna di queste tecniche per disegnare un oggetto <xref:System.Windows.Shapes.Rectangle> blu.  
  
## Esempio  
 **Utilizzo di un pennello predefinito**  
  
 Nell'esempio riportato di seguito viene utilizzato il pennello predefinito <xref:System.Windows.Media.Brushes.Blue%2A> per disegnare un rettangolo blu.  
  
 [!code-xml[brushsamples_snip#_graphicsmm_PredefinedBrush1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_predefinedbrush1)]  
  
 [!code-csharp[brushsamples_procedural_snip#_graphicsmm_PredefinedBrush1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/SolidColorBrushExample.cs#_graphicsmm_predefinedbrush1)]  
  
 **Utilizzo della notazione esadecimale**  
  
 Nell’esempio successivo viene utilizzata la notazione esadecimale a 8 cifre per disegnare un rettangolo blu.  
  
 [!code-xml[brushsamples_snip#_graphicsmm_HexNotation8Digit1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_hexnotation8digit1)]  
  
 **Utilizzo dei valori ARGB**  
  
 Nell’esempio successivo viene creato un oggetto <xref:System.Windows.Media.SolidColorBrush> e viene descritta la relativa proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> utilizzando i valori ARGB per il colore blu.  
  
 [!code-xml[brushsamples_snip#_graphicsmm_RgbNotation1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/SolidColorBrushExample.xaml#_graphicsmm_rgbnotation1)]  
  
 [!code-csharp[brushsamples_procedural_snip#_graphicsmm_RgbNotation1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/SolidColorBrushExample.cs#_graphicsmm_rgbnotation1)]  
  
 Per altre modalità di descrizione del colore, vedere la struttura <xref:System.Windows.Media.Color>.  
  
 **Argomenti correlati**  
  
 Per ulteriori informazioni su <xref:System.Windows.Media.SolidColorBrush> e per esempi aggiuntivi, vedere i Cenni preliminari su [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).  
  
 Questo esempio di codice fa parte di un esempio più esaustivo fornito per la classe <xref:System.Windows.Media.SolidColorBrush>.  Per l'esempio completo, vedere [Esempio Brush](http://go.microsoft.com/fwlink/?LinkID=159973) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Brushes>