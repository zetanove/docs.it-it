---
title: "Procedura: impostare il testo visualizzato da un controllo Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "controlli [Windows Form], impostazione di didascalie"
  - "Windows Form, impostazione del testo visualizzato"
ms.assetid: 9d18e0e0-f17f-4074-837d-e67ceeeaa89d
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: impostare il testo visualizzato da un controllo Windows Form utilizzando la finestra di progettazione
In genere, i controlli Windows Form consentono di visualizzare il testo relativo alla funzione principale del controllo.  Un controllo <xref:System.Windows.Forms.Button>, ad esempio, solitamente consente di visualizzare una didascalia dell'azione che verrà eseguita quando si sceglie il pulsante.  Per tutti i controlli, il testo può essere impostato o restituito mediante la proprietà <xref:System.Windows.Forms.Control.Text%2A>.  È possibile modificare il tipo di carattere utilizzando la proprietà <xref:System.Windows.Forms.Control.Font%2A>.  
  
### Per impostare il testo e il tipo di carattere con la finestra di progettazione  
  
1.  Nella finestra Proprietà, impostare la proprietà <xref:System.Windows.Forms.Control.Text%2A> del controllo su una stringa appropriata.  
  
     Per creare un tasto di scelta rapida sottolineato inserire una e commerciale \(&\) prima della lettera che costituirà il tasto di scelta rapida.  
  
2.  Nella finestra Proprietà, fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.Control.Font%2A>.  
  
     Nella finestra di dialogo standard dei caratteri, selezionare il carattere, lo stile, le dimensioni, gli effetti, ad esempio barrato o sottolineato, e lo script desiderati.  
  
## Vedere anche  
 [Procedura: impostare il testo visualizzato da un controllo di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)