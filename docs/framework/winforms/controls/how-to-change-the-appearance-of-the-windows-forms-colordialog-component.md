---
title: "Procedura: modificare l&#39;aspetto del componente ColorDialog di Windows Form | Microsoft Docs"
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
  - "finestra di dialogo dei colori, configurazione dell'aspetto"
  - "ColorDialog (componente), esempi"
  - "ColorDialog (componente), formattazione dell'aspetto"
ms.assetid: bba4e262-1cd7-4f63-89cf-330a36f7b539
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: modificare l&#39;aspetto del componente ColorDialog di Windows Form
È possibile configurare l'aspetto e alcune delle proprietà del componente <xref:System.Windows.Forms.ColorDialog> di Windows Form.  La finestra di dialogo è composta da due sezioni: in una sono riportati i colori di base e nell'altra è possibile definire colori personalizzati.  
  
 La maggior parte delle proprietà limita il numero di colori che l'utente può selezionare dalla finestra di dialogo.  Se la proprietà <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A> è impostata su `true`, verrà consentito all'utente di definire colori personalizzati.  Se la proprietà <xref:System.Windows.Forms.ColorDialog.FullOpen%2A> è impostata su `true`, la finestra di dialogo verrà espansa per la definizione dei colori personalizzati. In caso contrario, sarà necessario scegliere il pulsante "Definisci colori personalizzati".  Quando la proprietà <xref:System.Windows.Forms.ColorDialog.AnyColor%2A> è impostata su `true`, nella finestra di dialogo vengono visualizzati tutti i colori disponibili nell'insieme dei colori di base.  Se la proprietà <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> è impostata su `true`, l'utente non potrà selezionare colori con retinatura e saranno disponibili soltanto colori a tinta unita.  
  
 Se la proprietà <xref:System.Windows.Forms.ColorDialog.ShowHelp%2A> è impostata su `true`, nella finestra di dialogo verrà visualizzato il pulsante ?.  Quando l'utente sceglie il pulsante ?, viene generato l'evento <xref:System.Windows.Forms.CommonDialog.HelpRequest> del componente <xref:System.Windows.Forms.ColorDialog>.  
  
### Per configurare l'aspetto della finestra di dialogo dei colori  
  
1.  Impostare le proprietà <xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A>, <xref:System.Windows.Forms.ColorDialog.AnyColor%2A>, <xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A> e <xref:System.Windows.Forms.ColorDialog.ShowHelp%2A> sui valori desiderati.  
  
    ```vb  
    ColorDialog1.AllowFullOpen = True  
    ColorDialog1.AnyColor = True  
    ColorDialog1.SolidColorOnly = False  
    ColorDialog1.ShowHelp = True  
  
    ```  
  
    ```csharp  
    colorDialog1.AllowFullOpen = true;  
    colorDialog1.AnyColor = true;  
    colorDialog1.SolidColorOnly = false;  
    colorDialog1.ShowHelp = true;  
  
    ```  
  
    ```cpp  
    colorDialog1->AllowFullOpen = true;  
    colorDialog1->AnyColor = true;  
    colorDialog1->SolidColorOnly = false;  
    colorDialog1->ShowHelp = true;  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ColorDialog>   
 [Componente ColorDialog](../../../../docs/framework/winforms/controls/colordialog-component-windows-forms.md)   
 [Cenni preliminari sul componente ColorDialog](../../../../docs/framework/winforms/controls/colordialog-component-overview-windows-forms.md)