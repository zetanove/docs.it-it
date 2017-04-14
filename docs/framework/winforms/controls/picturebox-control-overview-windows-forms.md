---
title: "Cenni preliminari sul controllo PictureBox (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "PictureBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli immagini, informazioni sui controlli immagini"
  - "controlli immagini, informazioni sui controlli immagini"
  - "PictureBox (controllo) [Windows Form], informazioni sui controlli PictureBox"
ms.assetid: e5befee7-dc29-4888-a7c4-3b177e394112
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Cenni preliminari sul controllo PictureBox (Windows Form)
Il controllo <xref:System.Windows.Forms.PictureBox> Windows Form viene utilizzato per visualizzare immagini in formato bitmap, GIF, JPEG, metafile o icona.  
  
## Proprietà e metodi principali  
 L'immagine visualizzata viene determinata dalla proprietà <xref:System.Windows.Forms.PictureBox.Image%2A>, che può essere impostata in fase di esecuzione o in fase di progettazione.  In alternativa, è possibile specificare l'immagine impostando la proprietà <xref:System.Windows.Forms.PictureBox.ImageLocation%2A> e quindi caricare l'immagine in modo sincrono tramite il metodo <xref:System.Windows.Forms.PictureBox.Load%2A> oppure in modo asincrono tramite il metodo <xref:System.Windows.Forms.PictureBox.LoadAsync%2A>.  La proprietà <xref:System.Windows.Forms.PictureBox.SizeMode%2A> controlla il posizionamento reciproco tra immagine e controllo associato.  Per ulteriori informazioni, vedere [Procedura: modificare le dimensioni o la posizione di un'immagine in fase di esecuzione](../../../../docs/framework/winforms/controls/how-to-modify-the-size-or-placement-of-a-picture-at-run-time-windows-forms.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.PictureBox>   
 [Procedura: caricare un'immagine utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/how-to-load-a-picture-using-the-designer-windows-forms.md)   
 [Procedura: modificare le dimensioni o la posizione di un'immagine in fase di esecuzione](../../../../docs/framework/winforms/controls/how-to-modify-the-size-or-placement-of-a-picture-at-run-time-windows-forms.md)   
 [Procedura: impostare le immagini in fase di esecuzione](../../../../docs/framework/winforms/controls/how-to-set-pictures-at-run-time-windows-forms.md)   
 [Controllo PictureBox](../../../../docs/framework/winforms/controls/picturebox-control-windows-forms.md)