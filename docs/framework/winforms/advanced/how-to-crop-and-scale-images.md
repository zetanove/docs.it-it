---
title: "Procedura: ritagliare e adattare immagini | Microsoft Docs"
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
  - "immagini [Windows Form], ritaglio"
  - "immagini [Windows Form], adattamento"
ms.assetid: 053e3360-bca0-4b25-9afa-0e77a6f17b03
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: ritagliare e adattare immagini
Nella classe <xref:System.Drawing.Graphics> sono disponibili numerosi metodi <xref:System.Drawing.Graphics.DrawImage%2A>, alcuni dei quali dispongono di parametri dei rettangoli di origine e di destinazione utilizzabili per ritagliare e adattare le immagini.  
  
## Esempio  
 Nell'esempio che segue viene costruito un oggetto <xref:System.Drawing.Image> dal file su disco Apple.gif.  L'intera immagine della mela viene disegnata con le dimensioni originali.  Il codice chiama quindi il metodo <xref:System.Drawing.Graphics.DrawImage%2A> di un oggetto <xref:System.Drawing.Graphics> per disegnare parte dell'immagine della mela in un rettangolo di destinazione con dimensioni superiori a quelle dell'immagine originale.  
  
 Il metodo <xref:System.Drawing.Graphics.DrawImage%2A> consente di determinare quale parte della mela disegnare, tramite un esame del rettangolo di origine, specificato dal terzo, quarto, quinto e sesto argomento.  In questo caso la mela verrà ridotta al 75% della sua larghezza e altezza.  
  
 Il metodo <xref:System.Drawing.Graphics.DrawImage%2A> consente di determinare dove e con quali dimensioni disegnare la mela ritagliata, tramite un esame del rettangolo di destinazione, specificato dal secondo argomento.  In questo caso il rettangolo di destinazione sarà più alto e più largo del 30% rispetto all'originale.  
  
 Nell'illustrazione che segue si visibili l'immagine originale e l'immagine adattata e ritagliata.  
  
 ![Ritaglio e adattamento](../../../../docs/framework/winforms/advanced/media/cscropscale1.png "csCropScale1")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.WorkingWithImages#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  Sostituire `Apple.gif` con il nome e il percorso di un file di immagine valido per il sistema.  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)