---
title: "Procedura: disabilitare le schede | Microsoft Docs"
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
  - "schede, nascoste in form"
  - "TabControl (controllo) [Windows Form], disabilitazione di pagine"
ms.assetid: adcc6618-8a34-4ee1-bbe3-47e732de6a59
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: disabilitare le schede
In alcune circostanze può risultare necessario limitare l'accesso ai dai disponibili nell'applicazione Windows Form,  ad esempio quando i dati sono visualizzati nelle pagine di un controllo scheda e si desidera riservare agli amministratori una scheda contenente informazioni riservate cui impedire l'accesso a utenti guest o di livello inferiore.  
  
### Per disabilitare gli oggetti TabPage a livello di codice  
  
1.  Scrivere il codice per gestire l'evento <xref:System.Windows.Forms.TabControl.SelectedIndexChanged> della scheda.  Si tratta dell'evento generato quando l'utente passa da una scheda a quella successiva.  
  
2.  Verificare le credenziali.  A seconda delle informazioni visualizzate, è possibile fare in modo da verificare il nome dell'utente che ha effettuato l'accesso o un altro tipo di credenziali prima di consentire all'utente di visualizzare la scheda.  
  
3.  Se l'utente dispone delle credenziali appropriate, visualizzare la scheda selezionata.  Se invece le credenziali utente non sono valide, visualizzare una casella di messaggio o un altro tipo di interfaccia utente, in cui si avverte che l'utente non dispone dell'accesso e tornare alla scheda iniziale.  
  
    > [!NOTE]
    >  Quando si implementa questa funzionalità nelle applicazioni di produzione, è possibile eseguire la verifica delle credenziali durante l'evento <xref:System.Windows.Forms.Form.Load> del form.  In questo modo la scheda verrà nascosta prima della visualizzazione di un qualsiasi tipo di interfaccia utente e il codice risulterà più chiaro.  La metodologia relativa alla verifica delle credenziali e alla disabilitazione della scheda durante l'evento <xref:System.Windows.Forms.TabControl.SelectedIndexChanged>, qui di seguito, è utilizzata a solo scopo esemplificativo.  
  
4.  Se ad esempio si dispone di più di due pagine scheda, è possibile visualizzarne una diversa da quella originale.  
  
     Nell'esempio seguente viene utilizzato un controllo <xref:System.Windows.Forms.CheckBox> anziché la verifica delle credenziali, in quanto i criteri di accesso alla scheda variano a seconda dell'applicazione.  Quando viene generato l'evento <xref:System.Windows.Forms.TabControl.SelectedIndexChanged>, se la verifica delle credenziali ha esito positivo, ossia se la casella di controllo è selezionata, e la scheda selezionata è `TabPage2`, ossia la scheda contenente informazioni riservate in questo esempio, verrà visualizzata la scheda `TabPage2`.  In caso contrario, verrà visualizzata la scheda `TabPage3` unitamente a una casella di messaggio in cui si informa che l'utente non dispone dei privilegi di accesso appropriati.  Nel codice riportato di seguito si presuppone l'esistenza di un controllo <xref:System.Windows.Forms.CheckBox> \(`CredentialCheck`\) e di un controllo <xref:System.Windows.Forms.TabControl> contenente tre pagine scheda.  
  
    ```vb  
    Private Sub TabControl1_SelectedIndexChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles TabControl1.SelectedIndexChanged  
       ' Check Credentials Here  
  
       If CredentialCheck.Checked = True And _   
       TabControl1.SelectedTab Is TabPage2 Then  
          TabControl1.SelectedTab = TabPage2  
       ElseIf CredentialCheck.Checked = False _   
       And TabControl1.SelectedTab Is TabPage2 Then  
          MessageBox.Show _   
         ("Unable to load tab. You have insufficient access privileges.")  
          TabControl1.SelectedTab = TabPage3  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void tabControl1_SelectedIndexChanged(object sender, System.EventArgs e)  
    {  
        // Check Credentials Here  
  
        if ((CredentialCheck.Checked == true) && (tabControl1.SelectedTab == tabPage2))   
        {  
            tabControl1.SelectedTab = tabPage2;  
        }  
        else if ((CredentialCheck.Checked == false) && (tabControl1.SelectedTab == tabPage2))  
        {  
            MessageBox.Show("Unable to load tab. You have insufficient access privileges.");  
            tabControl1.SelectedTab = tabPage3;  
        }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void tabControl1_SelectedIndexChanged(  
          System::Object ^ sender,  
          System::EventArgs ^  e)  
       {  
          // Check Credentials Here  
          if ((CredentialCheck->Checked == true) &&  
              (tabControl1->SelectedTab == tabPage2))  
          {  
             tabControl1->SelectedTab = tabPage2;  
          }  
          else if ((CredentialCheck->Checked == false) &&  
                   (tabControl1->SelectedTab == tabPage2))  
          {  
             MessageBox::Show(String::Concat("Unable to load tab. ",  
                "You have insufficient access privileges."));  
             tabControl1->SelectedTab = tabPage3;  
          }  
       }  
    ```  
  
     \(Visual C\#, Visual C\+\+\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.tabControl1.SelectedIndexChanged +=   
       new System.EventHandler(this.tabControl1_SelectedIndexChanged);  
  
    ```  
  
    ```cpp  
    this->tabControl1->SelectedIndexChanged +=  
       gcnew System::EventHandler(this, &Form1::tabControl1_SelectedIndexChanged);  
    ```  
  
## Vedere anche  
 [Cenni preliminari sul controllo TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-overview-windows-forms.md)   
 [Procedura: aggiungere un controllo a un oggetto TabPage](../../../../docs/framework/winforms/controls/how-to-add-a-control-to-a-tab-page.md)   
 [Procedura: aggiungere e rimuovere schede tramite il controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)   
 [Procedura: modificare l'aspetto del controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)