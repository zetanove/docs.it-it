---
title: "Procedura: impostare le descrizioni comandi per i controlli in un Windows Form in fase di progettazione | Microsoft Docs"
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
  - "esempi [Windows Form], descrizioni comandi"
  - "descrizioni comandi [Windows Form], per i controlli"
ms.assetid: c4b60637-4c0a-44c2-a103-f66dff887936
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: impostare le descrizioni comandi per i controlli in un Windows Form in fase di progettazione
È possibile impostare una stringa <xref:System.Windows.Forms.ToolTip> nel codice o nella finestra di progettazione di Windows Form.  Per ulteriori informazioni sul componente <xref:System.Windows.Forms.ToolTip>, vedere [Cenni preliminari sul componente ToolTip](../../../../docs/framework/winforms/controls/tooltip-component-overview-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per impostare una descrizione comandi a livello di codice  
  
1.  Aggiungere il controllo con cui verrà visualizzata la descrizione comandi.  
  
2.  Utilizzare il metodo <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> del componente <xref:System.Windows.Forms.ToolTip>.  
  
    ```vb  
    ' In this example, Button1 is the control to display the ToolTip.  
    ToolTip1.SetToolTip(Button1, "Save changes")  
  
    ```  
  
    ```csharp  
    // In this example, button1 is the control to display the ToolTip.  
    toolTip1.SetToolTip(button1, "Save changes");  
  
    ```  
  
    ```cpp  
    // In this example, button1 is the control to display the ToolTip.  
    toolTip1->SetToolTip(button1, "Save changes");  
    ```  
  
### Per impostare una descrizione comandi nella finestra di progettazione  
  
1.  Aggiungere un componente <xref:System.Windows.Forms.ToolTip> al form.  
  
2.  Selezionare il controllo in cui verrà visualizzata la descrizione comandi oppure aggiungere il controllo al form.  
  
3.  Nella finestra **Proprietà** impostare il valore **ToolTip on ToolTip1** su una stringa di testo appropriata.  
  
## Vedere anche  
 [Cenni preliminari sul componente ToolTip](../../../../docs/framework/winforms/controls/tooltip-component-overview-windows-forms.md)   
 [Procedura: modificare il ritardo del componente ToolTip di Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)   
 [Componente ToolTip](../../../../docs/framework/winforms/controls/tooltip-component-windows-forms.md)