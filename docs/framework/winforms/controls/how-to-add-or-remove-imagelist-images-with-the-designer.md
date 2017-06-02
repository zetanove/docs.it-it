---
title: "Procedura: aggiungere o rimuovere immagini ImageList con la finestra di progettazione | Microsoft Docs"
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
  - "ImageList (componente) [Windows Form], aggiunta di immagini"
  - "ImageList (componente) [Windows Form], rimozione di immagini"
  - "immagini [Windows Form], aggiunta al componente ImageList"
ms.assetid: 5699b244-e37c-4d20-bc35-7441e55c1e3a
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: aggiungere o rimuovere immagini ImageList con la finestra di progettazione
È possibile aggiungere immagini a un componente <xref:System.Windows.Forms.ImageList> in molti modi.  Per aggiungere immagini molto velocemente, è possibile utilizzare lo smart tag associato alla classe <xref:System.Windows.Forms.ImageList> oppure, se si impostano diverse altre proprietà sulla classe <xref:System.Windows.Forms.ImageList>, può essere molto utile ricorrere alla finestra Proprietà.  Le immagini possono essere aggiunte anche mediante codice.  Per ulteriori informazioni su come aggiungere immagini con il codice, vedere [Procedura: aggiungere o rimuovere immagini tramite il componente ImageList Windows Form](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md).  Di solito, le immagini vengono inserite nel componente <xref:System.Windows.Forms.ImageList> prima che questo venga associato a un controllo, ma questa operazione non è obbligatoria.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere o rimuovere immagini mediante la finestra Proprietà  
  
1.  Selezionare il componente <xref:System.Windows.Forms.ImageList> o aggiungerne uno al form.  
  
2.  Nella finestra Proprietà, fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.ImageList.Images%2A>.  
  
3.  Nell'**Editor della raccolta Images**, fare clic su **Aggiungi** o **Rimuovi** per aggiungere o rimuovere immagini dall'elenco.  
  
### Per aggiungere o rimuovere immagini mediante smart tag  
  
1.  Selezionare il componente <xref:System.Windows.Forms.ImageList> o aggiungerne uno al form.  
  
2.  Fare clic sul glifo dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\).  
  
3.  Scegliere **Seleziona immagini** nella finestra di dialogo **Attività ImageList**.  
  
4.  Nell'**Editor della raccolta Images**, fare clic su **Aggiungi** o **Rimuovi** per aggiungere o rimuovere immagini dall'elenco.  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Procedura dettagliata: esecuzione di attività comuni utilizzando gli smart tag nei controlli Windows Form](../../../../docs/framework/winforms/controls/performing-common-tasks-using-smart-tags-on-wf-controls.md)   
 [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)