---
title: "Procedura: riempire una forma con una trama basata su un&#39;immagine | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "bitmap [Windows Form], utilizzo di trame"
  - "immagini [Windows Form], utilizzo con pennelli"
  - "forme, riempimento con immagini"
ms.assetid: 508da5a6-2433-4d2b-9680-eaeae4e96e3b
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: riempire una forma con una trama basata su un&#39;immagine
È possibile riempire una forma chiusa con una trama utilizzando le classi <xref:System.Drawing.Image> e <xref:System.Drawing.TextureBrush>.  
  
## Esempio  
 Nell'esempio riportato di seguito si riempie un'ellisse con un'immagine.  Il codice costruisce un oggetto <xref:System.Drawing.Image>, quindi passa l'indirizzo di tale oggetto <xref:System.Drawing.Image> come argomento al costruttore <xref:System.Drawing.TextureBrush.%23ctor%2A>.  Con la terza istruzione vengono adatta le proporzioni dell'immagine, mentre con la quarta si riempie l'ellisse con copie ripetute dell'immagine riproporzionata.  
  
 Nel codice seguente la proprietà <xref:System.Drawing.TextureBrush.Transform%2A> contiene la trasformazione applicata all'immagine prima che venga disegnata.  Si suppone che l'immagine originale abbia una larghezza di 640 pixel e un'altezza di 480 pixel.  Con la trasformazione l'immagine viene ridotta a 75×75 impostando i valori di scala orizzontali e verticali.  
  
> [!NOTE]
>  Nell'esempio seguente le dimensioni dell'immagine sono pari a 75×75 e quelle dell'ellisse sono pari a 150×250\-  Poiché l'immagine è più piccola dell'ellisse da riempire, viene affiancata più volte nell'ellisse.  L'affiancamento consiste nel ripetere l'immagine in orizzontale e in verticale fino al limite della forma.  Per ulteriori informazioni sull'affiancamento, vedere [Procedura: riempire una forma con immagini affiancate](../../../../docs/framework/winforms/advanced/how-to-tile-a-shape-with-an-image.md).  
  
 [!code-csharp[System.Drawing.UsingABrush#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingABrush#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#21)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Utilizzo di un oggetto Brush per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)