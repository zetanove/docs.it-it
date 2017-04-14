---
title: "Procedura: impostare l&#39;immagine visualizzata da un controllo Windows Form | Microsoft Docs"
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
  - "Button (controllo) [Windows Form], immagini"
  - "controlli [Windows Form], immagini"
  - "esempi [Windows Form], controlli"
  - "immagini [Windows Form], controlli Windows Form"
  - "controlli Windows Form, immagini"
ms.assetid: 9445af8f-4f62-48b0-a3f6-068058964b9f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: impostare l&#39;immagine visualizzata da un controllo Windows Form
In numerosi controlli Windows Form possono essere visualizzate immagini.  Tali immagini possono corrispondere a icone che illustrano la finalità del controllo, ad esempio l'icona di un dischetto su un pulsante indica il comando **Salva**.  In alternativa le icone possono corrispondere a immagini di sfondo per fornire al controllo l'aspetto e il comportamento desiderati.  
  
### Per impostare l'immagine visualizzata da un controllo  
  
1.  Impostare la proprietà `Image` o `BackgroundImage` del controllo su un oggetto di tipo <xref:System.Drawing.Image>.  L'immagine viene di solito caricata da un file mediante il metodo <xref:System.Drawing.Image.FromFile%2A>.  
  
     Nell'esempio di codice riportato di seguito il percorso impostato per la posizione dell'immagine corrisponde alla cartella **Immagini**,  inclusa nella maggior parte dei computer che eseguono un sistema operativo Windows.  Questa impostazione consente inoltre agli utenti con livelli minimi di accesso al sistema di eseguire l'applicazione in modo sicuro.  Per l'esempio è necessario un form a cui sia già stato aggiunto il controllo <xref:System.Windows.Forms.PictureBox>.  
  
    ```vb  
    ' Replace the image named below  
    ' with an icon of your own choosing.  
    PictureBox1.Image = Image.FromFile _  
       (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.MyPictures) _  
       & "\Image.gif")  
  
    ```  
  
    ```csharp  
    // Replace the image named below  
    // with an icon of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    pictureBox1.Image = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.MyPictures)  
       + @"\Image.gif");  
  
    ```  
  
    ```cpp  
    // Replace the image named below  
    // with an icon of your own choosing.  
    pictureBox1->Image = Image::FromFile(String::Concat  
       (System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::MyPictures),  
       "\\Image.gif"));  
    ```  
  
## Vedere anche  
 <xref:System.Drawing.Image.FromFile%2A>   
 <xref:System.Drawing.Image>   
 <xref:System.Windows.Forms.Control.BackgroundImage%2A>