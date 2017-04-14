---
title: "Cenni preliminari sul controllo TextBox (Windows Form) | Microsoft Docs"
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
  - "TextBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "caselle di testo, aggiunta"
  - "TextBox (controllo) [Windows Form], informazioni sui controlli TextBox"
ms.assetid: d1a9c7f5-fa53-480a-a75c-158f8649ea2f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul controllo TextBox (Windows Form)
Le caselle di testo di Windows Form vengono utilizzate per ricevere l'input dall'utente o per la visualizzazione di testo.  Il controllo <xref:System.Windows.Forms.TextBox> viene in genere utilizzato per il testo modificabile, anche se è possibile definire il testo in modo che risulti in sola lettura.  Le caselle di testo possono visualizzare più righe, mandare il testo a capo in base alle dimensioni del controllo e aggiungere formattazione di base.  Il controllo <xref:System.Windows.Forms.TextBox> fornisce un unico stile di formattazione per il testo visualizzato o inserito nel controllo.  Per visualizzare più tipi di testo formattato, utilizzare il controllo <xref:System.Windows.Forms.RichTextBox>.  Per ulteriori informazioni, vedere [Cenni preliminari sul controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-overview-windows-forms.md).  
  
## Utilizzo del controllo TextBox  
 Il testo visualizzato dal controllo è contenuto nella proprietà <xref:System.Windows.Forms.TextBox.Text%2A>.  In base all'impostazione predefinita, è possibile inserire in una casella di testo un massimo di 2048 caratteri.  Se si imposta la proprietà <xref:System.Windows.Forms.TextBox.Multiline%2A> su `true`, è possibile inserire fino a un massimo di 32 KB di testo.  È possibile impostare la proprietà <xref:System.Windows.Forms.TextBox.Text%2A> in fase di progettazione nella finestra Proprietà, in fase di esecuzione nel codice o tramite l'input dell'utente.  Il contenuto corrente di una casella di testo può essere recuperato in fase di esecuzione mediante la lettura delle informazioni contenute nella proprietà <xref:System.Windows.Forms.TextBox.Text%2A>.  
  
 Nell'esempio di codice seguente il testo viene impostato nel controllo in fase di esecuzione.  La routine `InitializeMyControl`  non viene eseguita automaticamente, ma deve essere richiamata.  
  
```vb  
Private Sub InitializeMyControl()  
   ' Put some text into the control first.  
   TextBox1.Text = "This is a TextBox control."  
End Sub  
  
```  
  
```csharp  
private void InitializeMyControl() {  
   // Put some text into the control first.  
   textBox1.Text = "This is a TextBox control.";  
}  
  
```  
  
```cpp  
private:  
   void InitializeMyControl()  
   {  
      // Put some text into the control first.  
      textBox1->Text = "This is a TextBox control.";  
   }  
```  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextBox>   
 [Procedura: controllare il punto di inserimento in un controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo Password con il controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo in sola lettura](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [Procedura: inserire virgolette in una stringa](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [Procedura: selezionare testo nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [Procedura: visualizzare più righe nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [Controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)