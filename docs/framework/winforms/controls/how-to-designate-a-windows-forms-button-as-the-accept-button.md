---
title: "Procedura: designare un pulsante Windows Form come pulsante di conferma | Microsoft Docs"
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
  - "pulsante di conferma in Windows Form"
  - "Button (controllo) [Windows Form], come pulsante predefinito"
  - "pulsanti, predefinite di Windows Form"
  - "controlli Windows Form, pulsante predefinito su form"
ms.assetid: 22cc9da6-b913-4e04-9554-dee443ac5c3a
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: designare un pulsante Windows Form come pulsante di conferma
In qualsiasi Windows Form è possibile designare un controllo <xref:System.Windows.Forms.Button> come pulsante di conferma, ovvero come pulsante predefinito.  Ogni volta che si preme INVIO il pulsante predefinito viene scelto, anche se lo stato attivo è detenuto da un altro controllo del form.  
  
> [!NOTE]
>  L'unica eccezione si verifica se lo stato attivo è detenuto da un controllo che è a sua volta un pulsante \(in tal caso verrà scelto quest'ultimo\), una casella di testo a più righe oppure un controllo che intercetta il tasto INVIO.  
  
### Per designare il pulsante di conferma  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Form.AcceptButton%2A> del form sul controllo <xref:System.Windows.Forms.Button> appropriato.  
  
    ```vb  
    Private Sub SetDefault(ByVal myDefaultBtn As Button)  
      Me.AcceptButton = myDefaultBtn   
    End Sub  
    ```  
  
    ```csharp  
    private void SetDefault(Button myDefaultBtn)  
    {  
       this.AcceptButton = myDefaultBtn;  
    }  
    ```  
  
    ```cpp  
    private:  
       void SetDefault(Button ^ myDefaultBtn)  
       {  
          this->AcceptButton = myDefaultBtn;  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.Form.AcceptButton%2A>   
 [Cenni preliminari sul controllo Button](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [Modalità di selezione di un controllo Button Windows Form](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [Procedura: rispondere alla selezione dei pulsanti di Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [Procedura: impostare un pulsante Windows Form come pulsante di annullamento](../../../../docs/framework/winforms/controls/how-to-designate-a-windows-forms-button-as-the-cancel-button.md)   
 [Controllo Button](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)