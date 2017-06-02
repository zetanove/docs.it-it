---
title: "Procedura: animare una matrice utilizzando fotogrammi chiave | Microsoft Docs"
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
  - "animazione, Matrix (proprietà con fotogrammi chiave)"
  - "fotogrammi chiave, animazione di proprietà Matrix"
  - "Matrix (proprietà), animazione con fotogrammi chiave"
ms.assetid: b851a4c7-ecb1-420e-9203-83e7afd037fd
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: animare una matrice utilizzando fotogrammi chiave
In questo esempio viene illustrato come animare la proprietà <xref:System.Windows.Media.MatrixTransform.Matrix%2A> di un oggetto <xref:System.Windows.Media.MatrixTransform> utilizzando fotogrammi chiave.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la classe <xref:System.Windows.Media.Animation.MatrixAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.Media.MatrixTransform.Matrix%2A> di un oggetto <xref:System.Windows.Media.MatrixTransform>.  Nell'esempio si utilizza l'oggetto <xref:System.Windows.Media.MatrixTransform> per trasformare l'aspetto e la posizione di un oggetto <xref:System.Windows.Controls.Button>.  
  
 Questa animazione utilizza la classe <xref:System.Windows.Media.Animation.DiscreteMatrixKeyFrame> per creare due fotogrammi chiave mediante i quali effettua le seguenti operazioni:  
  
1.  Animazione del primo oggetto <xref:System.Windows.Media.Matrix> durante i primi 0,2 secondi.  Nell'esempio le proprietà <xref:System.Windows.Media.Matrix.M11%2A> e <xref:System.Windows.Media.Matrix.M12%2A> dell'oggetto <xref:System.Windows.Media.Matrix> vengono modificate.  In seguito a questa modifica il pulsante si allunga e si inclina.  Nell'esempio vengono modificate anche le proprietà <xref:System.Windows.Media.Matrix.OffsetX%2A> e <xref:System.Windows.Media.Matrix.OffsetY%2A> in modo che il pulsante cambi posizione.  
  
2.  Animazione del secondo oggetto <xref:System.Windows.Media.Matrix> a 1,0 secondi.  Il pulsante si sposta in un'altra posizione e non è più inclinato o allungato.  
  
3.  Ripetizione a oltranza dell'animazione.  
  
> [!NOTE]
>  I fotogrammi chiave che derivano dall'oggetto <xref:System.Windows.Media.Animation.DiscreteMatrixKeyFrame> creano passaggi improvvisi tra due valori, per cui l'animazione si muove a scatti.  
  
 [!code-xml[keyframes_snip#MatrixAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/MatrixAnimationUsingKeyFramesExample.xaml#matrixanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.MatrixTransform.Matrix%2A>   
 <xref:System.Windows.Media.MatrixTransform>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)