---
title: "Disegno, posizionamento e duplicazione delle immagini in GDI+ | Microsoft Docs"
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
  - "disegno, immagini"
  - "disegno, immagini raster"
  - "GDI+, duplicazione delle immagini"
  - "GDI+, disegno di immagini"
  - "GDI+, posizionamento delle immagini"
  - "immagini [Windows Form], duplicazione"
  - "immagini [Windows Form], disegno"
  - "immagini [Windows Form], posizionamento"
  - "immagini raster"
ms.assetid: 09f0c07a-19c0-43b4-90a2-862a10545ce8
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Disegno, posizionamento e duplicazione delle immagini in GDI+
È possibile utilizzare la classe <xref:System.Drawing.Bitmap> per caricare e visualizzare immagini raster e utilizzare la classe <xref:System.Drawing.Imaging.Metafile> per caricare e visualizzare immagini vettoriali.  Le classi <xref:System.Drawing.Bitmap> e <xref:System.Drawing.Imaging.Metafile> ereditano dalla classe <xref:System.Drawing.Image>.  Per visualizzare un'immagine vettoriale, sono necessari un'istanza della classe <xref:System.Drawing.Graphics> e <xref:System.Drawing.Imaging.Metafile>.  Per visualizzare un'immagine raster, sono necessari un'istanza della classe <xref:System.Drawing.Graphics> e <xref:System.Drawing.Bitmap>.  L'istanza della classe <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawImage%2A> che riceve <xref:System.Drawing.Imaging.Metafile> o <xref:System.Drawing.Bitmap> come argomento.  
  
## Tipi di file e duplicazione  
 Nell'esempio di codice che segue viene illustrato come costruire un oggetto <xref:System.Drawing.Bitmap> dal file Climber.jpg e visualizzare la bitmap.  Il punto di destinazione per l'angolo superiore sinistro dell'immagine, \(10, 10\), è specificato nel secondo e nel terzo parametro.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#11)]  
  
 Di seguito viene mostrata l'immagine.  
  
 ![Esempio Image](../../../../docs/framework/winforms/advanced/media/aboutgdip03-art04.png "AboutGdip03\_Art04")  
  
 È possibile costruire oggetti <xref:System.Drawing.Bitmap> utilizzando una vasta gamma di formati di file grafici: BMP, GIF, JPEG, EXIF, PNG, TIFF e ICON.  
  
 Nell'esempio di codice che segue viene illustrato come costruire oggetti <xref:System.Drawing.Bitmap> utilizzando svariati tipi di file e visualizzare le bitmap.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#12)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#12)]  
  
 Nella classe <xref:System.Drawing.Bitmap> è disponibile il metodo <xref:System.Drawing.Bitmap.Clone%2A>, che consente la creazione di una copia di un oggetto <xref:System.Drawing.Bitmap> esistente.  Nel metodo <xref:System.Drawing.Bitmap.Clone%2A> è presente un parametro relativo al rettangolo di origine, che consente di specificare la porzione della bitmap originale che si desidera copiare.  Nell'esempio di codice che segue viene illustrato come creare un oggetto <xref:System.Drawing.Bitmap> tramite la duplicazione della metà superiore di un oggetto <xref:System.Drawing.Bitmap> esistente.  Vengono quindi tracciate entrambe le immagini.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#13](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#13)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#13](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#13)]  
  
 Di seguito vengono mostrate le due immagini.  
  
 ![Ritaglio](../../../../docs/framework/winforms/advanced/media/aboutgdip03-art05.png "AboutGdip03\_Art05")  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)