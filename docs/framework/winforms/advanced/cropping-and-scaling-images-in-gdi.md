---
title: "Ritaglio e ridimensionamento di immagini in GDI+ | Microsoft Docs"
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
  - "compressione di dati, immagini"
  - "GDI+, ritaglio di immagini"
  - "GDI+, ridimensionamento delle immagini"
  - "immagini [Windows Form], compressione"
  - "immagini [Windows Form], ritaglio"
  - "immagini [Windows Form], espansione"
  - "immagini [Windows Form], adattamento"
  - "rettangoli, destinazione"
  - "rettangoli, origine"
ms.assetid: ad5daf26-005f-45bc-a2af-e0e97777a21a
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Ritaglio e ridimensionamento di immagini in GDI+
È possibile utilizzare il metodo <xref:System.Drawing.Graphics.DrawImage%2A> della classe <xref:System.Drawing.Graphics> per tracciare e posizionare immagini vettoriali e immagini raster.  <xref:System.Drawing.Graphics.DrawImage%2A> è un metodo di overload, quindi è possibile fornire argomenti a tale metodo in svariati modi.  
  
## Variazioni del metodo DrawImage  
 Una variazione del metodo <xref:System.Drawing.Graphics.DrawImage%2A> riceve un oggetto <xref:System.Drawing.Bitmap> e un oggetto <xref:System.Drawing.Rectangle>.  Il rettangolo consente di specificare la destinazione per l'operazione di disegno, ovvero di specificare il rettangolo in cui verrà tracciata l'immagine.  Se le dimensioni del rettangolo di destinazione non corrispondono alle dimensioni dell'immagine originale, tale immagine verrà ridimensionata e adattata al rettangolo di destinazione.  Nell'esempio seguente viene illustrato come disegnare la stessa immagine tre volte: una volta senza ridimensionamento, una volta con espansione e una volta con compressione.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#31)]  
  
 Di seguito vengono mostrate le tre immagini.  
  
 ![Ridimensionamento](../../../../docs/framework/winforms/advanced/media/aboutgdip03-art06.png "AboutGdip03\_Art06")  
  
 In alcune variazioni del metodo <xref:System.Drawing.Graphics.DrawImage%2A> oltre al parametro relativo al rettangolo di destinazione è disponibile anche il parametro relativo al rettangolo di origine.  Il parametro relativo al rettangolo di origine consente di specificare la porzione dell'immagine originale da tracciare.  Il rettangolo di destinazione consente di specificare il rettangolo in cui la porzione dell'immagine verrà tracciata.  Se le dimensioni del rettangolo di destinazione non corrispondono alle dimensioni del rettangolo di origine, l'immagine verrà ridimensionata e adattata al rettangolo di destinazione.  
  
 Nell'esempio di codice che segue viene illustrato come costruire un oggetto <xref:System.Drawing.Bitmap> dal file Runner.jpg.  L'intera immagine viene tracciata senza ridimensionamento nella posizione \(0, 0\).  Una porzione ridotta dell'immagine viene quindi tracciata due volte: una volta con riduzione e una volta con espansione.  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#32)]  
  
 Di seguito vengono mostrate l'immagine non ridimensionata e le porzioni di immagine ridotte ed espanse.  
  
 ![Ritaglio e ridimensionamento](../../../../docs/framework/winforms/advanced/media/aboutgdip03-art07.png "AboutGdip03\_Art07")  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)