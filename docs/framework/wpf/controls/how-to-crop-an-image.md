---
title: "Procedura: ritagliare un&#39;immagine | Microsoft Docs"
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
  - "classi, CroppedBitmap"
  - "CroppedBitmap (classe)"
  - "ritaglio di immagini"
  - "immagini, ritaglio"
ms.assetid: c6bba109-c6e7-4cf8-bfe6-9cf8d01bb4fc
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: ritagliare un&#39;immagine
In questo esempio viene mostrato come ritagliare un'immagine utilizzando un oggetto <xref:System.Windows.Media.Imaging.CroppedBitmap>.  
  
 L'oggetto <xref:System.Windows.Media.Imaging.CroppedBitmap> viene utilizzato principalmente quando si codifica una versione ritagliata di un'immagine da salvare in un file.  Per ritagliare un'immagine per la visualizzazione, vedere l'argomento [Create a Clip Region](http://msdn.microsoft.com/it-it/56e4bed6-78d7-4292-b917-d72d0b3e4376).  
  
## Esempio  
 La sintassi [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] seguente definisce le risorse utilizzate all'interno degli esempi forniti di seguito.  
  
 [!code-xml[imageelementexample#CroppedXAML1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml1)]  
  
 Nell'esempio seguente viene creata un'immagine utilizzando un oggetto <xref:System.Windows.Media.Imaging.CroppedBitmap> come origine.  
  
 [!code-xml[imageelementexample#CroppedXAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml2)]  
  
 [!code-csharp[imageelementexample#CroppedCSharp1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml.cs#croppedcsharp1)]
 [!code-vb[imageelementexample#CroppedCSharp1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/CroppedImageExample.xaml.vb#croppedcsharp1)]  
  
 L'oggetto <xref:System.Windows.Media.Imaging.CroppedBitmap> può anche essere utilizzato come origine di un altro oggetto <xref:System.Windows.Media.Imaging.CroppedBitmap>, concatenando il ritaglio.  Notare che l'oggetto <xref:System.Windows.Media.Imaging.CroppedBitmap.SourceRect%2A> utilizza valori relativi alla bitmap ritagliata di origine e non all'immagine iniziale.  
  
 [!code-xml[imageelementexample#CroppedXAML3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml3)]  
  
 [!code-csharp[imageelementexample#CroppedCSharp2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml.cs#croppedcsharp2)]
 [!code-vb[imageelementexample#CroppedCSharp2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/CroppedImageExample.xaml.vb#croppedcsharp2)]  
  
## Vedere anche  
 [Create a Clip Region](http://msdn.microsoft.com/it-it/56e4bed6-78d7-4292-b917-d72d0b3e4376)