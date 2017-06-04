---
title: "Procedura: attivare eventi di menu per i pulsanti di una barra degli strumenti | Microsoft Docs"
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
  - "esempi [Windows Form], barre degli strumenti"
  - "ToolBar (controllo) [Windows Form], gestori di eventi click"
  - "ToolBar (controllo) [Windows Form], codifica di eventi di scelta di pulsanti"
  - "barre degli strumenti [Windows Form], gestori di eventi click"
ms.assetid: 98374f70-993d-4ca4-89fb-48fea6ce5b45
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: attivare eventi di menu per i pulsanti di una barra degli strumenti
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.ToolStrip> sostituisca il controllo <xref:System.Windows.Forms.ToolBar> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.ToolBar> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 Se i Windows Form presentano un controllo <xref:System.Windows.Forms.ToolBar> con pulsanti di una barra degli strumenti, è possibile individuare il pulsante selezionato dall'utente.  
  
 Nell'evento <xref:System.Windows.Forms.ToolBar.ButtonClick> del controllo <xref:System.Windows.Forms.ToolBar>, è possibile valutare la proprietà <xref:System.Windows.Forms.ToolBarButtonClickEventArgs.Button%2A> della classe <xref:System.Windows.Forms.ToolBarButtonClickEventArgs>.  Nell'esempio riportato di seguito viene mostrata una finestra di messaggio, in cui viene indicato il pulsante selezionato.  Per informazioni dettagliate, vedere [Classe MessageBox](frlrfSystemWindowsFormsMessageBoxClassTopic).  
  
 Nell'esempio qui di seguito si presuppone che un controllo <xref:System.Windows.Forms.ToolBar> sia stato aggiunto a un Windows Form.  
  
### Per gestire l'evento Click su una barra degli strumenti  
  
1.  In una routine, aggiungere i pulsanti di una barra degli strumenti al controllo <xref:System.Windows.Forms.ToolBar>.  
  
    ```vb  
    Public Sub ToolBarConfig()  
    ' Instantiate the toolbar buttons, set their Text properties  
    ' and add them to the ToolBar control.  
       ToolBar1.Buttons.Add(New ToolBarButton("One"))  
       ToolBar1.Buttons.Add(New ToolBarButton("Two"))  
       ToolBar1.Buttons.Add(New ToolBarButton("Three"))  
    ' Add the event handler delegate.  
       AddHandler ToolBar1.ButtonClick, AddressOf Me.ToolBar1_ButtonClick  
    End Sub  
  
    ```  
  
    ```csharp  
    public void ToolBarConfig()   
    {  
       toolBar1.Buttons.Add(new ToolBarButton("One"));  
       toolBar1.Buttons.Add(new ToolBarButton("Two"));  
       toolBar1.Buttons.Add(new ToolBarButton("Three"));  
  
       toolBar1.ButtonClick +=   
          new ToolBarButtonClickEventHandler(this.toolBar1_ButtonClick);  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void ToolBarConfig()  
       {  
          toolBar1->Buttons->Add(gcnew ToolBarButton("One"));  
          toolBar1->Buttons->Add(gcnew ToolBarButton("Two"));  
          toolBar1->Buttons->Add(gcnew ToolBarButton("Three"));  
  
          toolBar1->ButtonClick +=   
             gcnew ToolBarButtonClickEventHandler(this,  
             &Form1::toolBar1_ButtonClick);  
       }  
    ```  
  
2.  Aggiungere un gestore eventi per l'evento <xref:System.Windows.Forms.ToolBar.ButtonClick> del controllo <xref:System.Windows.Forms.ToolBar>.  Utilizzare un'istruzione case di passaggio e la classe <xref:System.Windows.Forms.ToolBarButtonClickEventArgs> per individuare il pulsante della barra degli strumenti selezionato.  Verrà visualizzata una finestra di messaggio appropriata.  
  
    > [!NOTE]
    >  In questo esempio una finestra di messaggio viene utilizzata unicamente come segnaposto.  È possibile aggiungere altro codice da eseguire quando vengono selezionati i pulsanti della barra degli strumenti.  
  
    ```vb  
    Protected Sub ToolBar1_ButtonClick(ByVal sender As Object, _  
    ByVal e As ToolBarButtonClickEventArgs)  
    ' Evaluate the Button property of the ToolBarButtonClickEventArgs  
    ' to determine which button was clicked.  
       Select Case ToolBar1.Buttons.IndexOf(e.Button)  
         Case 0  
           MessageBox.Show("First toolbar button clicked")  
         Case 1  
           MessageBox.Show("Second toolbar button clicked")  
         Case 2  
           MessageBox.Show("Third toolbar button clicked")  
       End Select  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void toolBar1_ButtonClick(object sender,  
    ToolBarButtonClickEventArgs e)  
    {  
       // Evaluate the Button property of the ToolBarButtonClickEventArgs  
       // to determine which button was clicked.  
       switch (toolBar1.Buttons.IndexOf(e.Button))  
       {  
          case 0 :  
             MessageBox.Show("First toolbar button clicked");  
             break;  
          case 1 :  
             MessageBox.Show("Second toolbar button clicked");  
             break;  
          case 2 :  
             MessageBox.Show("Third toolbar button clicked");  
             break;  
       }  
    }  
  
    ```  
  
    ```cpp  
    protected:  
       void toolBar1_ButtonClick(System::Object ^ sender,  
          ToolBarButtonClickEventArgs ^ e)  
       {  
         // Evaluate the Button property of the ToolBarButtonClickEventArgs  
         // to determine which button was clicked.  
          switch (toolBar1->Buttons->IndexOf(e->Button))  
          {  
             case 0 :  
                MessageBox::Show("First toolbar button clicked");  
                break;  
             case 1 :  
                MessageBox::Show("Second toolbar button clicked");  
                break;  
             case 2 :  
                MessageBox::Show("Third toolbar button clicked");  
                break;  
          }  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolBar>   
 [Procedura: aggiungere pulsanti a un controllo ToolBar](../../../../docs/framework/winforms/controls/how-to-add-buttons-to-a-toolbar-control.md)   
 [Procedura: definire un'icona per un pulsante ToolBar](../../../../docs/framework/winforms/controls/how-to-define-an-icon-for-a-toolbar-button.md)   
 [Controllo ToolBar](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)