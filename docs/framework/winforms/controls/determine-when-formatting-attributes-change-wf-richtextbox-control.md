---
title: "Procedura: individuare le modifiche degli attributi di formattazione nel controllo RichTextBox Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], caselle di testo"
  - "RichTextBox (controllo) [Windows Form], rilevamento modifiche al tipo di carattere"
  - "SelBold (proprietà)"
  - "SelChange (evento)"
  - "caselle di testo, rilevamento modifiche al tipo di carattere"
ms.assetid: bdfed015-f77a-41e5-b38f-f8629b2fa166
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: individuare le modifiche degli attributi di formattazione nel controllo RichTextBox Windows Form
Generalmente il controllo <xref:System.Windows.Forms.RichTextBox> Windows Form viene utilizzato per formattare del testo con attributi, quali opzioni dei caratteri o stili dei paragrafi.  È possibile che nell'applicazione sia necessario tenere traccia delle modifiche apportate alla formattazione del testo allo scopo di visualizzare una barra degli strumenti, come nel caso di molti programmi di elaborazione testi.  
  
### Per rispondere alle modifiche degli attributi di formattazione  
  
1.  Nel gestore eventi <xref:System.Windows.Forms.RichTextBox.SelectionChanged> scrivere il codice per eseguire un'azione appropriata in base al valore dell'attributo.  Nell'esempio qui di seguito viene modificato l'aspetto di un pulsante della barra degli strumenti in base al valore della proprietà <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A>.  Il pulsante della barra degli strumenti verrà aggiornato solo quando il punto di inserimento viene spostato nel controllo.  
  
     Si presuppone l'esistenza di un form contenente un controllo <xref:System.Windows.Forms.RichTextBox> e un controllo <xref:System.Windows.Forms.ToolBar> che contiene a sua volta un pulsante della barra degli strumenti.  Per ulteriori informazioni sulle barre degli strumenti e i relativi pulsanti, vedere [Procedura: aggiungere pulsanti a un controllo ToolBar](../../../../docs/framework/winforms/controls/how-to-add-buttons-to-a-toolbar-control.md).  
  
    ```vb  
    ' The following code assumes the existence of a toolbar control  
    ' with at least one toolbar button.  
    Private Sub RichTextBox1_SelectionChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles RichTextBox1.SelectionChanged  
       If RichTextBox1.SelectionBullet = True Then  
          ' Bullet button on toolbar should appear pressed  
          ToolBarButton1.Pushed = True  
       Else  
           ' Bullet button on toolbar should appear unpressed  
           ToolBarButton1.Pushed = False  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    // The following code assumes the existence of a toolbar control  
    // with at least one toolbar button.  
    private void richTextBox1_SelectionChanged(object sender,  
    System.EventArgs e)  
    {  
       if (richTextBox1.SelectionBullet == true)   
       {  
          // Bullet button on toolbar should appear pressed  
          toolBarButton1.Pushed = true;  
       }  
       else   
       {  
          // Bullet button on toolbar should appear unpressed  
          toolBarButton1.Pushed = false;  
       }  
    }  
  
    ```  
  
    ```cpp  
    // The following code assumes the existence of a toolbar control  
    // with at least one toolbar button.  
    private:  
       System::Void richTextBox1_SelectionChanged(  
          System::Object ^  sender, System::EventArgs ^  e)  
       {  
          if (richTextBox1->SelectionBullet == true)  
          {  
             // Bullet button on toolbar should appear pressed  
             toolBarButton1->Pushed = true;  
          }  
          else  
          {  
             // Bullet button on toolbar should appear unpressed  
             toolBarButton1->Pushed = false;  
          }  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBox.SelectionChanged>   
 <xref:System.Windows.Forms.RichTextBox>   
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)