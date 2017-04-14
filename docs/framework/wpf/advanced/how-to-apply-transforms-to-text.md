---
title: "Procedura: applicare trasformazioni al testo | Microsoft Docs"
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
  - "testo ruotato"
  - "testo ridimensionato"
  - "testo ombreggiato"
  - "testo inclinato"
  - "trasformazioni nel testo"
  - "testo convertito"
  - "tipografia, testo ruotato"
  - "tipografia, testo ridimensionato"
  - "tipografia, testo ombreggiato"
  - "tipografia, testo inclinato"
  - "tipografia, trasformazioni"
  - "tipografia, testo convertito"
ms.assetid: 0d61678a-4185-4f2a-85c6-c1d020f96fa0
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: applicare trasformazioni al testo
Le trasformazioni possono alternare la visualizzazione del testo nell'applicazione.  Negli esempi riportati di seguito vengono utilizzati tipi diversi di trasformazioni di rendering per modificare la visualizzazione del testo in un controllo <xref:System.Windows.Controls.TextBlock>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato del testo ruotato intorno a un punto specifico del piano x\-y bidimensionale.  
  
 ![Testo ruotato con RotateTransform](../../../../docs/framework/wpf/advanced/media/transformedtext01.png "TransformedText01")  
Esempio di testo ruotato di 90 gradi  
  
 Nell'esempio di codice riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.RotateTransform> per ruotare il testo.  Con la proprietà <xref:System.Windows.Media.RotateTransform.Angle%2A> impostata su 90 l'elemento viene ruotato di 90 gradi in senso orario.  
  
 [!code-xml[TextTransformSample#TextTransformSample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTransformSample/CS/Window1.xaml#texttransformsample1)]  
  
 Nell'esempio riportato di seguito viene illustrata la seconda riga del testo ridimensionata del 150% lungo l'asse x e la terza riga del testo ridimensionata del 150% lungo l'asse y.  
  
 ![Testo ridimensionato con ScaleTransform](../../../../docs/framework/wpf/advanced/media/transformedtext02.png "TransformedText02")  
Esempio di testo ridimensionato  
  
 Nell'esempio di codice riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.ScaleTransform> per ridimensionare il testo rispetto alle dimensioni originali.  
  
 [!code-xml[TextTransformSample#TextTransformSample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTransformSample/CS/Window1.xaml#texttransformsample2)]  
  
> [!NOTE]
>  Il ridimensionamento del testo non è dato dall'aumento delle dimensioni dei caratteri del testo.  Le dimensioni dei caratteri vengono calcolate in modo indipendente per fornire la migliore risoluzione a dimensioni diverse.  Il testo ridimensionato mantiene invece le proporzioni del testo nelle dimensioni originali.  
  
 Nell'esempio riportato di seguito viene illustrato un testo inclinato lungo l'asse x.  
  
 ![Testo inclinato con SkewTransform](../../../../docs/framework/wpf/advanced/media/transformedtext03.png "TransformedText03")  
Esempio di testo inclinato  
  
 Nell'esempio di codice riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.SkewTransform> per inclinare il testo.  L'inclinazione, nota anche come distorsione, è una trasformazione che estende lo spazio delle coordinate in modo non uniforme.  In questo esempio, le due stringhe di testo sono inclinate di \-30° e 30° lungo la coordinata x.  
  
 [!code-xml[TextTransformSample#TextTransformSample3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTransformSample/CS/Window1.xaml#texttransformsample3)]  
  
 Nell'esempio riportato di seguito viene illustrato del testo traslato, o spostato, lungo l'asse x e y.  
  
 ![Offset del testo con TranslateTransform](../../../../docs/framework/wpf/advanced/media/transformedtext04.png "TransformedText04")  
Esempio di testo traslato  
  
 Nell'esempio di codice riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.TranslateTransform> per applicare un offset al testo.  In questo esempio, una copia del testo con un leggero offset sotto il testo primario crea un effetto di ombreggiatura.  
  
 [!code-xml[TextTransformSample#TextTransformSample4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextTransformSample/CS/Window1.xaml#texttransformsample4)]  
  
> [!NOTE]
>  L'oggetto <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> offre un'ampia gamma di funzionalità per ottenere effetti di ombreggiatura.  Per ulteriori informazioni, vedere [Creare un testo con un'ombreggiatura](../../../../docs/framework/wpf/advanced/how-to-create-text-with-a-shadow.md).  
  
## Vedere anche  
 [Applicare animazioni al testo](../../../../docs/framework/wpf/advanced/how-to-apply-animations-to-text.md)