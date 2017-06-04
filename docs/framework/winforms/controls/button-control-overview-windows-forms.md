---
title: "Cenni preliminari sul controllo Button (Windows Form) | Microsoft Docs"
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
  - "Button"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Button (controllo) [Windows Form], informazioni sul controllo Button"
  - "pulsanti, informazioni sui pulsanti"
ms.assetid: 255b291b-51a9-4a92-a1a4-2400cd82443f
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Cenni preliminari sul controllo Button (Windows Form)
Il controllo <xref:System.Windows.Forms.Button> Windows Form consente all'utente di eseguire le operazioni desiderate facendo clic su un pulsante.  Una volta scelto, il pulsante viene visualizzato come se fosse stato effettivamente attivato e poi rilasciato.  Quando l'utente fa clic su un pulsante, viene richiamato il gestore eventi <xref:System.Windows.Forms.Control.Click>.  Per eseguire qualsiasi operazione, inserire il codice nel gestore eventi <xref:System.Windows.Forms.Control.Click>.  
  
 Il testo visualizzato nel pulsante è specificato nella proprietà <xref:System.Windows.Forms.Control.Text%2A>.  Se la larghezza del testo è superiore a quella del pulsante, il testo viene mandato a capo.  In caso le dimensioni del pulsante non siano comunque sufficienti a contenerlo, il testo risulterà tagliato.  Per ulteriori informazioni, vedere [Procedura: impostare il testo visualizzato da un controllo di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md).  La proprietà <xref:System.Windows.Forms.Control.Text%2A> può contenere un tasto di scelta che consente di selezionare il controllo premendo contemporaneamente ALT e tale tasto.  Per informazioni dettagliate, vedere [Procedura: creare tasti di scelta per i controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md).  L'aspetto del testo viene controllato dalle proprietà <xref:System.Windows.Forms.Control.Font%2A> e <xref:System.Windows.Forms.ButtonBase.TextAlign%2A>.  
  
 Il controllo  <xref:System.Windows.Forms.Button> consente inoltre di visualizzare immagini utilizzando le proprietà <xref:System.Windows.Forms.ButtonBase.Image%2A> e <xref:System.Windows.Forms.ButtonBase.ImageList%2A>.  Per ulteriori informazioni, vedere [Procedura: impostare l'immagine visualizzata da un controllo Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-image-displayed-by-a-windows-forms-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.Button>   
 [Procedura: rispondere alla selezione dei pulsanti di Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [Modalità di selezione di un controllo Button Windows Form](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [Procedura: designare un pulsante Windows Form come pulsante di conferma utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/designate-a-wf-button-as-the-accept-button-using-the-designer.md)   
 [Procedura: designare un pulsante Windows Form come pulsante Annulla utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/designate-a-wf-button-as-the-cancel-button-using-the-designer.md)   
 [Controllo Button](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)