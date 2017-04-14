---
title: "Procedura: eseguire il rendering delle immagini con GDI+ | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "GDI+, rendering di immagini esistenti"
  - "immagini [Windows Form], creazione"
ms.assetid: c128b79a-3e31-47d8-9e66-3470f570a056
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: eseguire il rendering delle immagini con GDI+
È possibile utilizzare [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] per il rendering di immagini presenti nelle applicazioni sotto forma di file.  A questo scopo, è necessario creare un nuovo oggetto di una classe <xref:System.Drawing.Image>, ad esempio <xref:System.Drawing.Bitmap>, creare quindi un oggetto <xref:System.Drawing.Graphics> che faccia riferimento alla superficie di disegno da utilizzare, infine chiamare il metodo <xref:System.Drawing.Graphics.DrawImage%2A> dell'oggetto <xref:System.Drawing.Graphics>.  L'immagine verrà disegnata nella superficie di disegno rappresentata dalla classe Graphics.  È possibile utilizzare l'Editor immagini per creare e modificare file di immagine in fase di progettazione ed eseguirne il rendering con [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] in fase di esecuzione.  Per ulteriori informazioni, vedere [Image Editor for Icons](../Topic/Image%20Editor%20for%20Icons.md).  
  
### Per eseguire il rendering di un'immagine con GDI\+  
  
1.  Creare un oggetto che rappresenta l'immagine da visualizzare.  Tale oggetto deve essere membro di una classe che eredita da <xref:System.Drawing.Image>, ad esempio <xref:System.Drawing.Bitmap> o <xref:System.Drawing.Imaging.Metafile>.  Di seguito viene riportato un esempio:  
  
    ```vb  
    ' Uses the System.Environment.GetFolderPath to get the path to the   
    ' current user's MyPictures folder.  
    Dim myBitmap as New Bitmap _  
       (System.Environment.GetFolderPath _  
          (System.Environment.SpecialFolder.MyPictures))  
  
    ```  
  
    ```csharp  
    // Uses the System.Environment.GetFolderPath to get the path to the   
    // current user's MyPictures folder.  
    Bitmap myBitmap = new Bitmap  
       (System.Environment.GetFolderPath  
          (System.Environment.SpecialFolder.MyPictures));  
  
    ```  
  
    ```cpp  
    // Uses the System.Environment.GetFolderPath to get the path to the   
    // current user's MyPictures folder.  
    Bitmap^ myBitmap = gcnew Bitmap  
       (System::Environment::GetFolderPath  
          (System::Environment::SpecialFolder::MyPictures));  
    ```  
  
2.  Creare un oggetto <xref:System.Drawing.Graphics> che rappresenti la superficie di disegno da utilizzare.  Per ulteriori informazioni, vedere [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md).  
  
    ```vb  
    ' Creates a Graphics object that represents the drawing surface of   
    ' Button1.  
    Dim g as Graphics = Button1.CreateGraphics  
  
    ```  
  
    ```csharp  
    // Creates a Graphics object that represents the drawing surface of   
    // Button1.  
    Graphics g = Button1.CreateGraphics();  
  
    ```  
  
    ```cpp  
    // Creates a Graphics object that represents the drawing surface of   
    // Button1.  
    Graphics^ g = button1->CreateGraphics();  
    ```  
  
3.  Chiamare il metodo <xref:System.Drawing.Graphics.DrawImage%2A> dell'oggetto Graphics per eseguire il rendering dell'immagine.  È necessario specificare sia l'immagine da creare che le coordinate del punto in cui deve essere creata.  
  
    ```vb  
    g.DrawImage(myBitmap, 1, 1)  
  
    ```  
  
    ```csharp  
    g.DrawImage(myBitmap, 1, 1);  
  
    ```  
  
    ```cpp  
    g->DrawImage(myBitmap, 1, 1);  
    ```  
  
## Vedere anche  
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [Penne, linee e rettangoli in GDI\+](../../../../docs/framework/winforms/advanced/pens-lines-and-rectangles-in-gdi.md)   
 [Procedura: disegnare testo in un Windows Form](../../../../docs/framework/winforms/advanced/how-to-draw-text-on-a-windows-form.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Drawing Lines or Closed Figures](../Topic/Drawing%20Lines%20or%20Closed%20Figures%20\(Image%20Editor%20for%20Icons\).md)   
 [Image Editor for Icons](../Topic/Image%20Editor%20for%20Icons.md)