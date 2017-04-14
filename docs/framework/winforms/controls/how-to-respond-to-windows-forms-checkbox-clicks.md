---
title: "Procedura: rispondere alla selezione di controlli CheckBox Windows Form | Microsoft Docs"
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
  - "caselle di controllo, risposta a eventi"
  - "CheckBox (controllo) [Windows Form], eventi Click"
  - "Click (evento), CheckBox (controllo)"
  - "doppio clic"
  - "eventi [Windows Form], eventi Click"
ms.assetid: c39f901e-8899-43b6-aa31-939cbf7089fb
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: rispondere alla selezione di controlli CheckBox Windows Form
Se si fa clic su un controllo <xref:System.Windows.Forms.CheckBox> Windows Form, viene generato un evento <xref:System.Windows.Forms.Control.Click>.  È possibile programmare l'applicazione per eseguire una data azione in base allo stato della casella di controllo.  
  
### Per programmare la risposta agli eventi Click dei controlli CheckBox  
  
1.  Nel gestore eventi <xref:System.Windows.Forms.Control.Click> utilizzare la proprietà <xref:System.Windows.Forms.CheckBox.Checked%2A> per determinare lo stato del controllo ed eseguire le operazioni eventualmente necessarie.  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       ' The CheckBox control's Text property is changed each time the   
       ' control is clicked, indicating a checked or unchecked state.  
       If CheckBox1.Checked = True Then  
          CheckBox1.Text = "Checked"  
       Else  
          CheckBox1.Text = "Unchecked"  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       // The CheckBox control's Text property is changed each time the   
       // control is clicked, indicating a checked or unchecked state.  
       if (checkBox1.Checked)  
       {  
          checkBox1.Text = "Checked";  
       }  
       else  
       {  
          checkBox1.Text = "Unchecked";  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if (checkBox1->Checked)  
          {  
             checkBox1->Text = "Checked";  
          }  
          else  
          {  
             checkBox1->Text = "Unchecked";  
          }  
       }  
    ```  
  
    > [!NOTE]
    >  Se si fa doppio clic sul controllo <xref:System.Windows.Forms.CheckBox>, ogni clic viene elaborato singolarmente, dato che il controllo <xref:System.Windows.Forms.CheckBox> non supporta l'evento generato dal doppio clic.  
  
    > [!NOTE]
    >  Quando la proprietà <xref:System.Windows.Forms.CheckBox.AutoCheck%2A> è impostata su `true` \(impostazione predefinita\), il controllo <xref:System.Windows.Forms.CheckBox> viene selezionato o deselezionato automaticamente quando ci si fa clic sopra.  In caso contrario è necessario impostare manualmente la proprietà <xref:System.Windows.Forms.CheckBox.Checked%2A> quando viene generato l'evento <xref:System.Windows.Forms.Control.Click>.  
  
     È inoltre possibile utilizzare il controllo <xref:System.Windows.Forms.CheckBox> per stabilire un'operazione da eseguire.  
  
### Per stabilire un'operazione da eseguire quando si seleziona una casella di controllo  
  
1.  Utilizzare un'istruzione per interrogare il valore della proprietà <xref:System.Windows.Forms.CheckBox.CheckState%2A> e stabilire un'azione da eseguire.  Se la proprietà <xref:System.Windows.Forms.CheckBox.ThreeState%2A> è impostata su `true`, la proprietà <xref:System.Windows.Forms.CheckBox.CheckState%2A> può restituire tre valori possibili che rappresentano la casella selezionata, la casella deselezionata o un terzo stato non definito in cui la casella viene visualizzata come inattiva per indicare che l'opzione non è disponibile.  
  
    ```vb  
    Private Sub CheckBox1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles CheckBox1.Click  
       Select Case CheckBox1.CheckState  
          Case CheckState.Checked  
             ' Code for checked state.  
          Case CheckState.Unchecked  
             ' Code for unchecked state.  
          Case CheckState.Indeterminate  
             ' Code for indeterminate state.  
       End Select   
    End Sub  
  
    ```  
  
    ```csharp  
    private void checkBox1_Click(object sender, System.EventArgs e)  
    {  
       switch(checkBox1.CheckState)  
       {  
          case CheckState.Checked:  
             // Code for checked state.  
             break;  
          case CheckState.Unchecked:  
             // Code for unchecked state.  
             break;  
          case CheckState.Indeterminate:  
             // Code for indeterminate state.  
             break;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          switch(checkBox1->CheckState) {  
             case CheckState::Checked:  
                // Code for checked state.  
                break;  
             case CheckState::Unchecked:  
                // Code for unchecked state.  
                break;  
             case CheckState::Indeterminate:  
                // Code for indeterminate state.  
                break;  
          }  
       }  
    ```  
  
    > [!NOTE]
    >  Quando la proprietà <xref:System.Windows.Forms.CheckBox.ThreeState%2A> è impostata su `true`, la proprietà <xref:System.Windows.Forms.CheckBox.Checked%2A> restituisce `true` sia per <xref:System.Windows.Forms.CheckState> che per <xref:System.Windows.Forms.CheckState>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.CheckBox>   
 [Cenni preliminari sul controllo CheckBox](../../../../docs/framework/winforms/controls/checkbox-control-overview-windows-forms.md)   
 [Procedura: impostare opzioni con i controlli CheckBox di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-options-with-windows-forms-checkbox-controls.md)   
 [Controllo CheckBox](../../../../docs/framework/winforms/controls/checkbox-control-windows-forms.md)