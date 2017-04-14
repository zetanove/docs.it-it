---
title: "Modalit&#224; di selezione di un controllo Button Windows Form | Microsoft Docs"
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
  - "Button (controllo) [Windows Form], selezione"
ms.assetid: fe2fc058-5118-4f70-b264-6147d64a7a8d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Modalit&#224; di selezione di un controllo Button Windows Form
È possibile scegliere un pulsante di Windows Form in uno dei modi seguenti:  
  
-   Fare clic sul pulsante con il mouse.  
  
-   Richiamare l'evento <xref:System.Windows.Forms.Control.Click> del pulsante tramite il codice.  
  
-   Spostare lo stato attivo sul pulsante premendo TAB, quindi scegliere il pulsante premendo BARRA SPAZIATRICE o INVIO.  
  
-   Premere il tasto di scelta del pulsante \(ALT \+ lettera sottolineata\).  Per ulteriori informazioni sui tasti di scelta, vedere [Procedura: creare tasti di scelta per i controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md).  
  
-   Se il pulsante in questione è il pulsante di conferma del form, premendo INVIO si sceglierà tale pulsante anche se un altro controllo detiene lo stato attivo, a meno che quest'ultimo non sia a sua volta un pulsante, una casella di testo a più righe oppure un controllo personalizzato che intercetta il tasto Invio.  
  
-   Se il pulsante in questione è il pulsante di annullamento del form, premendo ESC si sceglierà tale pulsante anche se un altro controllo detiene lo stato attivo.  
  
-   Chiamare il metodo <xref:System.Windows.Forms.Button.PerformClick%2A> per scegliere il pulsante a livello di codice.  
  
## Vedere anche  
 [Cenni preliminari sul controllo Button](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [Procedura: rispondere alla selezione dei pulsanti di Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [Controllo Button](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)