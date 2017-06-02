---
title: "How to: Display Dialog Boxes for Windows Forms | Microsoft Docs"
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
  - "Windows Forms, displaying"
  - "Windows Forms dialog boxes, displaying"
  - "Windows Forms, calling one form from another"
  - "dialog boxes, displaying for Windows Forms"
ms.assetid: aaac1b38-c651-495a-8d3d-5a9bfb32fee3
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Display Dialog Boxes for Windows Forms
Le finestre di dialogo vengono visualizzate nello stesso modo in cui sono visualizzati gli altri form dell'applicazione.  Il form di avvio viene caricato automaticamente quando si esegue l'applicazione.  Per visualizzare un secondo form o una seconda finestra di dialogo all'interno dell'applicazione, è necessario scrivere il codice che ne consente il caricamento e la visualizzazione.  Analogamente, per consentire la scomparsa del form o della finestra di dialogo, scrivere il codice per scaricare o nascondere l’elemento.  
  
### Per visualizzare una finestra di dialogo  
  
1.  Passare al gestore eventi tramite il quale si desidera aprire la finestra di dialogo.  Ciò può accadere quando si sceglie un comando di menu, quando si fa clic su un pulsante o quando si verifica un qualsiasi altro evento.  
  
2.  Nel gestore eventi aggiungere il codice per aprire la finestra di dialogo.  Nell'esempio che segue viene utilizzato un evento Click relativo a un pulsante per visualizzare la finestra di dialogo:  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim dlg1 as new Form()  
       dlg1.ShowDialog()  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)   
    {  
       Form dlg1 = new Form();  
       dlg1.ShowDialog();  
    }  
  
    ```  
  
    ```cpp  
    private:   
      void button1_Click(System::Object ^ sender,  
        System::EventArgs ^ e)  
      {  
        Form ^ dlg1 = gcnew Form();  
        dlg1->ShowDialog();  
      }  
    ```