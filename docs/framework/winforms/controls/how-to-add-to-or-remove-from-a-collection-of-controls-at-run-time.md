---
title: "Procedura: aggiungere o rimuovere controlli da una raccolta in fase di esecuzione | Microsoft Docs"
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
  - "raccolte, aggiunta di elementi"
  - "controlli [Windows Form], aggiunta tramite raccolte"
  - "controlli [Windows Form], rimozione tramite raccolte"
  - "raccolte di controlli"
  - "runtime, aggiunta di controlli"
  - "runtime, rimozione di controlli"
ms.assetid: 771bf895-3d5f-469b-a324-3528f343657e
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: aggiungere o rimuovere controlli da una raccolta in fase di esecuzione
Nello sviluppo delle applicazioni, alcune attività comuni consistono nell'aggiunta e nella rimozione di controlli da un controllo contenitore sui form, ad esempio la classe <xref:System.Windows.Forms.Panel> o il controllo <xref:System.Windows.Forms.GroupBox> oppure il form stesso.  In fase di progettazione è possibile trascinare direttamente i controlli su un pannello o una casella di gruppo.  In fase di esecuzione i controlli mantengono una raccolta `Controls` che tiene traccia dei controlli contenuti.  
  
> [!NOTE]
>  L'esempio di codice riportato di seguito è applicabile a qualsiasi controllo che mantenga una raccolta di controlli al proprio interno.  
  
### Per aggiungere un controllo a una raccolta a livello di codice  
  
1.  Creare un'istanza del controllo da aggiungere.  
  
2.  Impostare le proprietà del nuovo controllo.  
  
3.  Aggiungere il controllo alla raccolta `Controls` del controllo padre.  
  
     Nell'esempio di codice riportato di seguito viene illustrato come creare un'istanza del controllo <xref:System.Windows.Forms.Button>.  Richiede un form con un controllo <xref:System.Windows.Forms.Panel> e che il metodo per la gestione degli eventi per il pulsante che si crea, `NewPanelButton_Click`, sia già stato creato.  
  
    ```vb  
    Public NewPanelButton As New Button()  
  
    Public Sub AddNewControl()  
       ' The Add method will accept as a parameter any object that derives  
       ' from the Control class. In this case, it is a Button control.  
       Panel1.Controls.Add(NewPanelButton)  
       ' The event handler indicated for the Click event in the code   
       ' below is used as an example. Substite the appropriate event  
       ' handler for your application.  
       AddHandler NewPanelButton.Click, AddressOf NewPanelButton_Click  
    End Sub  
  
    ```  
  
    ```csharp  
    public Button newPanelButton = new Button();  
  
    public void addNewControl()  
    {   
       // The Add method will accept as a parameter any object that derives  
       // from the Control class. In this case, it is a Button control.  
       panel1.Controls.Add(newPanelButton);  
       // The event handler indicated for the Click event in the code   
       // below is used as an example. Substite the appropriate event  
       // handler for your application.  
       this.newPanelButton.Click += new System.EventHandler(this. NewPanelButton_Click);  
    }  
    ```  
  
### Per rimuovere i controlli da una raccolta a livello di codice  
  
1.  Rimuovere il gestore eventi dall'evento.  In [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] utilizzare la parola chiave [RemoveHandler Statement](../../../../ocs/visual-basic/language-reference/statements/removehandler-statement.md), mentre in [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] utilizzare [Operatore \-\=](../Topic/-=%20Operator%20\(C%23%20Reference\)2.md).  
  
2.  Utilizzare il metodo `Remove` per eliminare il controllo desiderato dalla raccolta `Controls` del pannello.  
  
3.  Chiamare il metodo <xref:System.Windows.Forms.Control.Dispose%2A> per liberare tutte le risorse utilizzate dal controllo.  
  
    ```vb  
    Public Sub RemoveControl()  
    ' NOTE: The code below uses the instance of   
    ' the button (NewPanelButton) from the previous example.  
       If Panel1.Controls.Contains(NewPanelButton) Then  
          RemoveHandler NewPanelButton.Click, AddressOf _   
             NewPanelButton_Click  
          Panel1.Controls.Remove(NewPanelButton)  
          NewPanelButton.Dispose()  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void removeControl(object sender, System.EventArgs e)  
    {  
    // NOTE: The code below uses the instance of   
    // the button (newPanelButton) from the previous example.  
       if(panel1.Controls.Contains(newPanelButton))  
       {  
          this.newPanelButton.Click -= new System.EventHandler(this.   
             NewPanelButton_Click);  
          panel1.Controls.Remove(newPanelButton);  
          newPanelButton.Dispose();  
       }  
    }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.Panel>   
 [Controllo Panel](../../../../docs/framework/winforms/controls/panel-control-windows-forms.md)