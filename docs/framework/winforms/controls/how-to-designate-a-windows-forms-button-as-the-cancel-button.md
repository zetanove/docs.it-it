---
title: "Procedura: impostare un pulsante Windows Form come pulsante di annullamento | Microsoft Docs"
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
  - "Button (controllo) [Windows Form], come pulsante Annulla"
  - "pulsanti, pulsanti Annulla"
ms.assetid: 252f0834-e54b-44d9-96f7-ee5f50e94f2c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: impostare un pulsante Windows Form come pulsante di annullamento
In qualsiasi Windows Form è possibile designare un controllo <xref:System.Windows.Forms.Button> come pulsante di annullamento.  Il pulsante di annullamento viene scelto ogni volta che si preme ESC, anche se lo stato attivo è detenuto da un altro controllo del form.  Il pulsante di annullamento viene in genere programmato per consentire all'utente di abbandonare l'esecuzione di un'operazione senza intraprendere un'azione specifica.  
  
### Per designare il pulsante di annullamento  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Form.CancelButton%2A> del form sul controllo <xref:System.Windows.Forms.Button> appropriato.  
  
    ```vb  
    Private Sub SetCancelButton(ByVal myCancelBtn As Button)  
       Me.CancelButton = myCancelBtn  
    End Sub  
    ```  
  
    ```csharp  
    private void SetCancelButton(Button myCancelBtn)  
    {  
       this.CancelButton = myCancelBtn;  
    }  
    ```  
  
    ```cpp  
    private:  
       void SetCancelButton(Button ^ myCancelBtn)  
       {  
          this->CancelButton = myCancelBtn;  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.Form.CancelButton%2A>   
 [Cenni preliminari sul controllo Button](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [Modalità di selezione di un controllo Button Windows Form](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [Procedura: rispondere alla selezione dei pulsanti di Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [Procedura: designare un pulsante Windows Form come pulsante di conferma](../../../../docs/framework/winforms/controls/how-to-designate-a-windows-forms-button-as-the-accept-button.md)   
 [Controllo Button](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)