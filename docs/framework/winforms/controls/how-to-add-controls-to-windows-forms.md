---
title: "Procedura: aggiungere controlli a un Windows Form | Microsoft Docs"
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
  - "controlli [Windows Form], aggiunta"
  - "controlli Windows Form, aggiunta a form"
ms.assetid: 2af86001-9d62-4154-87fb-66db2c3cd9fd
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: aggiungere controlli a un Windows Form
La maggior parte dei form viene progettata aggiungendo controlli sulla relativa superficie per definire un'interfaccia utente.  Un *controllo* è un componente su un form utilizzato per visualizzare informazioni o per accettare l'input dell'utente.  Per ulteriori informazioni sui controlli, vedere [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per disegnare un controllo su un form  
  
1.  Aprire il form.  Per ulteriori informazioni, vedere [How to: Display Windows Forms in the Designer](http://msdn.microsoft.com/it-it/bf3f1e5b-ea07-4529-85c6-6af3ded0cec5).  
  
2.  Nella **Casella degli strumenti** fare clic sul controllo che si desidera aggiungere al form.  
  
3.  Nel form fare clic sul punto in cui si desidera posizionare l'angolo superiore sinistro del controllo, quindi trascinare fino al punto in cui si desidera posizionare l'angolo inferiore destro.  
  
     Il controllo verrà aggiunto al form con la posizione e le dimensioni specificate.  
  
    > [!NOTE]
    >  Ciascun controllo presenta dimensioni predefinite.  È possibile aggiungere al form un controllo di dimensioni predefinite trascinandolo dalla **Casella degli strumenti** al form.  
  
### Per trascinare un controllo in un form  
  
1.  Aprire il form.  Per ulteriori informazioni, vedere [How to: Display Windows Forms in the Designer](http://msdn.microsoft.com/it-it/bf3f1e5b-ea07-4529-85c6-6af3ded0cec5).  
  
2.  Nella **Casella degli strumenti** fare clic sul controllo desiderato e trascinarlo nel form.  
  
     Il controllo verrà aggiunto al form nella posizione specificata e con le dimensioni predefinite.  
  
    > [!NOTE]
    >  Se si fa doppio clic su un controllo nella **Casella degli strumenti**, il controllo verrà aggiunto nell'angolo superiore sinistro del form nella dimensione predefinita.  
  
     È anche possibile aggiungere controlli a un form dinamicamente in fase di esecuzione.  Nell'esempio di codice riportato di seguito un controllo <xref:System.Windows.Forms.TextBox> viene aggiunto al form quando si fa clic sul controllo <xref:System.Windows.Forms.Button>.  
  
    > [!NOTE]
    >  Nella procedura che segue si presuppone l'esistenza di un form che contiene già un controllo **Button**, `Button1`.  
  
### Per aggiungere un controllo a un form a livello di programmazione  
  
1.  Nel metodo che gestisce l'evento `Click` del pulsante all'interno della classe del form inserire codice simile a quello illustrato di seguito per aggiungere il riferimento alla variabile del controllo, impostare la proprietà `Location` del controllo, quindi aggiungere il controllo.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim MyText As New TextBox()  
       MyText.Location = New Point(25, 25)  
       Me.Controls.Add(MyText)  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)   
    {  
       TextBox myText = new TextBox();  
       myText.Location = new Point(25,25);  
       this.Controls.Add (myText);  
    }  
  
    ```  
  
    ```cpp  
    private:  
      System::Void button1_Click(System::Object ^  sender,  
        System::EventArgs ^  e)  
      {  
        TextBox ^ myText = gcnew TextBox();  
        myText->Location = Point(25,25);  
        this->Controls->Add(myText);  
      }  
    ```  
  
    > [!NOTE]
    >  È anche possibile aggiungere codice per inizializzare altre proprietà del controllo.  
  
    > [!IMPORTANT]
    >  Il riferimento a un controllo `UserControl` dannoso può esporre il computer locale a un rischio per la sicurezza,  Questo problema diventa grave nel momento in cui si aggiunge inconsapevolmente al proprio progetto un controllo personalizzato dannoso appositamente sviluppato da un utente con pochi scrupoli.  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Procedura: ridimensionare i controlli di un Windows Form](../../../../docs/framework/winforms/controls/how-to-resize-controls-on-windows-forms.md)   
 [Procedura: impostare il testo visualizzato da un controllo di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)