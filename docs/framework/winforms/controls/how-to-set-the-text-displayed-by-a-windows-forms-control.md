---
title: "Procedura: impostare il testo visualizzato da un controllo di Windows Form | Microsoft Docs"
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
  - "Button (controllo) [Windows Form], testo dei pulsanti"
  - "Button (controllo) [Windows Form], visualizzazione di testo"
  - "pulsanti, testo"
  - "didascalie, impostazione"
  - "didascalie, controlli Windows Form"
  - "controlli [Windows Form], didascalie"
  - "esempi [Windows Form], controlli"
  - "form, didascalie"
  - "etichette, aggiunta al controllo CommandButton"
  - "StdFont (oggetto) e didascalia CommandButton"
  - "testo"
  - "Text (proprietà), controllo Windows Form"
  - "testo, controlli Windows Form"
  - "Windows Form, didascalie"
ms.assetid: 36b95bff-8780-479d-b86a-f1a0673653aa
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: impostare il testo visualizzato da un controllo di Windows Form
I controlli Windows Form in genere visualizzano il testo relativo alla funzione principale del controllo.  Un controllo <xref:System.Windows.Forms.Button>, ad esempio, solitamente visualizza una didascalia indicante l'azione che verrà eseguita quando si sceglie il pulsante.  Per tutti i controlli, il testo può essere impostato o restituito mediante la proprietà <xref:System.Windows.Forms.Control.Text%2A>.  È possibile modificare il tipo di carattere usando la proprietà <xref:System.Windows.Forms.Control.Font%2A>.  È anche possibile impostare il testo nella finestra di progettazione.  Vedere anche [Procedura: Creare tasti di scelta per i controlli Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/ms233673\(v=vs.110\)), [Procedura: Impostare il testo visualizzato da un controllo Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/ms233665\(v=vs.110\)), [Procedura: Impostare l'immagine visualizzata da un controllo Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/ms233656\(v=vs.110\)).  
  
### Per impostare il testo visualizzato da un controllo a livello di codice  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Control.Text%2A> su una stringa.  
  
     Per creare un tasto di scelta sottolineato, includere una e commerciale \(&\) prima della lettera che corrisponderà al tasto di scelta.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.Control.Font%2A> su un oggetto di tipo <xref:System.Drawing.Font>.  
  
    ```vb  
    Button1.Text = "Click here to save changes"  
    Button1.Font = New Font("Arial", 10, FontStyle.Bold, GraphicsUnit.Point)  
    ```  
  
    ```csharp  
    button1.Text = "Click here to save changes";  
    button1.Font = new Font("Arial", 10, FontStyle.Bold,  
       GraphicsUnit.Point);  
    ```  
  
    ```cpp#  
    button1->Text = "Click here to save changes";  
    button1->Font = new System::Drawing::Font("Arial",  
       10, FontStyle::Bold, GraphicsUnit::Point);  
    ```  
  
    > [!NOTE]
    >  È possibile usare un carattere di escape per visualizzare un carattere speciale in elementi dell'interfaccia utente in cui tale carattere verrebbe in genere interpretato in modo diverso, ad esempio nelle voci di menu.  Nella riga di codice seguente, ad esempio, il testo della voce di menu viene impostato in modo che appaia come "& Now For Something Completely Different":  
  
    ```vb  
    MPMenuItem.Text = "&& Now For Something Completely Different"  
    ```  
  
    ```csharp  
    mpMenuItem.Text = "&& Now For Something Completely Different";  
    ```  
  
    ```cpp#  
    mpMenuItem->Text = "&& Now For Something Completely Different";  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.Text%2A?displayProperty=fullName>   
 [Procedura: creare tasti di scelta per i controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)   
 [Procedura: rispondere alla selezione dei pulsanti di Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)