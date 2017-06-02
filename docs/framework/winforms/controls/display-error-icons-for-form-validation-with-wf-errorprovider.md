---
title: "Procedura: visualizzare le icone di errori per la convalida dei form con il componente ErrorProvider di Windows Form | Microsoft Docs"
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
  - "icone di errore"
  - "messaggi di errore, visualizzazione di icone"
  - "ErrorProvider (componente) [Windows Form], visualizzazione di icone di errore"
  - "errori [Windows Form], visualizzazione per gli utenti"
ms.assetid: 3b681a32-9db4-497b-a34b-34980eabee46
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: visualizzare le icone di errori per la convalida dei form con il componente ErrorProvider di Windows Form
È possibile utilizzare un componente <xref:System.Windows.Forms.ErrorProvider> di Windows Form per visualizzare un'icona di errore quando l'utente immette dati non validi.  È necessario che nel form siano presenti almeno due controlli per richiamare il codice di convalida passando da un controllo all'altro.  
  
### Per visualizzare un'icona di errore quando il valore di un controllo non è valido  
  
1.  Aggiungere due controlli, ad esempio due caselle di testo, a un Windows Form.  
  
2.  Aggiungere un componente <xref:System.Windows.Forms.ErrorProvider> al form.  
  
3.  Selezionare il primo controllo e aggiungere il codice al corrispondente gestore eventi <xref:System.Windows.Forms.Control.Validating>.  Perché il codice venga eseguito in modo corretto, la routine deve essere collegata all'evento.  Per ulteriori informazioni, vedere [How to: Create Event Handlers at Run Time for Windows Forms](../../../../docs/framework/winforms/how-to-create-event-handlers-at-run-time-for-windows-forms.md).  
  
     Mediante il codice riportato di seguito viene verificata la validità dei dati immessi dall'utente; se i dati non sono validi, viene chiamato il metodo <xref:System.Windows.Forms.ErrorProvider.SetError%2A>.  Il primo argomento del metodo <xref:System.Windows.Forms.ErrorProvider.SetError%2A> specifica il controllo accanto al quale visualizzare l'icona.  Il secondo argomento è il testo dell'errore da visualizzare.  
  
    ```vb  
    Private Sub TextBox1_Validating(ByVal Sender As Object, _  
       ByVal e As System.ComponentModel.CancelEventArgs) Handles _  
       TextBox1.Validating  
          If Not IsNumeric(TextBox1.Text) Then  
             ErrorProvider1.SetError(TextBox1, "Not a numeric value.")  
          Else  
             ' Clear the error.  
             ErrorProvider1.SetError(TextBox1, "")  
          End If  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void textBox1_Validating (object sender,  
       System.ComponentModel.CancelEventArgs e)  
    {  
       try  
       {  
          int x = Int32.Parse(textBox1.Text);  
          errorProvider1.SetError(textBox1, "");  
       }  
       catch (Exception ex)  
       {  
          errorProvider1.SetError(textBox1, "Not an integer value.");  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void textBox1_Validating(System::Object ^  sender,  
          System::ComponentModel::CancelEventArgs ^  e)  
       {  
          try  
          {  
             int x = Int32::Parse(textBox1->Text);  
             errorProvider1->SetError(textBox1, "");  
          }  
          catch (System::Exception ^ ex)  
          {  
             errorProvider1->SetError(textBox1, "Not an integer value.");  
          }  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.textBox1.Validating += new  
    System.ComponentModel.CancelEventHandler(this.textBox1_Validating);  
  
    ```  
  
    ```cpp  
    this->textBox1->Validating += gcnew  
       System::ComponentModel::CancelEventHandler  
       (this, &Form1::textBox1_Validating);  
    ```  
  
4.  Eseguire il progetto.  Digitare dati non validi, ad esempio non numerici, nel primo controllo e quindi passare al secondo.  Quando viene visualizzata l'icona di errore, posizionare il mouse sull'icona per visualizzare il testo dell'errore.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ErrorProvider.SetError%2A>   
 [Cenni preliminari sul componente ErrorProvider](../../../../docs/framework/winforms/controls/errorprovider-component-overview-windows-forms.md)   
 [Procedura: visualizzare errori in un dataset tramite il componente ErrorProvider di Windows Form](../../../../docs/framework/winforms/controls/view-errors-within-a-dataset-with-wf-errorprovider-component.md)