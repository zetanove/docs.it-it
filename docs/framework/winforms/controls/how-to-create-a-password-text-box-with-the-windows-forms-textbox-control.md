---
title: "Procedura: creare una casella di testo Password con il controllo TextBox Windows Form | Microsoft Docs"
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
  - "caselle password, creazione"
  - "PasswordChar (proprietà nelle caselle di testo)"
  - "password, maschera di input"
  - "password, Password (casella di testo)"
  - "TextBox (controllo) [Windows Form], immissione di password"
ms.assetid: d105d6b9-3d50-44cd-80d8-2c0e2f486727
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: creare una casella di testo Password con il controllo TextBox Windows Form
Una casella di testo Password è una casella di testo di Windows Form che visualizza caratteri segnaposto mentre l'utente digita una stringa.  
  
### Per creare una casella di testo Password  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.TextBox.PasswordChar%2A> del controllo <xref:System.Windows.Forms.TextBox> su un carattere specifico.  
  
     La proprietà <xref:System.Windows.Forms.TextBox.PasswordChar%2A> specifica il carattere visualizzato nella casella di testo.  Se ad esempio si desidera che vengano visualizzati degli asterischi che sostituiscano ogni carattere digitato nella casella password, specificare \* per la proprietà <xref:System.Windows.Forms.TextBox.PasswordChar%2A> nella finestra Proprietà.  Verrà visualizzato un asterisco indipendentemente dal carattere digitato dall'utente.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.MaxLength%2A> \(facoltativo\).  La proprietà determina il numero di caratteri che è possibile digitare nella casella di testo.  Se si supera la lunghezza massima consentita, il sistema emetterà un segnale acustico e la casella di testo non accetterà ulteriori caratteri.  Si noti che è improbabile che si intenda eseguire tale operazione, in quanto la lunghezza massima di una password potrebbe rappresentare un'informazione utile per eventuali malintenzionati che tentino di indovinare la password stessa.  
  
     Nel codice qui di seguito viene illustrato come inizializzare una casella di testo che accetta una stringa di un massimo di 14 caratteri e visualizza una serie di asterischi al posto della stringa.  La routine `InitializeMyControl`  non viene eseguita automaticamente, ma deve essere richiamata.  
  
    > [!IMPORTANT]
    >  Utilizzando la proprietà <xref:System.Windows.Forms.TextBox.PasswordChar%2A> su una casella di testo è possibile evitare che altri utenti scoprano la password di un utente al momento dell'accesso.  Questo metodo di sicurezza non impedisce l'archiviazione o la trasmissione della password dovuta alla logica dell'applicazione.  Poiché il testo non è crittografato in alcun modo, è opportuno considerarlo come dati riservati.  Anche se non appare come tale, la password verrà comunque considerata come stringa di solo testo, a meno che non sia stato implementato un ulteriore metodo di sicurezza.  
  
    ```vb  
    Private Sub InitializeMyControl()  
       ' Set to no text.  
       TextBox1.Text = ""  
       ' The password character is an asterisk.  
       TextBox1.PasswordChar = "*"  
       ' The control will allow no more than 14 characters.  
       TextBox1.MaxLength = 14  
    End Sub  
  
    ```  
  
    ```csharp  
    private void InitializeMyControl()  
    {  
       // Set to no text.  
       textBox1.Text = "";  
       // The password character is an asterisk.  
       textBox1.PasswordChar = '*';  
       // The control will allow no more than 14 characters.  
       textBox1.MaxLength = 14;  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void InitializeMyControl()  
       {  
          // Set to no text.  
          textBox1->Text = "";  
          // The password character is an asterisk.  
          textBox1->PasswordChar = '*';  
          // The control will allow no more than 14 characters.  
          textBox1->MaxLength = 14;  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextBox>   
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [Procedura: controllare il punto di inserimento in un controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo in sola lettura](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [Procedura: inserire virgolette in una stringa](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [Procedura: selezionare testo nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [Procedura: visualizzare più righe nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [Controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)