---
title: "Procedura: selezionare testo nel controllo TextBox Windows Form | Microsoft Docs"
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
  - "caselle di testo, selezione di testo a livello di codice"
  - "testo, selezione in caselle di testo a livello di codice"
  - "TextBox (controllo) [Windows Form], selezione di testo a livello di codice"
ms.assetid: 8c591546-6a01-45c7-8e03-f78431f903b1
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Procedura: selezionare testo nel controllo TextBox Windows Form
Nel controllo <xref:System.Windows.Forms.TextBox> Windows Form è possibile selezionare testo a livello di codice.  Se ad esempio si crea una funzione che cerca il testo di una particolare stringa, sarà possibile selezionare il testo da visualizzare per mostrare all'utente il percorso della stringa trovata.  
  
### Per selezionare testo a livello di codice  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> all'inizio del testo che si desidera selezionare.  
  
     La proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> è un numero che indica il punto di inserimento all'interno della stringa di testo. La cifra zero \(0\) rappresenta la posizione più a sinistra.  Se la proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> è impostata su un valore uguale o maggiore al numero di caratteri nella casella di testo, il punto di inserimento verrà posizionato dopo l'ultimo carattere.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> sulla lunghezza del testo che si desidera selezionare.  
  
     La proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> è un valore numerico che imposta la larghezza del punto di inserimento.  Se si imposta la proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> su un numero maggiore di 0, verrà selezionato tale numero di caratteri a partire dal punto di inserimento corrente.  
  
3.  \(Facoltativo\) Accedere al testo selezionato tramite la proprietà <xref:System.Windows.Forms.TextBoxBase.SelectedText%2A>.  
  
     Il codice riportato di seguito consente di selezionare il contenuto di una casella di testo quando viene generato l'evento <xref:System.Windows.Forms.Control.Enter> relativo al controllo.  In questo esempio viene controllato se la casella di testo contiene un valore per la proprietà <xref:System.Windows.Forms.TextBox.Text%2A> diverso da `null` o una stringa vuota.  Quando la casella di testo ha lo stato attivo, viene selezionato il testo corrente nella casella di testo.  Il gestore eventi `TextBox1_Enter` deve essere associato al controllo. Per ulteriori informazioni, vedere [How to: Create Event Handlers at Run Time for Windows Forms](../../../../docs/framework/winforms/how-to-create-event-handlers-at-run-time-for-windows-forms.md).  
  
     Per testare questo esempio, premere TAB finché la casella di testo non ha lo stato attivo.  Se si fa clic nella casella di testo, il testo viene deselezionato.  
  
    ```vb  
    Private Sub TextBox1_Enter(ByVal sender As Object, ByVal e As System.EventArgs) Handles TextBox1.Enter  
       If (Not String.IsNullOrEmpty(TextBox1.Text)) Then  
          TextBox1.SelectionStart = 0  
          TextBox1.SelectionLength = TextBox1.Text.Length  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void textBox1_Enter(object sender, System.EventArgs e){  
       if (!String.IsNullOrEmpty(textBox1.Text))  
       {  
          textBox1.SelectionStart = 0;  
          textBox1.SelectionLength = textBox1.Text.Length;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void textBox1_Enter(System::Object ^ sender,  
          System::EventArgs ^ e) {  
       if (!System::String::IsNullOrEmpty(textBox1->Text))  
       {  
          textBox1->SelectionStart = 0;  
          textBox1->SelectionLength = textBox1->Text->Length;  
       }  
    }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextBox>   
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [Procedura: controllare il punto di inserimento in un controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo Password con il controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo in sola lettura](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [Procedura: inserire virgolette in una stringa](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [Procedura: visualizzare più righe nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [Controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)