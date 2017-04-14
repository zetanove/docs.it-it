---
title: "Procedura dettagliata: aggiornamento delle informazioni sulla barra di stato in fase di esecuzione | Microsoft Docs"
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
  - "pannelli, aggiornamento della barra di stato"
  - "barre di stato, aggiornamento di pannelli"
  - "barre di stato, aggiornamento in fase di esecuzione"
  - "StatusBar (controllo) [Windows Form], aggiornamento di pannelli"
ms.assetid: cc2abb06-c082-49f7-a5a3-2fd1bbcb58d1
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura dettagliata: aggiornamento delle informazioni sulla barra di stato in fase di esecuzione
> [!IMPORTANT]
>  Benché i controlli <xref:System.Windows.Forms.StatusStrip> e <xref:System.Windows.Forms.ToolStripStatusLabel> sostituiscano i controlli <xref:System.Windows.Forms.StatusBar> e <xref:System.Windows.Forms.StatusBarPanel> delle versioni precedenti aggiungendo funzionalità, i controlli <xref:System.Windows.Forms.StatusBar> e <xref:System.Windows.Forms.StatusBarPanel> vengono mantenuti per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  
  
 Spesso, in fase di esecuzione, un programma richiede di aggiornare in modo dinamico il contenuto dei pannelli della barra di stato in base alle modifiche dello stato dell'applicazione o all'interazione dell'utente.  Si tratta di un metodo comune utilizzato per segnalare agli utenti che sono attivati tasti quali BLOC MAIUSC, BLOC NUM o BLOC SCORR oppure per fornire la data o un orologio come riferimento.  
  
 Nell'esempio che segue viene utilizzata un'istanza della classe <xref:System.Windows.Forms.StatusBarPanel> per visualizzare un orologio.  
  
### Per preparare la barra di stato per l'aggiornamento  
  
1.  Creare un nuovo Windows Form.  
  
2.  Aggiungere un controllo <xref:System.Windows.Forms.StatusBar> al form.  Per informazioni dettagliate, vedere [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
3.  Aggiungere un pannello di barra di stato al controllo <xref:System.Windows.Forms.StatusBar>.  Per informazioni dettagliate, vedere [Procedura: aggiungere pannelli a un controllo StatusBar](../../../../docs/framework/winforms/controls/how-to-add-panels-to-a-statusbar-control.md).  
  
4.  Per il controllo <xref:System.Windows.Forms.StatusBar> aggiunto al form, impostare la proprietà <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> su `true`.  
  
5.  Aggiungere al form un componente <xref:System.Windows.Forms.Timer> Windows Form.  
  
    > [!NOTE]
    >  Il componente <xref:System.Windows.Forms.Timer?displayProperty=fullName> Windows Form è progettato per l'ambiente Windows Form.  Per informazioni su un timer adatto a un ambiente server, vedere [Introduction to Server\-Based Timers](http://msdn.microsoft.com/it-it/adc0bc0a-a519-4812-bafc-fb9d1a5801fc).  
  
6.  Impostare la proprietà <xref:System.Windows.Forms.Timer.Enabled%2A> su `true`.  
  
7.  Impostare la proprietà <xref:System.Windows.Forms.Timer.Interval%2A> del componente <xref:System.Windows.Forms.Timer> su 30000.  
  
    > [!NOTE]
    >  La proprietà <xref:System.Windows.Forms.Timer.Interval%2A> del componente <xref:System.Windows.Forms.Timer> viene impostata su 30 secondi \(30.000 millisecondi\) per garantire la visualizzazione dell'ora esatta.  
  
### Per implementare il timer per l'aggiornamento della barra di stato  
  
1.  Inserire il codice riportato di seguito nel gestore eventi del componente <xref:System.Windows.Forms.Timer> per aggiornare il pannello del controllo <xref:System.Windows.Forms.StatusBar>.  
  
    ```vb  
    Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick  
       StatusBar1.Panels(0).Text = Now.ToShortTimeString  
    End Sub  
  
    ```  
  
    ```csharp  
    private void timer1_Tick(object sender, System.EventArgs e)  
    {  
       statusBar1.Panels[0].Text = DateTime.Now.ToShortTimeString();  
    }  
  
    ```  
  
    ```cpp  
    private:  
      System::Void timer1_Tick(System::Object ^ sender,  
        System::EventArgs ^ e)  
      {  
        statusBar1->Panels[0]->Text =  
          DateTime::Now.ToShortTimeString();  
      }  
    ```  
  
     Ora è possibile eseguire l'applicazione per osservare l'orologio in funzione nel pannello della barra di stato.  
  
### Per eseguire il test dell'applicazione  
  
1.  Effettuare il debug dell'applicazione, quindi premere F5 per eseguirla.  Per informazioni dettagliate sul debug, vedere [Debug in Visual Studio](../Topic/Debugging%20in%20Visual%20Studio.md).  
  
    > [!NOTE]
    >  Sono richiesti circa 30 secondi per visualizzare l'orologio sulla barra di stato,  per ottenere l'ora più accurata possibile.  Al contrario, per visualizzare più rapidamente l'orologio, è possibile ridurre il valore della proprietà <xref:System.Windows.Forms.Timer.Interval%2A> impostata nel passaggio 7 precedente.  
  
## Vedere anche  
 <xref:System.Windows.Forms.StatusBar>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 [Procedura: aggiungere pannelli a un controllo StatusBar](../../../../docs/framework/winforms/controls/how-to-add-panels-to-a-statusbar-control.md)   
 [Procedura: individuare il pannello selezionato nel controllo StatusBar Windows Form](../../../../docs/framework/winforms/controls/determine-which-panel-wf-statusbar-control-was-clicked.md)   
 [Cenni preliminari sul controllo StatusBar](../../../../docs/framework/winforms/controls/statusbar-control-overview-windows-forms.md)