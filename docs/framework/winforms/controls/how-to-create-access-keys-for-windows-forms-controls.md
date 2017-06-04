---
title: "Procedura: creare tasti di scelta per i controlli Windows Form | Microsoft Docs"
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
  - "tasti di scelta, creazione per i controlli"
  - "tasti di scelta, Windows Form"
  - "ALT (tasto)"
  - "carattere e commerciale nel tasto di scelta rapida"
  - "Button (controllo) [Windows Form], tasti di scelta"
  - "controlli [Windows Form], tasti di scelta"
  - "controlli delle finestre di dialogo, tasti di scelta"
  - "esempi [Windows Form], controlli"
  - "tasti di scelta rapida, creazione per i controlli"
  - "tasti di scelta"
  - "tasti di scelta, aggiunta ai controlli delle finestre di dialogo"
  - "Text (proprietà), specifica di tasti di scelta per controlli"
  - "controlli Windows Form, tasti di scelta"
ms.assetid: 4faa0991-28ec-4eca-91db-51dc2cd6a7ac
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare tasti di scelta per i controlli Windows Form
Un *tasto di scelta* corrisponde a un carattere sottolineato presente nel testo di un menu o di una voce di menu oppure nell'etichetta di un controllo, ad esempio di un pulsante.  Grazie a tale tasto è possibile scegliere un pulsante premendo il tasto ALT in combinazione con il tasto di scelta predefinito.  Se ad esempio tramite un pulsante viene eseguita una routine per la stampa di un form e la relativa proprietà `Text` viene impostata su "Stampa", aggiungendo una e commerciale \(&\) prima della lettera "S" la lettera "S" del testo del pulsante risulterà sottolineata in fase di esecuzione.  L'utente può eseguire il comando associato al pulsante premendo ALT\+P.  Non è possibile associare un tasto di scelta a un controllo che non può ricevere lo stato attivo.  
  
### Per creare un tasto di scelta per un controllo  
  
1.  Impostare la proprietà `Text` su una stringa comprendente una e commerciale \(&\) prima della lettera che costituirà il tasto di scelta.  
  
    ```vb  
    ' Set the letter "P" as an access key.  
    Button1.Text = "&Print"  
  
    ```  
  
    ```csharp  
    // Set the letter "P" as an access key.  
    button1.Text = "&Print";  
  
    ```  
  
    ```cpp  
    // Set the letter "P" as an access key.  
    button1->Text = "&Print";  
    ```  
  
    > [!NOTE]
    >  Per includere una e commerciale in una didascalia senza creare un tasto di scelta, inserire due e commerciali \(&&\).  Nella didascalia verrà visualizzata una singola e commerciale e nessun carattere risulterà sottolineato.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Button>   
 [Procedura: rispondere alla selezione dei pulsanti di Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [Procedura: impostare il testo visualizzato da un controllo di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)