---
title: "Procedura: individuare il pannello selezionato nel controllo StatusBar Windows Form | Microsoft Docs"
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
  - "Panel (controllo) [Windows Form], rilevamento clic del mouse"
  - "PanelClick (evento), rilevamento pannello selezionato"
  - "pannelli, rilevamento clic del mouse"
  - "barre di stato, rilevamento pannello selezionato"
  - "StatusBar (controllo) [Windows Form], codifica di eventi di scelta di pannelli"
  - "StatusBar (controllo) [Windows Form], rilevamento pannello selezionato"
ms.assetid: d14c6092-04b2-4a07-8ddf-0dd11277ff5f
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: individuare il pannello selezionato nel controllo StatusBar Windows Form
> [!IMPORTANT]
>  Benché i controlli <xref:System.Windows.Forms.StatusStrip> e <xref:System.Windows.Forms.ToolStripStatusLabel> sostituiscano i controlli <xref:System.Windows.Forms.StatusBar> e <xref:System.Windows.Forms.StatusBarPanel> delle versioni precedenti aggiungendo funzionalità, i controlli <xref:System.Windows.Forms.StatusBar> e <xref:System.Windows.Forms.StatusBarPanel> vengono mantenuti per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  
  
 Per programmare il controllo [Controllo StatusBar](../../../../docs/framework/winforms/controls/statusbar-control-windows-forms.md) in modo da rispondere ai clic dell'utente, utilizzare un'istruzione case all'interno dell'evento <xref:System.Windows.Forms.StatusBar.PanelClick>.  L'evento contiene un argomento, l'argomento del pannello, che include un riferimento all'oggetto selezionato <xref:System.Windows.Forms.StatusBarPanel>.  Utilizzando questo riferimento, è possibile determinare l'indice del pannello selezionato ed eseguire la programmazione di conseguenza.  
  
> [!NOTE]
>  Verificare che la proprietà <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> del controllo <xref:System.Windows.Forms.StatusBar> sia impostata su `true`.  
  
### Per individuare il pannello selezionato  
  
1.  Nel gestore eventi <xref:System.Windows.Forms.StatusBar.PanelClick> utilizzare un'istruzione `Select Case` \(in [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\) oppure `switch case` \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] o [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) per determinare quale pannello è stato selezionato esaminando l'indice del pannello selezionato negli argomenti dell'evento.  
  
     Per l'esempio di codice riportato di seguito è necessario che sul form siano presenti un controllo <xref:System.Windows.Forms.StatusBar>, `StatusBar1` e due oggetti <xref:System.Windows.Forms.StatusBarPanel>,`StatusBarPanel1` e`StatusBarPanel2`.  
  
    ```vb  
    Private Sub StatusBar1_PanelClick(ByVal sender As System.Object, ByVal e As System.Windows.Forms.StatusBarPanelClickEventArgs) Handles StatusBar1.PanelClick  
       Select Case StatusBar1.Panels.IndexOf(e.StatusBarPanel)  
         Case 0  
           MessageBox.Show("You have clicked Panel One.")  
         Case 1  
           MessageBox.Show("You have clicked Panel Two.")  
       End Select  
    End Sub  
  
    ```  
  
    ```csharp  
    private void statusBar1_PanelClick(object sender,   
    System.Windows.Forms.StatusBarPanelClickEventArgs e)  
    {  
       switch (statusBar1.Panels.IndexOf(e.StatusBarPanel))  
       {  
          case 0 :  
             MessageBox.Show("You have clicked Panel One.");  
             break;  
          case 1 :  
             MessageBox.Show("You have clicked Panel Two.");  
             break;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void statusBar1_PanelClick(System::Object ^  sender,  
          System::Windows::Forms::StatusBarPanelClickEventArgs ^  e)  
       {  
          switch (statusBar1->Panels->IndexOf(e->StatusBarPanel))  
          {  
             case 0 :  
                MessageBox::Show("You have clicked Panel One.");  
                break;  
             case 1 :  
                MessageBox::Show("You have clicked Panel Two.");  
                break;  
          }  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.statusBar1.PanelClick += new   
       System.Windows.Forms.StatusBarPanelClickEventHandler   
       (this.statusBar1_PanelClick);  
  
    ```  
  
    ```cpp  
    this->statusBar1->PanelClick += gcnew  
       System::Windows::Forms::StatusBarPanelClickEventHandler  
       (this, &Form1::statusBar1_PanelClick);  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.StatusBar>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 [Procedura: impostare la dimensione dei pannelli della barra di stato](../../../../docs/framework/winforms/controls/how-to-set-the-size-of-status-bar-panels.md)   
 [Procedura dettagliata: aggiornamento delle informazioni sulla barra di stato in fase di esecuzione](../../../../docs/framework/winforms/controls/walkthrough-updating-status-bar-information-at-run-time.md)   
 [Cenni preliminari sul controllo StatusBar](../../../../docs/framework/winforms/controls/statusbar-control-overview-windows-forms.md)