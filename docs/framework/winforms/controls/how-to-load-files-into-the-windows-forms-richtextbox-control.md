---
title: "Procedura: caricare file nel controllo RichTextBox Windows Form | Microsoft Docs"
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
  - "caselle di testo, visualizzazione di file"
  - "esempi [Windows Form], caselle di testo"
  - "rtf, apertura di file nel controllo RichTextBox"
  - "file rtf, apertura nel controllo RichTextBox"
  - "testo, visualizzazione di file nel controllo RichTextBox"
  - "rtf, visualizzazione di file nel controllo RichTextBox"
  - "RichTextBox (controllo) [Windows Form], apertura di file"
  - "file rtf, visualizzazione nel controllo RichTextBox"
ms.assetid: c03451be-f285-4428-a71a-c41e002cc919
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: caricare file nel controllo RichTextBox Windows Form
Il controllo <xref:System.Windows.Forms.RichTextBox> Windows Form consente di visualizzare un file come testo normale, testo normale Unicode o in formato RTF \(Rich\-Text Format\). Per eseguire questa operazione, chiamare il metodo <xref:System.Windows.Forms.RichTextBox.LoadFile%2A>. È anche possibile usare <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> per caricare dati da un flusso. Per altre informazioni, vedere <xref:System.Windows.Forms.RichTextBox.LoadFile%28System.IO.Stream%2CSystem.Windows.Forms.RichTextBoxStreamType%29>.  
  
### Per caricare un file nel controllo RichTextBox  
  
1.  Determinare il percorso del file da aprire usando il componente <xref:System.Windows.Forms.OpenFileDialog>. Per informazioni generali, vedere [Cenni preliminari sul componente OpenFileDialog](../../../../docs/framework/winforms/controls/openfiledialog-component-overview-windows-forms.md).  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.RichTextBox.LoadFile%2A><xref:System.Windows.Forms.RichTextBox> specificando il file da caricare e, facoltativamente, un tipo di file. Nell'esempio seguente il file da caricare viene preso dalla proprietà <xref:System.Windows.Forms.FileDialog.FileName%2A> del componente <xref:System.Windows.Forms.OpenFileDialog>. Se si chiama il metodo usando come unico argomento un nome di file, si presuppone che il tipo del file sia RTF. Per specificare un altro tipo di file, chiamare il metodo con un valore dell'enumerazione <xref:System.Windows.Forms.RichTextBoxStreamType> come secondo argomento.  
  
     Nell'esempio seguente viene visualizzato il componente <xref:System.Windows.Forms.OpenFileDialog> quando si fa clic su un pulsante. Il file selezionato viene quindi aperto e visualizzato nel controllo <xref:System.Windows.Forms.RichTextBox>. In questo esempio si presuppone l'esistenza di un form contenente un pulsante `btnOpenFile`.  
  
    ```vb  
    Private Sub btnOpenFile_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles btnOpenFile.Click  
         If OpenFileDialog1.ShowDialog() = DialogResult.OK Then  
           RichTextBox1.LoadFile(OpenFileDialog1.FileName, _  
              RichTextBoxStreamType.RichText)  
          End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void btnOpenFile_Click(object sender, System.EventArgs e)  
    {  
       if(openFileDialog1.ShowDialog() == DialogResult.OK)  
       {  
         richTextBox1.LoadFile(openFileDialog1.FileName, RichTextBoxStreamType.RichText);  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void btnOpenFile_Click(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          if(openFileDialog1->ShowDialog() == DialogResult::OK)  
          {  
             richTextBox1->LoadFile(openFileDialog1->FileName,  
                RichTextBoxStreamType::RichText);  
          }  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.btnOpenFile.Click += new System.EventHandler(this. btnOpenFile_Click);  
  
    ```  
  
    ```cpp  
    this->btnOpenFile->Click += gcnew   
       System::EventHandler(this, &Form1::btnOpenFile_Click);  
    ```  
  
    > [!IMPORTANT]
    >  Per eseguire questo processo, l'assembly può richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>. Se l'esecuzione avviene in un contesto parzialmente attendibile, è possibile che il processo generi un'eccezione dovuta a privilegi insufficienti. Per altre informazioni, vedere [Code Access Security Basics](../../../../docs/framework/misc/code-access-security-basics.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBox.LoadFile%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.RichTextBox>   
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)