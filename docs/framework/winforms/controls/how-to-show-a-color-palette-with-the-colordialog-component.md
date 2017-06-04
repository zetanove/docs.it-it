---
title: "Procedura: visualizzare una tavolozza dei colori con il componente ColorDialog | Microsoft Docs"
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
  - "finestra di dialogo dei colori, visualizzazione di tavolozze dei colori"
  - "tavolozze dei colori, finestra di dialogo"
  - "tavolozze dei colori, visualizzazione nel componente ColorDialog"
  - "Color (proprietà)"
  - "ColorDialog (componente), visualizzazione di tavolozze dei colori"
  - "colori, selezionabili dall'utente"
  - "colori, visualizzazione di tavolozze"
  - "tavolozze, visualizzazione di colori"
ms.assetid: ee050f61-dbc8-4436-ba22-51360981ab48
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: visualizzare una tavolozza dei colori con il componente ColorDialog
Il componente [ColorDialog](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md) visualizza una tavolozza dei colori e restituisce una proprietà contenente il colore selezionato dall'utente.  
  
### Per scegliere un colore mediante il componente ColorDialog  
  
1.  Aprire la finestra di dialogo mediante il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>.  
  
2.  Utilizzare la proprietà <xref:System.Windows.Forms.DialogResult> per determinare in che modo è stata chiusa la finestra di dialogo.  
  
3.  Utilizzare la proprietà <xref:System.Windows.Forms.ColorDialog.Color%2A> del componente <xref:System.Windows.Forms.ColorDialog> per impostare il colore scelto.  
  
     Nell'esempio che segue viene utilizzato il gestore eventi <xref:System.Windows.Forms.Control.Click> del controllo <xref:System.Windows.Forms.Button> per aprire un componente <xref:System.Windows.Forms.ColorDialog>.  Quando viene scelto un colore e si fa clic su **OK**, il colore di sfondo del controllo <xref:System.Windows.Forms.Button> viene impostato sul colore scelto.  Si presuppone che il form contenga un controllo <xref:System.Windows.Forms.Button> e un componente <xref:System.Windows.Forms.ColorDialog>.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button1.Click  
       If ColorDialog1.ShowDialog() = DialogResult.OK Then  
          Button1.BackColor = ColorDialog1.Color  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(colorDialog1.ShowDialog() == DialogResult.OK)  
       {  
          button1.BackColor = colorDialog1.Color;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,   
          System::EventArgs ^ e)  
       {  
          if(colorDialog1->ShowDialog() == DialogResult::OK)  
          {  
             button1->BackColor = colorDialog1->Color;  
          }  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click +=   
       gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ColorDialog>   
 [Componente ColorDialog](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md)