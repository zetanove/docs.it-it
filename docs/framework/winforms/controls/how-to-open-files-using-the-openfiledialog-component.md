---
title: "Procedura: aprire file con il componente OpenFileDialog | Microsoft Docs"
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
  - "file, apertura mediante il componente OpenFileDialog"
  - "OpenFile (metodo)"
  - "OpenFile (metodo), OpenFileDialog (componente)"
  - "OpenFileDialog (componente), apertura di file"
ms.assetid: 9d88367a-cc21-4ffd-be74-89fd63767d35
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: aprire file con il componente OpenFileDialog
Il componente <xref:System.Windows.Forms.OpenFileDialog> consente di sfogliare le cartelle del proprio computer o di altri computer in rete e di selezionare uno o più file da aprire.  Nella finestra di dialogo vengono restituiti il percorso e il nome del file selezionato dall'utente.  
  
 Una volta selezionato il file da aprire, è possibile procedere all'apertura del file in due modi.  Se si preferisce utilizzare flussi di file, creare un'istanza della classe <xref:System.IO.StreamReader>.  In alternativa, è possibile utilizzare il metodo <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> per aprire il file selezionato.  
  
 Nel primo esempio qui di seguito, è previsto un controllo di autorizzazione <xref:System.Security.Permissions.FileIOPermission>, come descritto nella "Nota sulla sicurezza", ma viene consentito l'accesso al nome file.  Questa tecnica può essere utilizzata dal computer locale, dalla Intranet e da Internet.  Anche il secondo metodo prevede un controllo di autorizzazione <xref:System.Security.Permissions.FileIOPermission>, ma è più indicato per applicazioni in area Intranet o Internet.  
  
### Per aprire un file come flusso mediante il componente OpenFileDialog  
  
1.  Aprire la finestra di dialogo **Apri file** e chiamare un metodo per aprire il file selezionato dall'utente.  
  
     Un approccio consiste nell'utilizzo del metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> per visualizzare la finestra di dialogo Apri file e di un'istanza della classe <xref:System.IO.StreamReader> per aprire il file.  
  
     Nell'esempio che segue viene utilizzato il gestore eventi <xref:System.Windows.Forms.Control.Click> del controllo <xref:System.Windows.Forms.Button> per aprire un'istanza del componente <xref:System.Windows.Forms.OpenFileDialog>.  Quando viene scelto un file e l'utente fa clic su **OK**, il file selezionato nella finestra di dialogo si apre.  In questo caso, il contenuto viene visualizzato in una finestra di messaggio per indicare che il flusso di file è stato letto.  
  
    > [!IMPORTANT]
    >  Per ottenere o impostare la proprietà <xref:System.Windows.Forms.FileDialog.FileName%2A>, l'assembly richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>.  Se viene eseguito in un contesto ad affidabilità parziale, il processo può generare un'eccezione a causa dell'insufficienza di privilegi.  Per ulteriori informazioni, vedere [Nozioni fondamentali sulla sicurezza per l'accesso al codice](../../../../docs/framework/misc/code-access-security-basics.md).  
  
     Nell'esempio si presuppone che il form contenga un controllo <xref:System.Windows.Forms.Button> e un componente <xref:System.Windows.Forms.OpenFileDialog>.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       If OpenFileDialog1.ShowDialog() = System.Windows.Forms.DialogResult.OK Then  
         Dim sr As New System.IO.StreamReader(OpenFileDialog1.FileName)  
         MessageBox.Show(sr.ReadToEnd)  
         sr.Close()  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       if(openFileDialog1.ShowDialog() == System.Windows.Forms.DialogResult.OK)  
       {  
          System.IO.StreamReader sr = new   
             System.IO.StreamReader(openFileDialog1.FileName);  
          MessageBox.Show(sr.ReadToEnd());  
          sr.Close();  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          if(openFileDialog1->ShowDialog() == System::Windows::Forms::DialogResult::OK)  
          {  
             System::IO::StreamReader ^ sr = gcnew  
                System::IO::StreamReader(openFileDialog1->FileName);  
             MessageBox::Show(sr->ReadToEnd());  
             sr->Close();  
          }  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore dell'evento.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
    > [!NOTE]
    >  Per ulteriori informazioni sulla lettura da flussi di file, vedere [Metodo FileStream.BeginRead](frlrfSystemIOFileStreamClassBeginReadTopic) e [Metodo FileStream.Read](https://msdn.microsoft.com/en-us/library/system.io.filestream.read.aspx).  
  
### Per aprire un file come file mediante il componente OpenFileDialog  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> per visualizzare la finestra di dialogo e il metodo <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> per aprire il file.  
  
     Il metodo <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> del componente <xref:System.Windows.Forms.OpenFileDialog> restituisce i byte che compongono il file  e che forniscono un flusso da cui leggere.  Nell'esempio che segue, viene creata un'istanza del componente <xref:System.Windows.Forms.OpenFileDialog> con un filtro cursore su di esso, per consentire all'utente di scegliere solo i file con estensione `.cur`.  Se si sceglie un file `.cur` , il cursore del form viene impostato sul cursore selezionato.  
  
    > [!IMPORTANT]
    >  Per chiamare il metodo <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A>, l'assembly richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>.  Se viene eseguito in un contesto ad affidabilità parziale, il processo può generare un'eccezione a causa dell'insufficienza di privilegi.  Per ulteriori informazioni, vedere [Nozioni fondamentali sulla sicurezza per l'accesso al codice](../../../../docs/framework/misc/code-access-security-basics.md).  
  
     Nell'esempio si presuppone che il form contenga un controllo <xref:System.Windows.Forms.Button>.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       ' Displays an OpenFileDialog so the user can select a Cursor.  
       Dim openFileDialog1 As New OpenFileDialog()  
       openFileDialog1.Filter = "Cursor Files|*.cur"  
       openFileDialog1.Title = "Select a Cursor File"  
  
       ' Show the Dialog.  
       ' If the user clicked OK in the dialog and   
       ' a .CUR file was selected, open it.  
       If openFileDialog1.ShowDialog() = System.Windows.Forms.DialogResult.OK Then  
         ' Assign the cursor in the Stream to the Form's Cursor property.  
         Me.Cursor = New Cursor(openFileDialog1.OpenFile())  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // Displays an OpenFileDialog so the user can select a Cursor.  
       OpenFileDialog openFileDialog1 = new OpenFileDialog();  
       openFileDialog1.Filter = "Cursor Files|*.cur";  
       openFileDialog1.Title = "Select a Cursor File";  
  
       // Show the Dialog.  
       // If the user clicked OK in the dialog and  
       // a .CUR file was selected, open it.  
        if (openFileDialog1.ShowDialog() == System.Windows.Forms.DialogResult.OK)  
       {  
          // Assign the cursor in the Stream to the Form's Cursor property.  
          this.Cursor = new Cursor(openFileDialog1.OpenFile());  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Displays an OpenFileDialog so the user can select a Cursor.  
          OpenFileDialog ^ openFileDialog1 = new OpenFileDialog();  
          openFileDialog1->Filter = "Cursor Files|*.cur";  
          openFileDialog1->Title = "Select a Cursor File";  
  
          // Show the Dialog.  
          // If the user clicked OK in the dialog and  
          // a .CUR file was selected, open it.  
          if (openFileDialog1->ShowDialog() == System::Windows::Forms::DialogResult::OK)  
          {  
             // Assign the cursor in the Stream to  
             // the Form's Cursor property.  
             this->Cursor = gcnew  
                System::Windows::Forms::Cursor(  
                openFileDialog1->OpenFile());  
          }  
       }  
  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore dell'evento.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.OpenFileDialog>   
 [Componente OpenFileDialog](../../../../docs/framework/winforms/controls/openfiledialog-component-windows-forms.md)