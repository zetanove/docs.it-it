---
title: "Cenni preliminari sulle propriet&#224; di trasformazione Brush | Microsoft Docs"
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
  - "pennelli, proprietà di trasformazione"
  - "proprietà, trasformazione"
  - "proprietà di trasformazione dei pennelli"
ms.assetid: 8b9bfc09-12fd-4cd5-b445-99949f27bc39
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sulle propriet&#224; di trasformazione Brush
La classe Brush fornisce due proprietà di trasformazione: <xref:System.Windows.Media.Brush.Transform%2A> e <xref:System.Windows.Media.Brush.RelativeTransform%2A>.  Le proprietà consentono di ruotare, ridimensionare, inclinare e traslare il contenuto di un pennello.  Nel presente argomento vengono descritte le differenze tra queste due proprietà e vengono forniti degli esempi di utilizzo.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## Prerequisiti  
 Per comprendere questo argomento, è necessario capire le funzionalità del pennello che viene trasformato.  Per <xref:System.Windows.Media.LinearGradientBrush> e <xref:System.Windows.Media.RadialGradientBrush>, vedere [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).  Per <xref:System.Windows.Media.ImageBrush>, <xref:System.Windows.Media.DrawingBrush> o <xref:System.Windows.Media.VisualBrush>, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  È anche necessario avere familiarità con le trasformazioni 2D descritte in [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md).  
  
<a name="transformversusrelativetransform"></a>   
## Differenze tra le proprietà Transform e RelativeTransform  
 Quando viene applicata una trasformazione alla proprietà <xref:System.Windows.Media.Brush.Transform%2A> di un pennello, è necessario conoscere le dimensioni dell'area disegnata se si desidera trasformare il contenuto del pennello intorno al relativo centro.  Si supponga che l'area disegnata sia pari a 200 [Device Independent Pixel](GTMT) di larghezza e 150 di altezza.  Se si utilizzasse <xref:System.Windows.Media.RotateTransform> per ruotare l'output del pennello di 45 gradi intorno al relativo centro, si assegnerebbe a <xref:System.Windows.Media.RotateTransform> un <xref:System.Windows.Media.RotateTransform.CenterX%2A> di 100 e un <xref:System.Windows.Media.RotateTransform.CenterY%2A> di 75.  
  
 Quando viene applicata una trasformazione alla proprietà <xref:System.Windows.Media.Brush.RelativeTransform%2A> di un pennello, tale trasformazione viene applicata al pennello prima che venga eseguito il mapping del relativo output all'area disegnata.  Nel seguente elenco viene riportato l'ordine in base al quale il contenuto di un pennello viene elaborato e trasformato.  
  
1.  Elaborare il contenuto del pennello.  Per <xref:System.Windows.Media.GradientBrush>, questo significa stabilire l'area della sfumatura.  Per <xref:System.Windows.Media.TileBrush>, viene eseguito il mapping di <xref:System.Windows.Media.TileBrush.Viewbox%2A> a <xref:System.Windows.Media.TileBrush.Viewport%2A>.  Questo diventa l'output del pennello.  
  
2.  Proiettare l'output del pennello sul rettangolo di trasformazione 1 x 1.  
  
3.  Applicare la proprietà <xref:System.Windows.Media.Brush.RelativeTransform%2A> del pennello, se disponibile.  
  
4.  Proiettare l'output trasformato sull'area da disegnare.  
  
5.  Applicare la proprietà <xref:System.Windows.Media.Transform> del pennello, se disponibile.  
  
 Poiché <xref:System.Windows.Media.Brush.RelativeTransform%2A> viene applicato mentre viene eseguito il mapping dell'output del pennello a un rettangolo 1 x 1, il centro della trasformazione e i valori di offset sembrano essere relativi.  Ad esempio, se si utilizzasse <xref:System.Windows.Media.RotateTransform> per ruotare l'output del pennello di 45 gradi intorno al relativo centro, si assegnerebbe a <xref:System.Windows.Media.RotateTransform> un <xref:System.Windows.Media.RotateTransform.CenterX%2A> di 0,5 e un <xref:System.Windows.Media.RotateTransform.CenterY%2A> di 0,5.  
  
 Nella figura riportata di seguito viene illustrato l'output di numerosi pennelli ruotati di 45 gradi utilizzando le proprietà <xref:System.Windows.Media.Brush.RelativeTransform%2A> e <xref:System.Windows.Media.Brush.Transform%2A>.  
  
 ![Proprietà RelativeTransform e Transform](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brushrelativetransform-transform-small.png "graphicsmm\_brushrelativetransform\_transform\_small")  
  
<a name="relativetransformandtilebrush"></a>   
## Utilizzo di RelativeTransform con TileBrush  
 Poiché i pennelli tessera sono più complessi di altri pennelli, l'applicazione di <xref:System.Windows.Media.Brush.RelativeTransform%2A> a uno di questi pennelli potrebbe produrre risultati imprevisti.  Ad esempio, analizzare la seguente immagine.  
  
 ![Immagine di origine](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-1-original-image.png "graphicsmm\_reltransform\_1\_original\_image")  
  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.ImageBrush> per disegnare un'area rettangolare con l'immagine precedente.  In tal modo, <xref:System.Windows.Media.RotateTransform> viene applicato alla proprietà <xref:System.Windows.Media.Brush.RelativeTransform%2A> dell'oggetto <xref:System.Windows.Media.ImageBrush> e la relativa proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> viene impostata su <xref:System.Windows.Media.Stretch> consentendo di conservare le proporzioni dell'immagine quando viene estesa per riempire completamente il rettangolo.  
  
 [!code-xml[BrushOverviewExamples_snip#GraphicsMMRelativeTransformExample2Inline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/RelativeTransformIllustration.xaml#graphicsmmrelativetransformexample2inline)]  
  
 Questo esempio produce il seguente output:  
  
 ![Output trasformato](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-6-output.png "graphicsmm\_reltransform\_6\_output")  
  
 Si noti che l'immagine è distorta anche se la proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> del pennello era impostata su <xref:System.Windows.Media.Stretch>.  Ciò è dovuto al fatto che la trasformazione relativa viene applicata successivamente al mapping di <xref:System.Windows.Media.TileBrush.Viewbox%2A> al relativo <xref:System.Windows.Media.TileBrush.Viewport%2A>.  Nell'elenco riportato di seguito vengono descritti tutti i passaggi del processo.  
  
1.  Proiettare il contenuto del pennello \(<xref:System.Windows.Media.TileBrush.Viewbox%2A>\) sulla relativa tessera di base \(<xref:System.Windows.Media.TileBrush.Viewport%2A>\) utilizzando l'impostazione <xref:System.Windows.Media.TileBrush.Stretch%2A> del pennello.  
  
     ![Allungare l'oggetto Viewbox per adattarlo al viewport](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-2-viewbox-to-viewport.png "graphicsmm\_reltransform\_2\_viewbox\_to\_viewport")  
  
2.  Proiettare la tessera di base sul rettangolo di trasformazione 1 x 1.  
  
     ![Eseguire il mapping del viewport al rettangolo di trasformazione](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-3-output-to-transform.png "graphicsmm\_reltransform\_3\_output\_to\_transform")  
  
3.  Applicare <xref:System.Windows.Media.RotateTransform>.  
  
     ![Applicare la relativa trasformazione](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-4-transform-rotate.png "graphicsmm\_reltransform\_4\_transform\_rotate")  
  
4.  Proiettare la tessera di base trasformata sull'area da disegnare.  
  
     ![Proiettare il pennello trasformato nell'area di output](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-reltransform-5-transform-to-output.png "graphicsmm\_reltransform\_5\_transform\_to\_output")  
  
<a name="rotateexample"></a>   
## Esempio: rotazione di un oggetto ImageBrush di 45 gradi  
 Nell'esempio riportato di seguito <xref:System.Windows.Media.RotateTransform> viene applicato alla proprietà <xref:System.Windows.Media.Brush.RelativeTransform%2A> di <xref:System.Windows.Media.ImageBrush>.  Le proprietà <xref:System.Windows.Media.RotateTransform.CenterX%2A> e <xref:System.Windows.Media.RotateTransform.CenterY%2A> dell'oggetto <xref:System.Windows.Media.RotateTransform> sono entrambe impostate su 0,5, le coordinate relative del punto centrale del contenuto.  Di conseguenza, il contenuto del pennello viene ruotato intorno al relativo centro.  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushrelativetransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushrelativetransformexample)]
 [!code-xml[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushrelativetransformexample)]  
  
 Anche in quest'altro esempio <xref:System.Windows.Media.RotateTransform> viene applicato a <xref:System.Windows.Media.ImageBrush>, ma viene utilizzata la proprietà <xref:System.Windows.Media.Brush.Transform%2A> anziché la proprietà <xref:System.Windows.Media.Brush.RelativeTransform%2A>.  Per ruotare il pennello intorno al relativo centro, è necessario impostare <xref:System.Windows.Media.RotateTransform.CenterX%2A> e <xref:System.Windows.Media.RotateTransform.CenterY%2A> dell'oggetto <xref:System.Windows.Media.RotateTransform> su coordinate assolute.  Poiché il rettangolo disegnato dal pennello è di 175 per 90 pixel, il relativo punto centrale è \(87,5, 45\).  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushtransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushtransformexample)]
 [!code-xml[BrushesIntroduction_snip#ImageBrushTransformExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushtransformexample)]  
  
 Nell'immagine riportata di seguito viene illustrato il pennello senza trasformazioni, con la trasformazione applicata alla proprietà <xref:System.Windows.Media.Brush.RelativeTransform%2A>e con la trasformazione applicata alla proprietà <xref:System.Windows.Media.Brush.Transform%2A>.  
  
 ![Impostazioni RelativeTransform e Transform di Brush](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-transformandrelativetransform.png "wcpsdk\_graphicsmm\_transformandrelativetransform")  
  
 Questo esempio fa parte di un esempio più esaustivo.  Per l'esempio completo, vedere [Esempio Brush](http://go.microsoft.com/fwlink/?LinkID=159973) \(la pagina potrebbe essere in inglese\).  Per ulteriori informazioni sui pennelli, vedere [Cenni preliminari sui pennelli di WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-brushes-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.Brush.Transform%2A>   
 <xref:System.Windows.Media.Brush.RelativeTransform%2A>   
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.Brush>   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)