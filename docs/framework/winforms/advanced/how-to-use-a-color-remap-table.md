---
title: "Procedura: utilizzare una tabella di riassociazione cromatica | Microsoft Docs"
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
  - "tabelle di rimappatura dei colori, utilizzo"
  - "tabelle del colore, rimappatura dei colori"
  - "colori personalizzati, creazione con tabelle di rimappatura dei colori"
ms.assetid: 977df1ce-8665-42d4-9fb1-ef7f0ff63419
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: utilizzare una tabella di riassociazione cromatica
La riassociazione è il processo di conversione dei colori in un'immagine in base a una tabella di riassociazione cromatica.  Tale tabella è una matrice di oggetti <xref:System.Drawing.Imaging.ColorMap>.  Ogni oggetto <xref:System.Drawing.Imaging.ColorMap> contenuto nella matrice dispone di una proprietà <xref:System.Drawing.Imaging.ColorMap.OldColor%2A> e di una proprietà <xref:System.Drawing.Imaging.ColorMap.NewColor%2A>.  
  
 Quando si disegna un'immagine con [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], ciascun pixel dell'immagine viene confrontato con la matrice dei colori precedenti.  Se il colore di un pixel corrisponde a uno dei colori precedenti al pixel viene applicato il nuovo colore corrispondente.  I colori sono modificati solo a scopo di rendering; i valori cromatici veri e propri dell'immagine, memorizzati in un oggetto <xref:System.Drawing.Image> o <xref:System.Drawing.Bitmap>, non vengono modificati.  
  
 Per disegnare un'immagine riassociata, inizializzare una matrice di oggetti <xref:System.Drawing.Imaging.ColorMap>.  Passare la matrice al metodo <xref:System.Drawing.Imaging.ImageAttributes.SetRemapTable%2A> di un oggetto <xref:System.Drawing.Imaging.ImageAttributes>, quindi passare l'oggetto <xref:System.Drawing.Imaging.ImageAttributes> al metodo <xref:System.Drawing.Graphics.DrawImage%2A> di un oggetto <xref:System.Drawing.Graphics>.  
  
## Esempio  
 Nell'esempio che segue viene creato un oggetto <xref:System.Drawing.Image> dal file RemapInput.bmp.  Nel codice viene creata una tabella di riassociazione cromatica costituita da un unico oggetto <xref:System.Drawing.Imaging.ColorMap>.  La proprietà <xref:System.Drawing.Imaging.ColorMap.OldColor%2A> dell'oggetto `ColorRemap`  è il rosso e la proprietà <xref:System.Drawing.Imaging.ColorMap.NewColor%2A> è il blu.  L'immagine viene disegnata una volta con e una volta senza riassociazione.  Tramite il processo di riassociazione tutti i pixel rossi vengono cambiati in blu.  
  
 Nell'illustrazione che segue si mostra l'immagine originale a sinistra e l'immagine riassociata a destra.  
  
 [!code-csharp[System.Drawing.RecoloringImages#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.RecoloringImages#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#31)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Ricolorazione di immagini](../../../../docs/framework/winforms/advanced/recoloring-images.md)   
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)