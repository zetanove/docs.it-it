---
title: "Procedura: visualizzare un elenco di tipi di carattere con il componente FontDialog | Microsoft Docs"
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
  - "Tipo di carattere (finestra di dialogo), visualizzazione"
  - "Font (proprietà), impostazione con il componente FontDialog"
  - "FontDialog (componente) [Windows Form]"
  - "tipi di carattere, attributi"
  - "tipi di carattere, selezione"
  - "tipi di carattere, visualizzazione dell'elenco"
ms.assetid: 35692c1b-0937-4b7a-9207-1ae6bdc244a0
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: visualizzare un elenco di tipi di carattere con il componente FontDialog
Il componente [FontDialog](../../../../docs/framework/winforms/controls/fontdialog-component-windows-forms.md) consente agli utenti di selezionare un tipo di carattere, nonché di modificarne la visualizzazione, ad esempio lo spessore e le dimensioni.  
  
 Il tipo di carattere selezionato nella finestra di dialogo viene restituito nella proprietà <xref:System.Windows.Forms.FontDialog.Font%2A>.  Sfruttare il tipo di carattere selezionato dall'utente è semplice come leggere una proprietà.  
  
### Per selezionare le proprietà dei tipi di carattere mediante il componente FontDialog  
  
1.  Aprire la finestra di dialogo mediante il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>.  
  
2.  Utilizzare la proprietà <xref:System.Windows.Forms.DialogResult> per determinare in che modo è stata chiusa la finestra di dialogo.  
  
3.  Utilizzare la proprietà <xref:System.Windows.Forms.FontDialog.Font%2A> per impostare il tipo di carattere desiderato.  
  
     Nell'esempio che segue viene utilizzato il gestore eventi <xref:System.Windows.Forms.Control.Click> del controllo <xref:System.Windows.Forms.Button> per aprire un componente <xref:System.Windows.Forms.FontDialog>.  Quando viene scelto un tipo di carattere e si fa clic su **OK**, la proprietà <xref:System.Windows.Forms.FontDialog.Font%2A> di un controllo <xref:System.Windows.Forms.TextBox> presente sul form viene impostata sul tipo di carattere scelto.  Si presuppone che il form contenga un controllo <xref:System.Windows.Forms.Button>, un controllo <xref:System.Windows.Forms.TextBox> e un componente <xref:System.Windows.Forms.FontDialog>.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       If FontDialog1.ShowDialog() = DialogResult.OK Then  
          TextBox1.Font = FontDialog1.Font  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(fontDialog1.ShowDialog() == DialogResult.OK)  
       {  
          textBox1.Font = fontDialog1.Font;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if(fontDialog1->ShowDialog() == DialogResult::OK)  
          {  
             textBox1->Font = fontDialog1->Font;  
          }  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore dell'evento.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.FontDialog>   
 [Componente FontDialog](../../../../docs/framework/winforms/controls/fontdialog-component-windows-forms.md)