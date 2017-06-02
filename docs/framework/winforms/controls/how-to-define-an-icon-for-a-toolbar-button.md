---
title: "Procedura: definire un&#39;icona per un pulsante ToolBar | Microsoft Docs"
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
  - "pulsanti [Windows Form], icone"
  - "esempi [Windows Form], barre degli strumenti"
  - "icone [Windows Form], pulsanti della barra degli strumenti"
  - "immagini [Windows Form], pulsanti della barra degli strumenti"
  - "ToolBar (controllo) [Windows Form], aggiunta di icone a pulsanti"
  - "barre degli strumenti [Windows Form], aggiunta di icone a pulsanti"
ms.assetid: 84db98b4-8566-49ce-b2c8-1fd66a5eb3a0
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: definire un&#39;icona per un pulsante ToolBar
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.ToolStrip> sostituisca il controllo <xref:System.Windows.Forms.ToolBar> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.ToolBar> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 I pulsanti <xref:System.Windows.Forms.ToolBar> consentono di visualizzare icone al loro interno per semplificarne l'identificazione da parte degli utenti.  A tale scopo, vengono aggiunte immagini al componente [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md), quindi il componente <xref:System.Windows.Forms.ImageList> viene associato al controllo <xref:System.Windows.Forms.ToolBar>.  
  
### Per impostare un'icona per un pulsante di una barra degli strumenti a livello di codice  
  
1.  In una routine, creare un'istanza di un componente <xref:System.Windows.Forms.ImageList> e di un controllo <xref:System.Windows.Forms.ToolBar>.  
  
2.  Nella stessa routine, assegnare un'immagine al componente <xref:System.Windows.Forms.ImageList>.  
  
3.  Nella stessa routine, assegnare infine il controllo <xref:System.Windows.Forms.ImageList> al controllo <xref:System.Windows.Forms.ToolBar> e assegnare la proprietà <xref:System.Windows.Forms.ToolBarButton.ImageIndex%2A> dei singoli pulsanti della barra degli strumenti.  
  
     Nell'esempio di codice riportato di seguito il percorso impostato per la posizione dell'immagine corrisponde alla cartella **Documenti**.  Questa scelta è dovuta al fatto che si suppone che questa directory sia presente sulla maggior parte dei computer con sistema operativo Windows.  La scelta di questa posizione consente inoltre di eseguire l'applicazione senza problemi agli utenti che dispongono di livelli di accesso minimo.  Nell'esempio riportato di seguito si presuppone che un controllo <xref:System.Windows.Forms.PictureBox> sia già stato aggiunto al form.  
  
     La procedura illustrata in precedenza consente di scrivere un codice simile a quello riportato di seguito.  
  
    ```vb  
    Public Sub InitializeMyToolBar()  
    ' Instantiate an ImageList component and a ToolBar control.  
       Dim ToolBar1 as New ToolBar  
       Dim ImageList1 as New ImageList  
    ' Assign an image to the ImageList component.  
    ' You should replace the bold image  
    ' in the sample below with an icon of your own choosing.  
       Dim myImage As System.Drawing.Image = _   
          Image.FromFile Image.FromFile _  
          (System.Environment.GetFolderPath _  
          (System.Environment.SpecialFolder.Personal) _  
          & "\Image.gif")  
       ImageList1.Images.Add(myImage)  
    ' Create a ToolBarButton.  
       Dim ToolBarButton1 As New ToolBarButton()  
    ' Add the ToolBarButton to the ToolBar.  
       ToolBar1.Buttons.Add(toolBarButton1)  
    ' Assign an ImageList to the ToolBar.  
       ToolBar1.ImageList = ImageList1  
    ' Assign the ImageIndex property of the ToolBarButton.  
       ToolBarButton1.ImageIndex = 0  
    End Sub  
  
    ```  
  
    ```csharp  
    public void InitializeMyToolBar()  
    {  
       // Instantiate an ImageList component and a ToolBar control.  
       ToolBar toolBar1 = new  ToolBar();   
       ImageList imageList1 = new ImageList();  
       // Assign an image to the ImageList component.  
       // You should replace the bold image   
       // in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       Image myImage = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
       imageList1.Images.Add(myImage);  
       // Create a ToolBarButton.  
       ToolBarButton toolBarButton1 = new ToolBarButton();  
       // Add the ToolBarButton to the ToolBar.  
       toolBar1.Buttons.Add(toolBarButton1);  
       // Assign an ImageList to the ToolBar.  
       toolBar1.ImageList = imageList1;  
       // Assign ImageIndex property of the ToolBarButton.  
       toolBarButton1.ImageIndex = 0;  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void InitializeMyToolBar()  
       {  
          // Instantiate an ImageList component and a ToolBar control.  
          ToolBar ^ toolBar1 = gcnew  ToolBar();   
          ImageList ^ imageList1 = gcnew ImageList();  
          // Assign an image to the ImageList component.  
          // You should replace the bold image   
          // in the sample below with an icon of your own choosing.  
          Image ^ myImage = Image::FromFile(String::Concat  
             (System::Environment::GetFolderPath  
             (System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
          imageList1->Images->Add(myImage);  
          // Create a ToolBarButton.  
          ToolBarButton ^ toolBarButton1 = gcnew ToolBarButton();  
          // Add the ToolBarButton to the ToolBar.  
          toolBar1->Buttons->Add(toolBarButton1);  
          // Assign an ImageList to the ToolBar.  
          toolBar1->ImageList = imageList1;  
          // Assign ImageIndex property of the ToolBarButton.  
          toolBarButton1->ImageIndex = 0;  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolBar>   
 [Procedura: attivare eventi di menu per i pulsanti di una barra degli strumenti](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)   
 [Controllo ToolBar](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)   
 [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)