---
title: "Procedura: impostare lo sfondo di un controllo Panel Windows Form | Microsoft Docs"
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
  - "colori di sfondo, controlli Panel Windows Form"
  - "immagini di sfondo, controlli Panel Windows Form"
  - "colori, controlli Panel Windows Form"
  - "Panel (controllo) [Windows Form], sfondo"
ms.assetid: 096cbd8d-45cc-47b8-b1ef-a27f60ea8be0
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: impostare lo sfondo di un controllo Panel Windows Form
Un controllo <xref:System.Windows.Forms.Panel> Windows Form consente di visualizzare sia un colore di sfondo che un'immagine di sfondo.  La proprietà <xref:System.Windows.Forms.Control.BackColor%2A> imposta il colore di sfondo per i controlli contenuti nel pannello, ad esempio etichette e pulsanti di opzione.  Se la proprietà <xref:System.Windows.Forms.Control.BackgroundImage%2A> non è impostata, l'intero pannello verrà riempito dalla selezione <xref:System.Windows.Forms.Control.BackColor%2A>.  Se la proprietà <xref:System.Windows.Forms.Control.BackgroundImage%2A> è impostata, l'immagine verrà visualizzata dietro i controlli contenuti.  
  
### Per impostare lo sfondo a livello di codice  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Control.BackColor%2A> del pannello su un valore di tipo <xref:System.Drawing.Color?displayProperty=fullName>.  
  
    ```vb  
    Panel1.BackColor = Color.AliceBlue  
  
    ```  
  
    ```csharp  
    panel1.BackColor = Color.AliceBlue;  
  
    ```  
  
    ```cpp  
    panel1->BackColor = Color::AliceBlue;  
    ```  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.Control.BackgroundImage%2A> del pannello tramite il metodo <xref:System.Drawing.Image.FromFile%2A> della classe <xref:System.Drawing.Image?displayProperty=fullName>.  
  
    ```vb  
    ' You should replace the bolded image   
    ' in the sample below with an image of your own choosing.  
    Panel1.BackgroundImage = Image.FromFile _  
        (System.Environment.GetFolderPath _  
        (System.Environment.SpecialFolder.Personal) _  
        & "\Image.gif")  
  
    ```  
  
    ```csharp  
    // You should replace the bolded image   
    // in the sample below with an image of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    panel1.BackgroundImage = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
  
    ```  
  
    ```cpp  
    // You should replace the bolded image   
    // in the sample below with an image of your own choosing.  
    panel1->BackgroundImage = Image::FromFile(String::Concat(  
       System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\Image.gif"));  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.BackColor%2A>   
 <xref:System.Windows.Forms.Control.BackgroundImage%2A>   
 [Controllo Panel](../../../../docs/framework/winforms/controls/panel-control-windows-forms.md)   
 [Cenni preliminari sul controllo Panel](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)