---
title: "Procedura: eseguire il collegamento a un oggetto o a una pagina Web con il controllo LinkLabel di Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], LinkLabel (controllo)"
  - "collegamento, ad altri form"
  - "LinkLabel (controllo) [Windows Form], esempi"
  - "LinkLabel (controllo) [Windows Form], collegamento a oggetti o pagine Web"
  - "collegamenti, ad altri form"
  - "controllo di collegamento a pagina Web"
  - "Windows Form, collegamento a oggetti"
  - "Windows Form, collegamento a pagine Web"
ms.assetid: 6c91c975-3cb7-4504-82f0-fc6255f8fb85
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: eseguire il collegamento a un oggetto o a una pagina Web con il controllo LinkLabel di Windows Form
Il controllo <xref:System.Windows.Forms.LinkLabel> di Windows Form consente di creare collegamenti ipertestuali all'interno del form.  Se si fa clic sul collegamento, è possibile modificarne il colore per indicare che tale collegamento è stato visitato.  Per ulteriori informazioni sulla modifica del colore, vedere [Procedura: modificare l'aspetto del controllo LinkLabel di Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md).  
  
## Collegamento a un altro form  
  
#### Per creare un collegamento a un altro form tramite un controllo LinkLabel  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.LinkLabel.Text%2A> su una didascalia appropriata.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> per stabilire quale parte della didascalia verrà indicata come collegamento.  Il modo in cui il collegamento viene segnalato dipende dalle proprietà di aspetto del collegamento ipertestuale.  Il valore <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> viene rappresentato da un oggetto <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> contenente due numeri, la posizione del carattere iniziale e il numero di caratteri.  La proprietà <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> può essere impostata nella finestra Proprietà oppure nel codice in modo analogo all'esempio riportato di seguito:  
  
    ```vb  
    ' In this code example, the link area has been set to begin  
    ' at the first character and extend for eight characters.  
    ' You may need to modify this based on the text entered in Step 1.  
    LinkLabel1.LinkArea = New LinkArea(0, 8)  
  
    ```  
  
    ```csharp  
    // In this code example, the link area has been set to begin  
    // at the first character and extend for eight characters.  
    // You may need to modify this based on the text entered in Step 1.  
    linkLabel1.LinkArea = new LinkArea(0,8);  
  
    ```  
  
    ```cpp  
    // In this code example, the link area has been set to begin  
    // at the first character and extend for eight characters.  
    // You may need to modify this based on the text entered in Step 1.  
    linkLabel1->LinkArea = LinkArea(0,8);  
    ```  
  
3.  Nel gestore eventi <xref:System.Windows.Forms.LinkLabel.LinkClicked> richiamare il metodo <xref:System.Windows.Forms.Form.Show%2A> per aprire un altro form nel progetto e impostare la proprietà <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> su `true`.  
  
    > [!NOTE]
    >  Un'istanza della classe <xref:System.Windows.Forms.LinkLabelLinkClickedEventArgs> contiene un riferimento al controllo <xref:System.Windows.Forms.LinkLabel> scelto, pertanto non è necessario eseguire il cast dell'oggetto `sender` .  
  
    ```vb  
    Protected Sub LinkLabel1_LinkClicked(ByVal Sender As System.Object, _  
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _  
       Handles LinkLabel1.LinkClicked  
       ' Show another form.  
       Dim f2 As New Form()  
       f2.Show  
       LinkLabel1.LinkVisited = True  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void linkLabel1_LinkClicked(object sender, System. Windows.Forms.LinkLabelLinkClickedEventArgs e)  
    {  
       // Show another form.  
       Form f2 = new Form();  
       f2.Show();  
       linkLabel1.LinkVisited = true;  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          // Show another form.  
          Form ^ f2 = new Form();  
          f2->Show();  
          linkLabel1->LinkVisited = true;  
       }  
    ```  
  
## Collegamento a una pagina Web  
 Il controllo <xref:System.Windows.Forms.LinkLabel> può essere utilizzato anche per visualizzare una pagina Web con il browser predefinito.  
  
#### Per avviare Internet Explorer e creare un collegamento a una pagina Web tramite un controllo LinkLabel  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.LinkLabel.Text%2A> su una didascalia appropriata.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> per stabilire quale parte della didascalia verrà indicata come collegamento.  
  
3.  Nel gestore eventi <xref:System.Windows.Forms.LinkLabel.LinkClicked>, nella parte centrale di un blocco di gestione delle eccezioni, chiamare una seconda procedura che imposti la proprietà <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> su `true` e utilizzi il metodo <xref:System.Diagnostics.Process.Start%2A> per avviare il browser predefinito con l'URL desiderato.  Per utilizzare il metodo <xref:System.Diagnostics.Process.Start%2A>, è necessario aggiungere un riferimento allo spazio dei nomi <xref:System.Diagnostics?displayProperty=fullName>.  
  
    > [!IMPORTANT]
    >  Se il codice riportato di seguito viene eseguito in un ambiente parzialmente attendibile, ad esempio su un'unità condivisa, il compilatore JIT restituirà un errore quando viene chiamato il metodo `VisitLink`.  L'istruzione`System.Diagnostics.Process.Start` implica infatti una richiesta di collegamento in errore.  Intercettando l'eccezione durante la chiamata del metodo `VisitLink`, il codice riportato di seguito garantisce una corretta gestione dell'eventuale errore generato del compilatore JIT.  
  
    ```vb  
    Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, _  
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _  
       Handles LinkLabel1.LinkClicked  
       Try  
          VisitLink()  
       Catch ex As Exception  
          ' The error message  
          MessageBox.Show("Unable to open link that was clicked.")  
       End Try  
    End Sub  
  
    Sub VisitLink()  
       ' Change the color of the link text by setting LinkVisited   
       ' to True.  
       LinkLabel1.LinkVisited = True  
       ' Call the Process.Start method to open the default browser   
       ' with a URL:  
       System.Diagnostics.Process.Start("http://www.microsoft.com")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void linkLabel1_LinkClicked(object sender, System.Windows.Forms.LinkLabelLinkClickedEventArgs e)  
    {  
       try  
       {  
          VisitLink();  
       }  
       catch (Exception ex )  
       {  
          MessageBox.Show("Unable to open link that was clicked.");  
       }  
    }  
  
    private void VisitLink()  
    {  
       // Change the color of the link text by setting LinkVisited   
       // to true.  
       linkLabel1.LinkVisited = true;  
       //Call the Process.Start method to open the default browser   
       //with a URL:  
       System.Diagnostics.Process.Start("http://www.microsoft.com");  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          try  
          {  
             VisitLink();  
          }  
          catch (Exception ^ ex)  
          {  
             MessageBox::Show("Unable to open link that was clicked.");  
          }  
       }  
    private:  
       void VisitLink()  
       {  
          // Change the color of the link text by setting LinkVisited   
          // to true.  
          linkLabel1->LinkVisited = true;  
          // Call the Process.Start method to open the default browser   
          // with a URL:  
          System::Diagnostics::Process::Start("http://www.microsoft.com");  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Diagnostics.Process.Start%2A?displayProperty=fullName>   
 [Cenni preliminari sul controllo LinkLabel](../../../../docs/framework/winforms/controls/linklabel-control-overview-windows-forms.md)   
 [Procedura: modificare l'aspetto del controllo LinkLabel di Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)   
 [Controllo LinkLabel](../../../../docs/framework/winforms/controls/linklabel-control-windows-forms.md)