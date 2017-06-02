---
title: "Procedura: caricare un&#39;immagine utilizzando la finestra di progettazione (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "form, visualizzazione di immagini"
  - "immagini [Windows Form], visualizzazione su Windows Form"
  - "formati immagine"
  - "PictureBox (controllo) [Windows Form], aggiunta di immagini"
  - "immagini, visualizzazione"
ms.assetid: 4dc7b973-afb1-4276-8322-20825af96655
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: caricare un&#39;immagine utilizzando la finestra di progettazione (Windows Form)
Il controllo <xref:System.Windows.Forms.PictureBox> di Windows Form consente di caricare e visualizzare un'immagine in un form in fase di progettazione, impostando la proprietà <xref:System.Windows.Forms.PictureBox.Image%2A> su un'immagine valida.  Nella tabella seguente sono riportati i tipi di file validi.  
  
|Type|Estensione del nome file|  
|----------|------------------------------|  
|Bitmap|BMP|  
|Icona|ICO|  
|GIF|GIF|  
|Metafile|WMF|  
|JPEG|JPG|  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per visualizzare un'immagine in fase di progettazione  
  
1.  Creare un controllo <xref:System.Windows.Forms.PictureBox> in un form.  
  
2.  Nella finestra Proprietà selezionare la proprietà <xref:System.Windows.Forms.PictureBox.Image%2A>, quindi fare clic sul pulsante con i puntini di sospensione per visualizzare la finestra di dialogo **Apri**.  
  
3.  Se si desidera utilizzare file di tipo particolare, ad esempio file GIF, selezionare il tipo dalla casella **Tipo file**.  
  
4.  Selezionare il file che si desidera utilizzare.  
  
### Per rimuovere l'immagine in fase di progettazione  
  
1.  Nella finestra **Proprietà** selezionare la proprietà <xref:System.Windows.Forms.PictureBox.Image%2A> e fare clic con il pulsante destro del mouse sull'anteprima visualizzata a sinistra del nome dell'oggetto immagine.  Scegliere **Reimposta**.  
  
## Vedere anche  
 <xref:System.Windows.Forms.PictureBox>   
 [Cenni preliminari sul controllo PictureBox](../../../../docs/framework/winforms/controls/picturebox-control-overview-windows-forms.md)   
 [Procedura: modificare le dimensioni o la posizione di un'immagine in fase di esecuzione](../../../../docs/framework/winforms/controls/how-to-modify-the-size-or-placement-of-a-picture-at-run-time-windows-forms.md)   
 [Procedura: impostare le immagini in fase di esecuzione](../../../../docs/framework/winforms/controls/how-to-set-pictures-at-run-time-windows-forms.md)   
 [Controllo PictureBox](../../../../docs/framework/winforms/controls/picturebox-control-windows-forms.md)