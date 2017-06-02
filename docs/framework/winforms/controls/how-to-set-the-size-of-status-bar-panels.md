---
title: "Procedura: impostare la dimensione dei pannelli della barra di stato | Microsoft Docs"
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
  - "pannelli, impostazione delle dimensioni in barre di stato"
  - "barre di stato, impostazione delle dimensioni del pannello"
  - "StatusBar (controllo) [Windows Form], dimensione del pannello"
ms.assetid: a01bee43-d9eb-4954-84e6-45a93532d08d
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: impostare la dimensione dei pannelli della barra di stato
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.ToolStripStatusLabel> sostituisca il controllo <xref:System.Windows.Forms.StatusBar> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.StatusBar> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 Ciascuna istanza della classe <xref:System.Windows.Forms.StatusBarPanel> all'interno di un controllo [Controllo StatusBar](../../../../docs/framework/winforms/controls/statusbar-control-windows-forms.md) dispone di un determinato numero di proprietà dinamiche che ne stabiliscono la larghezza e il ridimensionamento in fase di esecuzione.  
  
### Per impostare le dimensioni di un pannello  
  
1.  Nella routine impostare le proprietà <xref:System.Windows.Forms.StatusBarPanel.AutoSize%2A>, <xref:System.Windows.Forms.StatusBarPanel.MinWidth%2A> e <xref:System.Windows.Forms.StatusBarPanel.Width%2A> \(o eventuali subset inclusi al loro interno\) per i pannelli della barra di stato utilizzando il relativo indice passato alla proprietà <xref:System.Windows.Forms.StatusBar.Panels%2A> della raccolta <xref:System.Windows.Forms.StatusBarPanel>.  
  
    ```vb  
    Public Sub SetStatusBarPanelSize()  
    ' Create panel and set text property.  
       StatusBar1.Panels.Add("One")  
    ' Set properties of panels.  
       StatusBar1.Panels(0).AutoSize = StatusBarPanelAutoSize.Spring  
       StatusBar1.Panels(0).Width = 200  
    ' Enable the StatusBar control to display panels.  
       StatusBar1.ShowPanels = True  
        End Sub  
  
    ```  
  
    ```csharp  
    public void SetStatusBarPanelSize()  
    {  
       // Create panel and set text property.  
       statusBar1.Panels.Add("One");  
       // Set properties of panels.  
       statusBar1.Panels[0].AutoSize = StatusBarPanelAutoSize.Spring;  
       statusBar1.Panels[0].Width = 200;  
       statusBar1.ShowPanels = true;  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void SetStatusBarPanelSize()  
       {  
          // Create panel and set text property.  
          statusBar1->Panels->Add("One");  
          // Set properties of panels.  
          statusBar1->Panels[0]->AutoSize =  
             StatusBarPanelAutoSize::Spring;  
          statusBar1->Panels[0]->Width = 200;  
          statusBar1->ShowPanels = true;  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.StatusBar>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 [Procedura dettagliata: aggiornamento delle informazioni sulla barra di stato in fase di esecuzione](../../../../docs/framework/winforms/controls/walkthrough-updating-status-bar-information-at-run-time.md)   
 [Procedura: individuare il pannello selezionato nel controllo StatusBar Windows Form](../../../../docs/framework/winforms/controls/determine-which-panel-wf-statusbar-control-was-clicked.md)   
 [Cenni preliminari sul controllo StatusBar](../../../../docs/framework/winforms/controls/statusbar-control-overview-windows-forms.md)