---
title: "Procedura: designare un pulsante Windows Form come pulsante di conferma utilizzando la finestra di progettazione | Microsoft Docs"
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
ms.assetid: a1da0590-755f-49f2-aca7-609fac6351bf
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: designare un pulsante Windows Form come pulsante di conferma utilizzando la finestra di progettazione
In qualsiasi Windows Form è possibile designare un controllo <xref:System.Windows.Forms.Button> come pulsante di conferma, ovvero come pulsante predefinito.  Ogni volta che si preme INVIO il pulsante predefinito viene scelto, anche se lo stato attivo è detenuto da un altro controllo del form.  L'unica eccezione si verifica se lo stato attivo è detenuto da un controllo che è a sua volta un pulsante \(in tal caso verrà scelto quest'ultimo\), una casella di testo a più righe oppure un controllo che intercetta il tasto INVIO.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per designare il pulsante di conferma  
  
1.  Fare clic sul form in cui si trova il pulsante.  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.Form.AcceptButton%2A> del form sul nome del controllo <xref:System.Windows.Forms.Button>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Form.AcceptButton%2A>   
 [Cenni preliminari sul controllo Button](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [Modalità di selezione di un controllo Button Windows Form](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)   
 [Procedura: rispondere alla selezione dei pulsanti di Windows Form](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [Procedura: designare un pulsante Windows Form come pulsante Annulla utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/designate-a-wf-button-as-the-cancel-button-using-the-designer.md)   
 [Controllo Button](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)