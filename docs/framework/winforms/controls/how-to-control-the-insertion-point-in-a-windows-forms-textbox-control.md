---
title: "Procedura: controllare il punto di inserimento in un controllo TextBox Windows Form | Microsoft Docs"
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
  - "punti di inserimento, controlli TextBox"
  - "caselle di testo, controllo del punto di inserimento"
  - "TextBox (controllo) [Windows Form], punto di inserimento"
ms.assetid: 5bee7d34-5121-429e-ab1f-d8ff67bc74c1
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: controllare il punto di inserimento in un controllo TextBox Windows Form
In base all'impostazione predefinita, quando un controllo <xref:System.Windows.Forms.TextBox> Windows Form riceve lo stato attivo il punto di inserimento all'interno della casella di testo si trova a sinistra del testo esistente.  È possibile spostare il punto di inserimento tramite tastiera o mouse.  Se la casella di testo torna allo stato attivo dopo essere stata disattivata, il punto di inserimento si troverà nell'ultima posizione assegnata dall'utente.  
  
 In alcuni casi ciò può costituire un problema per l'utente.  È possibile infatti che chi utilizza un'applicazione per l'elaborazione di testi ritenga scontato che i nuovi caratteri inseriti appaiano dopo il testo già presente.  Chi utilizza un'applicazione per l'inserimento di dati potrebbe invece aspettarsi che ogni nuovo carattere digitato sostituisca un carattere già esistente.  Le proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> e <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> consentono di modificare il comportamento per adattarlo alle specifiche esigenze.  
  
### Per controllare il punto di inserimento in un controllo TextBox  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionStart%2A> su un valore appropriato.  Zero posiziona il punto di inserimento immediatamente a sinistra del primo carattere.  
  
2.  \(Facoltativo\) Impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.SelectionLength%2A> sulla lunghezza del testo che si desidera selezionare.  
  
     Il codice riportato di seguito restituisce sempre il punto di inserimento su 0.  Il gestore eventi `TextBox1_Enter` deve essere associato al controllo. Per ulteriori informazioni, vedere [Creating Event Handlers in Windows Forms](../../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md).  
  
    ```vb  
    Private Sub TextBox1_Enter(ByVal sender As Object, ByVal e As System.EventArgs) Handles TextBox1.Enter  
       TextBox1.SelectionStart = 0  
       TextBox1.SelectionLength = 0  
    End Sub  
  
    ```  
  
    ```csharp  
    private void textBox1_Enter(Object sender, System.EventArgs e) {  
       textBox1.SelectionStart = 0;  
       textBox1.SelectionLength = 0;  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void textBox1_Enter(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          textBox1->SelectionStart = 0;  
          textBox1->SelectionLength = 0;  
       }  
    ```  
  
## Rendere il punto di inserimento visibile per impostazione predefinita  
 In un nuovo form il punto di inserimento di <xref:System.Windows.Forms.TextBox> è visibile per impostazione predefinita solo se il controllo <xref:System.Windows.Forms.TextBox> è il primo nell'ordine di tabulazione.  In caso contrario, il punto di inserimento viene visualizzato solo se si imposta lo stato attivo su <xref:System.Windows.Forms.TextBox> mediante la tastiera o il mouse.  
  
#### Per rendere il punto di inserimento della casella di testo visibile per impostazione predefinita sul nuovo form  
  
-   Impostare la proprietà <xref:System.Windows.Forms.Control.TabIndex%2A> del controllo <xref:System.Windows.Forms.TextBox> su `0`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextBox>   
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [Procedura: creare una casella di testo Password con il controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo in sola lettura](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [Procedura: inserire virgolette in una stringa](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [Procedura: selezionare testo nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [Procedura: visualizzare più righe nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [Controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)