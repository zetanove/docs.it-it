---
title: "Procedura: creare una casella di testo in sola lettura (Windows Form) | Microsoft Docs"
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
  - "caselle di testo in sola lettura"
  - "caselle di testo, sola lettura"
  - "TextBox (controllo) [Windows Form], sola lettura"
ms.assetid: 60baa9ab-fa57-44ad-bb7c-61b05aa64296
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare una casella di testo in sola lettura (Windows Form)
È possibile trasformare una casella di testo modificabile di Windows Form in un controllo in sola lettura.  Nella casella di testo, ad esempio, potrebbe essere visualizzato un valore che normalmente è modificato, ma che non lo è attualmente a causa dello stato dell'applicazione.  
  
### Per creare una casella di testo in sola lettura  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.ReadOnly%2A> del controllo <xref:System.Windows.Forms.TextBox> su `true`.  Se la proprietà è impostata su `true`, gli utenti potranno comunque scorrere ed evidenziare il testo all'interno di una casella di testo in cui non sono consentite modifiche.  Nella casella di testo è possibile utilizzare il comando **Copia**, mentre non è consentito scegliere i comandi **Taglia** e **Incolla**.  
  
    > [!NOTE]
    >  La proprietà <xref:System.Windows.Forms.TextBoxBase.ReadOnly%2A> ha effetto solo sull'interazione dell'utente in fase di esecuzione.  È possibile modificare il contenuto delle caselle di testo a livello di codice in fase di esecuzione, modificando la proprietà <xref:System.Windows.Forms.TextBox.Text%2A> della casella di testo.  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextBox>   
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [Procedura: controllare il punto di inserimento in un controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo Password con il controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [Procedura: inserire virgolette in una stringa](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [Procedura: selezionare testo nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [Procedura: visualizzare più righe nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)   
 [Controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)