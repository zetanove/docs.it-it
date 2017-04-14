---
title: "Procedura: determinare il figlio MDI attivo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "form figlio"
  - "Appunti, copia di dati"
  - "MDI, attivazione di form"
  - "MDI, finestre figlio"
  - "MDI, individuazione dello stato attivo"
ms.assetid: 33880ec3-0207-4c2b-a616-ff140443cc0f
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: determinare il figlio MDI attivo
Occasionalmente può essere utile fornire un comando che agisca sul controllo con lo stato attivo sul form figlio attualmente attivo.  Se si desidera, ad esempio, copiare il testo selezionato dalla casella di testo del form figlio negli Appunti,  creare una routine che copi il testo selezionato negli Appunti mediante l'evento <xref:System.Windows.Forms.Control.Click> della voce Copia del menu standard Modifica.  
  
 Poiché un'applicazione MDI può avere molte istanze dello stesso form figlio, è necessario specificare quale form deve essere utilizzato dalla routine.  Per specificare il form corretto, utilizzare la proprietà <xref:System.Windows.Forms.Form.ActiveMdiChild%2A> che restituisce il form figlio con lo stato attivo o quello che è stato attivato più recentemente.  
  
 Quando su un form sono disponibili diversi controlli è necessario specificare anche quale sia il controllo attivo.  Analogamente alla proprietà <xref:System.Windows.Forms.Form.ActiveMdiChild%2A>, la proprietà <xref:System.Windows.Forms.ContainerControl.ActiveControl%2A> restituisce il controllo con lo stato attivo sul form figlio attivo.  Di seguito è illustrata una routine di copia che può essere chiamata dal menu di un form figlio, da un menu sul form MDI o da un pulsante della barra degli strumenti.  
  
### Per determinare il figlio MDI attivo e copiarne il testo negli Appunti  
  
1.  In un metodo, copiare negli Appunti il testo del controllo attivo del form figlio attivo.  
  
    > [!NOTE]
    >  Nell'esempio qui di seguito si presume l'esistenza di un form padre MDI \(`Form1`\) con una o più finestre figlio MDI contenenti un controllo <xref:System.Windows.Forms.RichTextBox>.  Per ulteriori informazioni, vedere [Creazione di form padre MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md).  
  
    ```vb  
    Public Sub mniCopy_Click(ByVal sender As Object, _  
       ByVal e As System.EventArgs) Handles mniCopy.Click  
  
       ' Determine the active child form.  
       Dim activeChild As Form = Me.ActiveMDIChild  
  
       ' If there is an active child form, find the active control, which  
       ' in this example should be a RichTextBox.  
       If (Not activeChild Is Nothing) Then  
          Dim theBox As RichTextBox = _  
            TryCast(activeChild.ActiveControl, RichTextBox)  
  
          If (Not theBox Is Nothing) Then  
             'Put selected text on Clipboard.  
             Clipboard.SetDataObject(theBox.SelectedText)  
          Else  
             MessageBox.Show("You need to select a RichTextBox.")  
          End If  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void mniCopy_Click (object sender, System.EventArgs e)  
    {  
       // Determine the active child form.  
       Form activeChild = this.ActiveMdiChild;  
  
       // If there is an active child form, find the active control, which  
       // in this example should be a RichTextBox.  
       if (activeChild != null)  
       {    
          try  
          {  
             RichTextBox theBox = (RichTextBox)activeChild.ActiveControl;  
             if (theBox != null)  
             {  
                // Put the selected text on the Clipboard.  
                Clipboard.SetDataObject(theBox.SelectedText);  
  
             }  
          }  
          catch  
          {  
             MessageBox.Show("You need to select a RichTextBox.");  
          }  
       }  
    }  
  
    ```  
  
## Vedere anche  
 [Applicazioni MDI \(Interfaccia a documenti multipli, Multiple\-Document Interface\)](../../../../docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md)   
 [Procedura: creare form padre MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [Procedura: creare form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [Procedura: inviare dati al figlio MDI attivo](../../../../docs/framework/winforms/advanced/how-to-send-data-to-the-active-mdi-child.md)   
 [Procedura: disporre i form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-arrange-mdi-child-forms.md)