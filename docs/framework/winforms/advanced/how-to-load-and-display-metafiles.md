---
title: "Procedura: caricare e visualizzare metafile | Microsoft Docs"
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
  - "esempi [Windows Form], metafile"
  - "metafile, visualizzazione"
ms.assetid: 60af1714-f148-4d85-a739-0557965ffa73
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: caricare e visualizzare metafile
La classe <xref:System.Drawing.Imaging.Metafile>, che eredita dalla classe <xref:System.Drawing.Image>, fornisce metodi per la registrazione, la visualizzazione e l'esame delle immagini vettoriali.  
  
## Esempio  
 Per visualizzare sullo schermo un'immagine vettoriale \(metafile\), sono necessari un oggetto <xref:System.Drawing.Imaging.Metafile> e un oggetto <xref:System.Drawing.Graphics>.  Passare il nome di un file o di un flusso a un costruttore <xref:System.Drawing.Imaging.Metafile>.  Creare un oggetto <xref:System.Drawing.Imaging.Metafile>, quindi passare tale oggetto <xref:System.Drawing.Imaging.Metafile> al metodo <xref:System.Drawing.Graphics.DrawImage%2A> di un oggetto <xref:System.Drawing.Graphics>.  
  
 Nell'esempio viene creato un oggetto <xref:System.Drawing.Imaging.Metafile> a partire da un file EMF \(Enhanced MetaFile, metafile avanzato\), quindi l'immagine viene disegnata con l'angolo superiore sinistro in corrispondenza del punto \(60, 10\).  
  
 Nell'illustrazione che segue si mostra il metafile disegnato nella posizione specificata.  
  
 ![Posizione dell'immagine](../../../../docs/framework/winforms/advanced/media/imageposition2.png "imageposition2")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.WorkingWithImages#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#41)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)