---
title: "Procedura: rispondere alla selezione dei pulsanti di Windows Form | Microsoft Docs"
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
  - "Button (controllo) [Windows Form], risposta click"
  - "pulsanti, risposta a eventi Click"
  - "Click (evento), Button (controllo)"
  - "Click (evento), risposta"
  - "doppio clic"
  - "eventi [Windows Form], eventi Click"
  - "esempi [Windows Form], controlli"
  - "MouseDown (evento)"
ms.assetid: 7a4951bd-369c-4662-b246-28ad83eda484
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: rispondere alla selezione dei pulsanti di Windows Form
La funzione principale di un controllo <xref:System.Windows.Forms.Button> di Windows Form consiste nell'esecuzione di codice quando si fa clic sul pulsante.  
  
 La selezione di un controllo <xref:System.Windows.Forms.Button> genera inoltre alcuni altri eventi, tra cui <xref:System.Windows.Forms.Control.MouseEnter>, <xref:System.Windows.Forms.Control.MouseDown> e <xref:System.Windows.Forms.Control.MouseUp>.  Durante l'associazione di gestori eventi per questi eventi correlati, è necessario verificare che le operazioni corrispondenti non siano in conflitto.  Se, ad esempio, scegliendo un pulsante si cancellano le informazioni digitate in una casella di testo, se il puntatore del mouse si sofferma sul pulsante non dovrà apparire la descrizione comando con le informazioni non più esistenti.  
  
 Se si fa doppio clic sul controllo <xref:System.Windows.Forms.Button>, ogni clic verrà elaborato singolarmente poiché il controllo non supporta l'evento generato dal doppio clic.  
  
### Per rispondere alla scelta di un pulsante  
  
-   Scrivere il codice da eseguire nel delegato `Click` <xref:System.EventHandler> del pulsante  in modo da associare `Button1_Click` al controllo.  Per ulteriori informazioni, vedere la classe [How to: Create Event Handlers at Run Time for Windows Forms](../../../../docs/framework/winforms/how-to-create-event-handlers-at-run-time-for-windows-forms.md).  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       MessageBox.Show("Button1 was clicked")  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       MessageBox.Show("button1 was clicked");  
    }  
    ```  
  
    ```cpp#  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          MessageBox::Show("button1 was clicked");  
       }  
    ```  
  
## Vedere anche  
 [Cenni preliminari sul controllo Button](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [Modalità di selezione di un controllo Button Windows Form](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [Controllo Button](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)