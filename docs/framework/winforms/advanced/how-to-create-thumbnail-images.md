---
title: "Procedura: creare miniature | Microsoft Docs"
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
  - "immagini [Windows Form], creazione di anteprime in miniatura"
  - "anteprime in miniatura delle immagini, creazione"
ms.assetid: e956242a-1e5b-4217-a3cf-5f3fb45d00ba
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Procedura: creare miniature
Un'anteprima di immagine è una versione di un'immagine di dimensioni ridotte.  È possibile creare un'anteprima chiamando il metodo <xref:System.Drawing.Image.GetThumbnailImage%2A> di un oggetto <xref:System.Drawing.Image>.  
  
## Esempio  
 Nell'esempio che segue viene costruito un oggetto <xref:System.Drawing.Image> da un file JPG.  Si suppone che l'immagine originale abbia una larghezza di 640 pixel e un'altezza di 479 pixel.  Viene creata un'anteprima dell'immagine con una larghezza di 100 pixel e un'altezza di 100 pixel.  
  
 Nell'illustrazione che segue si mostra l'anteprima dell'immagine.  
  
 ![Immagine di anteprima](../../../../docs/framework/winforms/advanced/media/thumbnail1.png "Thumbnail1")  
  
> [!NOTE]
>  In questo esempio, un metodo di callback viene dichiarato ma mai utilizzato.  Supporta tutte le versioni di GDI\+.  
  
 [!code-csharp[System.Drawing.WorkingWithImages#71](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#71)]
 [!code-vb[System.Drawing.WorkingWithImages#71](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#71)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  Per eseguire l'esempio, attenersi alla seguente procedura:  
  
1.  Creare una nuova applicazione Windows Form.  
  
2.  Aggiungere il codice di esempio al form.  
  
3.  Creare un gestore per l'evento <xref:System.Windows.Forms.Control.Paint> del form.  
  
4.  Nel gestore di <xref:System.Windows.Forms.Control.Paint>, chiamare il metodo `GetThumbnail` e passare `e` per <xref:System.Windows.Forms.PaintEventArgs>.  
  
5.  Individuare un file di immagine del quale si desidera creare un'anteprima.  
  
6.  Nel metodo `GetThumbnail` specificare il percorso e il nome file dell'immagine.  
  
7.  Premere F5 per eseguire l'esempio.  
  
     Un'immagine di anteprima 100 x 100 verrà visualizzata nel form.  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)