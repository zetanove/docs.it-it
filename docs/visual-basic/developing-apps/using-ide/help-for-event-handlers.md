---
title: "Help for Event Handlers in Visual Basic Code | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CheckedListBox1_SelectedIndexChanged"
  - "Calendar1_SelectionChanged"
  - "Form1_Load"
  - "DropDownList1_SelectedIndexChanged"
  - "TextBox1_TextChanged"
  - "ListBox1_SelectedIndexChanged"
  - "TreeView1_AfterSelect"
  - "MaskedTextBox1_MaskInputRejected"
  - "Menu1_MenuItemClick"
  - "TabPage1_Click"
  - "LinkButton1_Click"
  - "CheckBoxList1_SelectedIndexChanged"
  - "ProgressBar1_Click"
  - "ToolStripButton1_Click"
  - "ImageButton1_Click"
  - "RadioButtonList1_SelectedIndexChanged"
  - "PictureBox1_Click"
  - "Label1_Click"
  - "ToolStrip1_ItemClicked"
  - "RichTextBox1_TextChanged"
  - "ListView1_SelectedIndexChanged"
  - "PrintPreviewControl1_Click"
  - "ComboBox1_SelectedIndexChanged"
  - "Button1_Click"
  - "Page_Load"
  - "TrackBar1_Scroll"
  - "WebBrowser1_DocumentCompleted"
  - "TreeView1_SelectedNodeChanged"
  - "CheckBox1_CheckedChanged"
  - "RadioButton1_CheckedChanged"
  - "NotifyIcon1_MouseDown"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "event handlers, getting F1 Help in Visual Basic code"
ms.assetid: 2c92decf-844e-4ba4-82c7-f2fc0adc3002
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Help for Event Handlers in Visual Basic Code
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Per visualizzare le informazioni della Guida relative a un determinato gestore eventi mentre è attiva la finestra dell'editor di codice, posizionare il cursore sulla clausola `Handles` alla fine della routine evento, quindi premere F1.  Nell'istruzione `Form1_Load` seguente, ad esempio, la posizione corretta per il cursore è `MyBase.Load`:  
  
```  
Private Sub Form1_Load(ByVal sender As System.Object,   
    ByVal e As System.EventArgs) Handles MyBase.Load  
  
End Sub  
```  
  
## Vedere anche  
 [Eventi](../Topic/Handling%20and%20Raising%20Events.md)   
 [Event Handlers Overview](../Topic/Event%20Handlers%20Overview%20\(Windows%20Forms\).md)