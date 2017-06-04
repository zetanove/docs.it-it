---
title: "Procedura: salvare file con il componente SaveFileDialog | Microsoft Docs"
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
  - "file, salvataggio"
  - "OpenFile (metodo), salvataggio di file con il componente SaveFileDialog"
  - "SaveFileDialog (componente), salvataggio di file"
  - "salvataggio di file"
ms.assetid: 02e8f409-b83f-4707-babb-e71f6b223d90
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: salvare file con il componente SaveFileDialog
Il componente <xref:System.Windows.Forms.SaveFileDialog> consente agli utenti di sfogliare il file system e selezionare i file da salvare.  Nella finestra di dialogo vengono restituiti il percorso e il nome del file selezionato dall'utente.  È tuttavia necessario scrivere il codice per salvare effettivamente i file sul disco.  
  
### Per salvare un file mediante il componente SaveFileDialog  
  
-   Aprire la finestra di dialogo **Salva file** e chiamare un metodo per salvare il file selezionato dall'utente.  
  
     Utilizzare il metodo <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> del componente <xref:System.Windows.Forms.SaveFileDialog> per salvare il file.  Con questo metodo, viene reso disponibile un oggetto <xref:System.IO.Stream> in cui scrivere.  
  
     Nell'esempio seguente viene utilizzata la proprietà <xref:System.Windows.Forms.DialogResult> per ottenere il nome del file e il metodo <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> per salvarlo.  Con il metodo <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> viene fornito un flusso su cui scrivere il file.  
  
     Nell'esempio qui di seguito, è presente un controllo <xref:System.Windows.Forms.Button> a cui è assegnata un'immagine.  Quando si fa clic sul pulsante, viene creata un'istanza del componente <xref:System.Windows.Forms.SaveFileDialog> con un filtro che ammette file di tipo GIF, JPEG e BMP.  Se si seleziona un file di questo tipo nella finestra di dialogo Salva file, viene salvata l'immagine del pulsante.  
  
    > [!IMPORTANT]
    >  Per ottenere o impostare la proprietà <xref:System.Windows.Forms.FileDialog.FileName%2A>, l'assembly richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>.  Se viene eseguito in un contesto ad affidabilità parziale, il processo può generare un'eccezione a causa dell'insufficienza di privilegi.  Per ulteriori informazioni, vedere [Nozioni fondamentali sulla sicurezza per l'accesso al codice](../../../../docs/framework/misc/code-access-security-basics.md).  
  
     Nell'esempio si presuppone che il form contenga un controllo <xref:System.Windows.Forms.Button> con la relativa proprietà <xref:System.Windows.Forms.ButtonBase.Image%2A> impostata su un file di tipo GIF, JPEG o BMP.  
  
    > [!NOTE]
    >  La proprietà <xref:System.Windows.Forms.FileDialog.FilterIndex%2A> della classe <xref:System.Windows.Forms.FileDialog>, che a causa dell'eredità fa parte della classe <xref:System.Windows.Forms.SaveFileDialog>, utilizza un indice in base uno,  caratteristica importante se si scrive codice per salvare i dati in un formato specifico, ad esempio per salvare un file come testo normale invece che in formato binario.  Questa proprietà è illustrata nell'esempio che segue.  
  
    ```vb  
    Private Sub Button2_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button2.Click  
       ' Displays a SaveFileDialog so the user can save the Image  
       ' assigned to Button2.  
       Dim saveFileDialog1 As New SaveFileDialog()  
       saveFileDialog1.Filter = "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif"  
       saveFileDialog1.Title = "Save an Image File"  
       saveFileDialog1.ShowDialog()  
  
       ' If the file name is not an empty string open it for saving.  
       If saveFileDialog1.FileName <> "" Then  
          ' Saves the Image via a FileStream created by the OpenFile method.  
          Dim fs As System.IO.FileStream = Ctype _  
             (saveFileDialog1.OpenFile(), System.IO.FileStream)  
          ' Saves the Image in the appropriate ImageFormat based upon the  
          ' file type selected in the dialog box.  
          ' NOTE that the FilterIndex property is one-based.  
          Select Case saveFileDialog1.FilterIndex  
             Case 1  
                Me.button2.Image.Save(fs, _  
                   System.Drawing.Imaging.ImageFormat.Jpeg)  
  
             Case 2  
                Me.button2.Image.Save(fs, _  
                   System.Drawing.Imaging.ImageFormat.Bmp)  
  
             Case 3  
                Me.button2.Image.Save(fs, _  
                   System.Drawing.Imaging.ImageFormat.Gif)  
           End Select  
  
           fs.Close()  
        End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button2_Click(object sender, System.EventArgs e)  
    {  
       // Displays a SaveFileDialog so the user can save the Image  
       // assigned to Button2.  
       SaveFileDialog saveFileDialog1 = new SaveFileDialog();  
       saveFileDialog1.Filter = "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif";  
       saveFileDialog1.Title = "Save an Image File";  
       saveFileDialog1.ShowDialog();  
  
       // If the file name is not an empty string open it for saving.  
       if(saveFileDialog1.FileName != "")  
       {  
          // Saves the Image via a FileStream created by the OpenFile method.  
          System.IO.FileStream fs =   
             (System.IO.FileStream)saveFileDialog1.OpenFile();  
          // Saves the Image in the appropriate ImageFormat based upon the  
          // File type selected in the dialog box.  
          // NOTE that the FilterIndex property is one-based.  
          switch(saveFileDialog1.FilterIndex)  
          {  
             case 1 :   
             this.button2.Image.Save(fs,   
                System.Drawing.Imaging.ImageFormat.Jpeg);  
             break;  
  
             case 2 :   
             this.button2.Image.Save(fs,   
                System.Drawing.Imaging.ImageFormat.Bmp);  
             break;  
  
             case 3 :   
             this.button2.Image.Save(fs,   
                System.Drawing.Imaging.ImageFormat.Gif);  
             break;  
          }  
  
       fs.Close();  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void button2_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Displays a SaveFileDialog so the user can save the Image  
          // assigned to Button2.  
          SaveFileDialog ^ saveFileDialog1 = new SaveFileDialog();  
          saveFileDialog1->Filter =   
             "JPeg Image|*.jpg|Bitmap Image|*.bmp|Gif Image|*.gif";  
          saveFileDialog1->Title = "Save an Image File";  
          saveFileDialog1->ShowDialog();  
          // If the file name is not an empty string, open it for saving.  
          if(saveFileDialog1->FileName != "")  
          {  
             // Saves the Image through a FileStream created by  
             // the OpenFile method.  
             System::IO::FileStream ^ fs =   
                safe_cast<System::IO::FileStream*>(  
                saveFileDialog1->OpenFile());  
             // Saves the Image in the appropriate ImageFormat based on  
             // the file type selected in the dialog box.  
             // Note that the FilterIndex property is one based.  
             switch(saveFileDialog1->FilterIndex)  
             {  
                case 1 :  
                   this->button2->Image->Save(fs,  
                      System::Drawing::Imaging::ImageFormat::Jpeg);  
                   break;  
                case 2 :  
                   this->button2->Image->Save(fs,   
                      System::Drawing::Imaging::ImageFormat::Bmp);  
                   break;  
                case 3 :  
                   this->button2->Image->Save(fs,   
                      System::Drawing::Imaging::ImageFormat::Gif);  
                   break;  
             }  
          fs->Close();  
          }  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore dell'evento.  
  
    ```csharp  
    this.button2.Click += new System.EventHandler(this.button2_Click);  
  
    ```  
  
    ```cpp  
    this->button2->Click += gcnew  
       System::EventHandler(this, &Form1::button2_Click);  
    ```  
  
     Per ulteriori informazioni sulla scrittura di flussi di file, vedere [Metodo FileStream.BeginWrite](frlrfSystemIOFileStreamClassBeginWriteTopic) e [Metodo FileStream.Write](https://msdn.microsoft.com/en-us/library/system.io.filestream.write.aspx).  
  
    > [!NOTE]
    >  Alcuni controlli, come <xref:System.Windows.Forms.RichTextBox>, consentono di salvare i file.  Per ulteriori informazioni, vedere la sezione "SaveFileDialog Component" dell'articolo tecnico di MSDN Online Library [Essential Code for Windows Forms Dialog Boxes](http://go.microsoft.com/fwlink/?LinkID=102575) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Forms.SaveFileDialog>   
 [Componente SaveFileDialog](../../../../docs/framework/winforms/controls/savefiledialog-component-windows-forms.md)