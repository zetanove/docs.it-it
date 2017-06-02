---
title: "Procedura: utilizzare l&#39;elemento Image | Microsoft Docs"
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
  - "BitmapImage (classe)"
  - "classi, BitmapImage"
  - "controlli, Immagine"
  - "Image (controllo)"
  - "rendering di immagini"
ms.assetid: 5b92e74b-1b56-4756-ac64-d5e9e08d9854
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: utilizzare l&#39;elemento Image
In questo esempio viene illustrato come includere immagini in un'applicazione utilizzando l'elemento <xref:System.Windows.Controls.Image>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come eseguire il rendering di un'immagine con una larghezza di 200 pixel.  In questo esempio [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], per definire l’immagine vengono utilizzate la sintassi degli attributi e la sintassi di tag di proprietà.  Per ulteriori informazioni sulla sintassi degli attributi e sulla sintassi delle proprietà, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  <xref:System.Windows.Media.Imaging.BitmapImage> viene utilizzato per definire i dati di origine dell'immagine e viene definito in modo esplicito per l'esempio della sintassi di tag di proprietà.  Inoltre, <xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelWidth%2A> di <xref:System.Windows.Media.Imaging.BitmapImage> viene impostato sulla stessa larghezza di <xref:System.Windows.FrameworkElement.Width%2A> di <xref:System.Windows.Controls.Image>.  Questa operazione viene eseguita per assicurare che la quantità minima di memoria vien utilizzata per eseguire il rendering dell'immagine.  
  
> [!NOTE]
>  In generale, se si desidera specificare le dimensioni di un'immagine sottoposta a rendering, specificare solo <xref:System.Windows.FrameworkElement.Width%2A> o <xref:System.Windows.FrameworkElement.Height%2A>, ma non entrambi.  Se si specifica solo uno di questi oggetti, le [proporzioni](GTMT) dell'immagine vengono mantenute.  In caso contrario, l'immagine potrebbe apparire inaspettatamente allungata o deformata.  Per controllare il comportamento di adattamento dell'immagine, utilizzare le proprietà <xref:System.Windows.Controls.Image.Stretch%2A> e <xref:System.Windows.Controls.Image.StretchDirection%2A>.  
  
> [!NOTE]
>  Quando si specificano le dimensione di un'immagine con <xref:System.Windows.FrameworkElement.Width%2A> o <xref:System.Windows.FrameworkElement.Height%2A>, è anche necessario impostare <xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelWidth%2A> o <xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelHeight%2A> rispettivamente sulle stesse dimensioni.  
  
 La proprietà <xref:System.Windows.Controls.Image.Stretch%2A> determina il modo in cui l’origine dell’immagine viene adattata per riempire l’elemento immagine.  Per ulteriori informazioni, vedere l'enumerazione <xref:System.Windows.Media.Stretch>.  
  
 [!code-xml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come eseguire il rendering di un'immagine con una larghezza di 200 pixel mediante codice.  
  
> [!NOTE]
>  L’impostazione delle proprietà <xref:System.Windows.Media.Imaging.BitmapImage> deve essere eseguita all'interno di un blocco <xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A> e <xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A>.  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
## Vedere anche  
 [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)