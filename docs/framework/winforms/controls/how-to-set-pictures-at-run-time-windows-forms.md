---
title: "Procedura: impostare le immagini in fase di esecuzione (Windows Form) | Microsoft Docs"
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
  - "bitmap [Windows Form], visualizzazione nel controllo PictureBox [Windows Form]"
  - "esempi [Windows Form], PictureBox (controllo)"
  - "immagini [Windows Form], aggiunta con il controllo PictureBox [Windows Form]"
  - "PictureBox (controllo) [Windows Form], aggiunta di immagini"
  - "PictureBox (controllo) [Windows Form], aggiunta di immagini"
  - "immagini, impostazione della visualizzazione"
ms.assetid: 18ca41d0-68a5-4660-985e-a6c1fbc01d76
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: impostare le immagini in fase di esecuzione (Windows Form)
È possibile impostare a livello di codice l'immagine visualizzata da un controllo <xref:System.Windows.Forms.PictureBox> Windows Form.  
  
### Per impostare un'immagine a livello di codice  
  
-   Impostare la proprietà <xref:System.Windows.Forms.PictureBox.Image%2A> tramite il metodo <xref:System.Drawing.Image.FromFile%2A> della classe <xref:System.Drawing.Image>.  
  
     Nell'esempio seguente il percorso impostato per la posizione dell'immagine coincide con la cartella Documenti.  Questa scelta è dovuta al fatto che si suppone che questa directory sia presente sulla maggior parte dei computer con sistema operativo Windows.  La scelta di questa posizione consente inoltre di eseguire l'applicazione senza problemi agli utenti che dispongono di livelli di accesso minimo.  Nell'esempio riportato di seguito si presuppone che un controllo <xref:System.Windows.Forms.PictureBox> sia già stato aggiunto al form.  
  
    ```vb  
    Private Sub LoadNewPict()  
       ' You should replace the bold image   
       ' in the sample below with an icon of your own choosing.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void LoadNewPict(){  
       // You should replace the bold image   
       // in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       pictureBox1.Image = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void LoadNewPict()  
       {  
          // You should replace the bold image   
          // in the sample below with an icon of your own choosing.  
          pictureBox1->Image = Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
       }  
    ```  
  
### Per cancellare un'immagine  
  
-   Rilasciare innanzitutto la memoria utilizzata dall'immagine, quindi cancellare l'oggetto grafico.  In caso di problemi di gestione della memoria, sarà possibile utilizzare successivamente la procedura di Garbage Collection.  
  
    ```vb  
    If Not (PictureBox1.Image Is Nothing) Then  
       PictureBox1.Image.Dispose()  
       PictureBox1.Image = Nothing  
    End If  
  
    ```  
  
    ```csharp  
    if (pictureBox1.Image != null)   
    {  
       pictureBox1.Image.Dispose();  
       pictureBox1.Image = null;  
    }  
  
    ```  
  
    ```cpp  
    if (pictureBox1->Image != nullptr)  
    {  
       pictureBox1->Image->Dispose();  
       pictureBox1->Image = nullptr;  
    }  
    ```  
  
    > [!NOTE]
    >  Per ulteriori informazioni sui motivi per i quali è preferibile utilizzare il metodo <xref:System.Drawing.Image.Dispose%2A> in questo modo, vedere [Cleaning Up Unmanaged Resources](../../../../docs/standard/garbage-collection/unmanaged.md).  
  
     Con questo codice l'immagine verrà cancellata anche se è stata caricata nel controllo in fase di progettazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.PictureBox>   
 <xref:System.Drawing.Image.FromFile%2A?displayProperty=fullName>   
 [Cenni preliminari sul controllo PictureBox](../../../../docs/framework/winforms/controls/picturebox-control-overview-windows-forms.md)   
 [Procedura: caricare un'immagine utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/how-to-load-a-picture-using-the-designer-windows-forms.md)   
 [Procedura: modificare le dimensioni o la posizione di un'immagine in fase di esecuzione](../../../../docs/framework/winforms/controls/how-to-modify-the-size-or-placement-of-a-picture-at-run-time-windows-forms.md)   
 [Controllo PictureBox](../../../../docs/framework/winforms/controls/picturebox-control-windows-forms.md)