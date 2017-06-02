---
title: "Procedura: disegnare una bitmap esistente sullo schermo | Microsoft Docs"
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
  - "bitmap [Windows Form], visualizzazione in Windows Form"
  - "bitmap [Windows Form], caricamento in applicazioni di Windows Form"
  - "immagini [Windows Form], visualizzazione su Windows Form"
ms.assetid: 5bc558d7-b326-4050-a834-b8600da0de95
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: disegnare una bitmap esistente sullo schermo
È possibile disegnare facilmente un'immagine esistente sullo schermo.  Per prima cosa, è necessario creare un oggetto <xref:System.Drawing.Bitmap> utilizzando il costruttore di bitmap che accetta un nome file, <xref:System.Drawing.Bitmap.%23ctor%28System.String%29>.  Questo costruttore accetta immagini con diversi formati di file differenti, inclusi BMP, GIF, JPEG, PNG e TIFF.  Una volta creato l'oggetto <xref:System.Drawing.Bitmap>, passare tale oggetto <xref:System.Drawing.Bitmap> al metodo <xref:System.Drawing.Graphics.DrawImage%2A> di un oggetto <xref:System.Drawing.Graphics>.  
  
## Esempio  
 Nell'esempio seguente viene creato un oggetto <xref:System.Drawing.Bitmap> a partire da un file JPEG, quindi viene tracciato l'oggetto Bitmap con l'angolo superiore sinistro in corrispondenza del punto \(60, 10\).  
  
 Nell'illustrazione che segue è visibile l'immagine bitmap disegnata nella posizione specificata.  
  
 ![Posizione dell'immagine](../../../../docs/framework/winforms/advanced/media/csimageposition1.png "csimageposition1")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.WorkingWithImages#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#21)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)