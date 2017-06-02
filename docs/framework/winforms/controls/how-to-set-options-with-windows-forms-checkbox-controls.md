---
title: "Procedura: impostare opzioni con i controlli CheckBox di Windows Form | Microsoft Docs"
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
  - "checked"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "caselle di controllo, utilizzo per impostare opzioni"
  - "CheckBox (controllo) [Windows Form], stato selezionato"
  - "CheckBox (controllo) [Windows Form], utilizzo per impostare opzioni"
ms.assetid: 2ac70498-7e3e-4e07-8901-ccabaeb5fd3e
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: impostare opzioni con i controlli CheckBox di Windows Form
Il controllo <xref:System.Windows.Forms.CheckBox> di Windows Form viene utilizzato per consentire agli utenti di scegliere tra le opzioni Vero\/Falso o Sì\/No.  Una volta effettuata la selezione, il controllo visualizzerà un segno di spunta.  
  
### Per impostare le opzioni con i controlli CheckBox  
  
1.  Verificare il valore della proprietà <xref:System.Windows.Forms.CheckBox.Checked%2A> per determinarne lo stato e utilizzare tale valore per impostare un'opzione.  
  
     Nell'esempio di codice riportato di seguito, quando viene generato l'evento <xref:System.Windows.Forms.CheckBox.CheckedChanged> del controllo <xref:System.Windows.Forms.CheckBox>, la proprietà <xref:System.Windows.Forms.Control.AllowDrop%2A> del form viene impostata su `false` se la casella di controllo è selezionata.  Questa funzione è utile per le situazioni in cui si desidera limitare l'interazione dell'utente.  
  
    ```vb  
    Private Sub CheckBox1_CheckedChanged(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles CheckBox1.CheckedChanged  
       ' Determine the CheckState of the check box.  
       If CheckBox1.CheckState = CheckState.Checked Then  
          ' If checked, do not allow items to be dragged onto the form.  
          Me.AllowDrop = False  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void checkBox1_CheckedChanged(object sender, System.EventArgs e)  
    {  
       // Determine the CheckState of the check box.  
       if (checkBox1.CheckState == CheckState.Checked)   
       {  
          // If checked, do not allow items to be dragged onto the form.  
          this.AllowDrop = false;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Determine the CheckState of the check box.  
          if (checkBox1->CheckState == CheckState::Checked)   
          {  
             // If checked, do not allow items to be dragged onto the form.  
             this->AllowDrop = false;  
          }  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.CheckBox>   
 [Cenni preliminari sul controllo CheckBox](../../../../docs/framework/winforms/controls/checkbox-control-overview-windows-forms.md)   
 [Procedura: rispondere alla selezione di controlli CheckBox Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-checkbox-clicks.md)   
 [Controllo CheckBox](../../../../docs/framework/winforms/controls/checkbox-control-windows-forms.md)