---
title: "Procedura: suddividere una finestra orizzontalmente | Microsoft Docs"
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
  - "SplitContainer (controllo) [Windows Form], barra di divisione orizzontale"
  - "finestre con separatore, modifica dell'orientamento della barra di divisione"
  - "finestre con separatore, orizzontali"
  - "finestre, suddivisione orizzontale"
ms.assetid: a1f74f29-048c-4723-85fa-b9d375ab8f4b
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: suddividere una finestra orizzontalmente
Nell'esempio di codice riportato di seguito viene creata la barra di divisione che divide il controllo <xref:System.Windows.Forms.SplitContainer> in senso orizzontale.  
  
> [!NOTE]
>  La proprietà <xref:System.Windows.Forms.SplitContainer.Orientation%2A> del controllo <xref:System.Windows.Forms.SplitContainer> determina la direzione della barra di divisione, non del controllo stesso.  
  
### Per dividere una finestra orizzontalmente  
  
1.  All'interno di una routine, impostare la proprietà <xref:System.Windows.Forms.SplitContainer.Orientation%2A> del controllo <xref:System.Windows.Forms.SplitContainer> su <xref:System.Windows.Forms.Orientation>.  
  
    ```vb  
    Sub ShowSplitContainer()  
        Dim splitContainer1 as new SplitContainer()  
        splitContainer1.BorderStyle = BorderStyle.Fixed3D  
        splitContainer1.Location = New System.Drawing.Point(74, 20)  
        splitContainer1.Name = "DemoSplitContainer"  
        splitContainer1.Size = New System.Drawing.Size(212, 435)  
        splitContainer1.TabIndex = 0  
        splitContainer1.Orientation = Orientation.Horizontal  
        Controls.Add(splitContainer1)  
    End Sub  
  
    ```  
  
    ```csharp  
    public void showSplitContainer()  
    {  
        SplitContainer splitContainer1 = new SplitContainer ();  
        splitContainer1.BorderStyle = BorderStyle.Fixed3D;  
        splitContainer1.Location = new System.Drawing.Point (74, 20);  
        splitContainer1.Name = "DemoSplitContainer";  
        splitContainer1.Size = new System.Drawing.Size (212, 435);  
        splitContainer1.TabIndex = 0;  
        splitContainer1.Orientation = Orientation.Horizontal;  
        this.Controls.Add (splitContainer1);  
  
    }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.SplitContainer>   
 [Controllo SplitContainer](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)