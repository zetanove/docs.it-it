---
title: "Procedura: inserire virgolette in una stringa (Windows Form) | Microsoft Docs"
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
  - "virgolette"
  - "virgolette, aggiunta a stringhe in caselle di testo"
  - "TextBox (controllo) [Windows Form], visualizzazione di virgolette"
ms.assetid: 68bdc3f3-4177-4eab-99cd-cac17a82b515
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: inserire virgolette in una stringa (Windows Form)
Talvolta è opportuno inserire virgolette \(" "\) in una stringa di testo.  Di seguito è riportato un esempio:  
  
 She said, "You deserve a treat\!"  
  
 In alternativa, è anche possibile utilizzare il campo <xref:Microsoft.VisualBasic.ControlChars.Quote> come costante.  
  
### Per inserire le virgolette in una stringa all'interno del codice  
  
1.  In [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] inserire due virgolette in una riga come virgolette incorporate.  In [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)] inserire la sequenza di escape \\" come virgolette incorporate.  Ad esempio, per creare la stringa sopra indicata, utilizzare il codice riportato di seguito.  
  
    ```vb  
    Private Sub InsertQuote()  
       TextBox1.Text = "She said, ""You deserve a treat!"" "  
    End Sub  
  
    ```  
  
    ```csharp  
    private void InsertQuote(){  
       textBox1.Text = "She said, \"You deserve a treat!\" ";  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void InsertQuote()  
       {  
          textBox1->Text = "She said, \"You deserve a treat!\" ";  
       }  
    ```  
  
     In alternativa  
  
2.  Inserire il carattere ASCII o Unicode per le virgolette.  In [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] utilizzare il carattere ASCII \(34\).  In [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] utilizzare il carattere Unicode \(\\u0022\).  
  
    ```vb  
    Private Sub InsertAscii()  
       TextBox1.Text = "She said, " & Chr(34) & "You deserve a treat!" & Chr(34)  
    End Sub  
  
    ```  
  
    ```csharp  
    private void InsertAscii(){  
       textBox1.Text = "She said, " + '\u0022' + "You deserve a treat!" + '\u0022';  
    }  
    ```  
  
    > [!NOTE]
    >  In questo esempio non è possibile utilizzare \\u0022 perché non è consentito l'uso di un nome universale che indica un carattere presente nel set di caratteri di base.  In caso contrario si otterrebbe C3851.  Per ulteriori informazioni, vedere [Errore del compilatore C3851](../Topic/Compiler%20Error%20C3851.md).  
  
     In alternativa  
  
3.  È inoltre possibile definire una costante per il carattere, da utilizzare quando è necessario.  
  
    ```vb  
    Const quote As String = """"  
    TextBox1.Text = "She said, " & quote & "You deserve a treat!" & quote  
  
    ```  
  
    ```csharp  
    const string quote = "\"";  
    textBox1.Text = "She said, " + quote +  "You deserve a treat!"+ quote ;  
  
    ```  
  
    ```cpp  
    const String^ quote = "\"";  
    textBox1->Text = String::Concat("She said, ",  
       const_cast<String^>(quote), "You deserve a treat!",  
       const_cast<String^>(quote));  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextBox>   
 <xref:Microsoft.VisualBasic.ControlChars.Quote>   
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [Procedura: controllare il punto di inserimento in un controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo Password con il controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo in sola lettura](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [Procedura: selezionare testo nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [Procedura: visualizzare più righe nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [Controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)