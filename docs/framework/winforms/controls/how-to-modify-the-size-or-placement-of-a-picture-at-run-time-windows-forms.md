---
title: "Procedura: modificare le dimensioni o la posizione di un&#39;immagine in fase di esecuzione (Windows Form) | Microsoft Docs"
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
  - "esempi [Windows Form], PictureBox (controllo)"
  - "immagini [Windows Form], controllo del posizionamento nel controllo PictureBox [Windows Form]"
  - "PictureBox (controllo) [Windows Form], dimensioni e allineamento di immagini"
  - "immagini, controllo del posizionamento nel controllo PictureBox [Windows Form]"
ms.assetid: d0b332a3-fae2-4891-957c-dc3e17743326
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: modificare le dimensioni o la posizione di un&#39;immagine in fase di esecuzione (Windows Form)
Se si desidera utilizzare il controllo <xref:System.Windows.Forms.PictureBox> di Windows Form in un form, è possibile impostarne la proprietà <xref:System.Windows.Forms.PictureBox.SizeMode%2A> su:  
  
-   Allineare l'angolo superiore sinistro dell'immagine con l'angolo superiore sinistro del controllo.  
  
-   Centrare l'immagine all'interno del controllo.  
  
-   Regolare le dimensioni del controllo in modo che possa contenere l'immagine da visualizzare.  
  
-   Estendere l'eventuale immagine visualizzata dal controllo in modo che corrisponda alle dimensioni del controllo stesso.  
  
 L'estensione di un'immagine, soprattutto se in formato bitmap, può causare una perdita di qualità.  Rispetto alle immagini bitmap, i metafile, che sono elenchi di istruzioni grafiche per la creazione di immagini in fase di esecuzione, risultano più adatti a essere estesi.  
  
### Per impostare la proprietà SizeMode in fase di esecuzione  
  
1.  Impostare <xref:System.Windows.Forms.PictureBox.SizeMode%2A> su <xref:System.Windows.Forms.PictureBoxSizeMode> \(impostazione predefinita\), <xref:System.Windows.Forms.PictureBoxSizeMode>, <xref:System.Windows.Forms.PictureBoxSizeMode> o <xref:System.Windows.Forms.PictureBoxSizeMode>.  Se si imposta su <xref:System.Windows.Forms.PictureBoxSizeMode>, l'immagine viene inserita nell'angolo superiore sinistro del controllo. Se l'immagine è più grande del controllo, i bordi inferiore e destro vengono tagliati.  Se si imposta su <xref:System.Windows.Forms.PictureBoxSizeMode>, l'immagine viene allineata al centro nel controllo. Se l'immagine è più grande del controllo, i bordi esterni dell'immagine vengono tagliati.  Se si imposta su <xref:System.Windows.Forms.PictureBoxSizeMode>, le dimensioni del controllo vengono adattate alle dimensioni dell'immagine.  Se si imposta su <xref:System.Windows.Forms.PictureBoxSizeMode>, avviene il contrario, ovvero le dimensioni dell'immagine vengono adattate alle dimensioni del controllo.  
  
     Nell'esempio seguente il percorso impostato per la posizione dell'immagine coincide con la cartella Documenti.  Questa scelta è dovuta al fatto che si suppone che questa directory sia presente sulla maggior parte dei computer con sistema operativo Windows.  La scelta di questa posizione consente inoltre di eseguire l'applicazione senza problemi agli utenti che dispongono di livelli di accesso minimo.  Nell'esempio riportato di seguito si presuppone che un controllo <xref:System.Windows.Forms.PictureBox> sia già stato aggiunto al form.  
  
    ```vb  
    Private Sub StretchPic()  
       ' Stretch the picture to fit the control.  
       PictureBox1.SizeMode = PictureBoxSizeMode.StretchImage  
       ' Load the picture into the control.  
       ' You should replace the bold image   
       ' in the sample below with an icon of your own choosing.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Image.gif")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void StretchPic(){  
       // Stretch the picture to fit the control.  
       PictureBox1.SizeMode = PictureBoxSizeMode.StretchImage;  
       // Load the picture into the control.  
       // You should replace the bold image   
       // in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       + @"\Image.gif")  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void StretchPic()  
       {  
          // Stretch the picture to fit the control.  
          pictureBox1->SizeMode = PictureBoxSizeMode::StretchImage;  
          // Load the picture into the control.  
          // You should replace the bold image   
          // in the sample below with an icon of your own choosing.  
          pictureBox1->Image = Image::FromFile(String::Concat(  
             System::Environment::GetFolderPath(  
             System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.PictureBox>   
 [Procedura: caricare un'immagine utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/how-to-load-a-picture-using-the-designer-windows-forms.md)   
 [Cenni preliminari sul controllo PictureBox](../../../../docs/framework/winforms/controls/picturebox-control-overview-windows-forms.md)   
 [Procedura: impostare le immagini in fase di esecuzione](../../../../docs/framework/winforms/controls/how-to-set-pictures-at-run-time-windows-forms.md)   
 [Controllo PictureBox](../../../../docs/framework/winforms/controls/picturebox-control-windows-forms.md)