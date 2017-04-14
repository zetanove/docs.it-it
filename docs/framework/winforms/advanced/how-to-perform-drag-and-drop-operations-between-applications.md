---
title: "How to: Perform Drag-and-Drop Operations Between Applications | Microsoft Docs"
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
  - "drag and drop, between applications"
ms.assetid: fa347436-2b12-4dd6-8507-59d7241f6a06
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Perform Drag-and-Drop Operations Between Applications
Eseguire operazioni di trascinamento della selezione tra applicazioni non è diverso dal consentire quest'azione nell'ambito di un'applicazione, purché entrambe le applicazioni implicate si comportino in base al "contratto" stabilito tra le proprietà <xref:System.Windows.Forms.DragEventArgs.AllowedEffect%2A> e <xref:System.Windows.Forms.DragEventArgs.Effect%2A>.  
  
 Nella procedura seguente si userà un'applicazione basata su Windows creata dall'utente e l'elaboratore di testi WordPad incluso con il sistema operativo Windows per eseguire operazioni di trascinamento della selezione tra applicazioni.  WordPad offre un determinato set di effetti consentiti per il trascinamento del testo selezionato; l'applicazione basata su Windows per cui si scriverà il codice interagirà con tali effetti, in modo che le operazioni di trascinamento della selezione possano essere completate correttamente.  
  
### Per eseguire una procedura di trascinamento della selezione tra applicazioni  
  
1.  Creare una nuova applicazione Windows Form.  
  
2.  Aggiungere un oggetto <xref:System.Windows.Forms.TextBox> al form.  
  
3.  Configurare il controllo <xref:System.Windows.Forms.TextBox> per ricevere dati trascinati.  
  
     Per altre informazioni, vedere [Procedura dettagliata: Esecuzione di un'operazione di trascinamento della selezione in Windows Form](../../../../docs/framework/winforms/advanced/walkthrough-performing-a-drag-and-drop-operation-in-windows-forms.md).  
  
4.  Eseguire l'applicazione basata su Windows e, mentre l'applicazione è in esecuzione, eseguire WordPad.  
  
     WordPad è un editor di testo installato da Windows che consente operazioni di trascinamento della selezione.  È accessibile premendo **Start**, selezionando **Esegui** e digitando `WordPad` nella casella di testo nella finestra di dialogo **Esegui** e facendo clic su **OK**.  
  
5.  Una volta aperto WordPad, digitare una stringa di testo al suo interno.  
  
6.  Usando il mouse, selezionare il testo e quindi trascinarlo sul controllo <xref:System.Windows.Forms.TextBox> nell'applicazione basata su Windows.  
  
     Osservare che quando si passa il mouse sul controllo <xref:System.Windows.Forms.TextBox> \(e, di conseguenza, si genera l'evento <xref:System.Windows.Forms.Control.DragEnter>\), il cursore cambia ed è possibile rilasciare il testo selezionato sul controllo <xref:System.Windows.Forms.TextBox>.  
  
     È anche possibile configurare il controllo <xref:System.Windows.Forms.TextBox> per consentire il trascinamento delle stringhe di testo in WordPad.  Per altre informazioni, vedere [Walkthrough: Performing a Drag\-and\-Drop Operation in Windows Forms](../../../../docs/framework/winforms/advanced/walkthrough-performing-a-drag-and-drop-operation-in-windows-forms.md).  
  
## Vedere anche  
 [How to: Add Data to the Clipboard](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md)   
 [How to: Retrieve Data from the Clipboard](../../../../docs/framework/winforms/advanced/how-to-retrieve-data-from-the-clipboard.md)   
 [Drag\-and\-Drop Operations and Clipboard Support](../../../../docs/framework/winforms/advanced/drag-and-drop-operations-and-clipboard-support.md)