---
title: "Procedura: visualizzare il componente PrintDialog | Microsoft Docs"
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
  - "Stampa (finestra di dialogo), visualizzazione"
  - "PrintDialog (componente) [Windows Form], visualizzazione"
  - "stampa [Windows Form], visualizzazione di finestre di dialogo per la stampa"
ms.assetid: 745a8db7-0526-4b21-b09d-18e13ed32014
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: visualizzare il componente PrintDialog
Il componente <xref:System.Windows.Forms.PrintDialog> rappresenta la finestra di dialogo per la stampa standard di Windows nota a molti utenti.  Poiché gli utenti saranno subito in grado di servirsene con facilità, l'utilizzo del componente <xref:System.Windows.Forms.PrintDialog> si rivela particolarmente vantaggioso.  
  
### Per visualizzare il componente PrintDialog  
  
-   Chiamare il metodo <xref:System.Windows.Forms.Form.ShowDialog%2A> dal codice dell'applicazione.  
  
     Una volta visualizzato il componente, gli utenti potranno utilizzarlo, impostando le proprietà del processo di stampa.  Queste proprietà vengono salvate nella classe [PrinterSettings](frlrfSystemDrawingPrintingPrinterSettingsMembersTopic), e nella classe [PageSettings](frlrfSystemDrawingPrintingPageSettingsMembersTopic) se l'utente accede a [Componente PageSetupDialog](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md) tramite il componente <xref:System.Windows.Forms.PrintDialog>, associata al processo di stampa.  Sarà quindi possibile effettuare delle chiamate alle proprietà così impostate per determinare le specifiche del processo di stampa.  
  
## Vedere anche  
 [How to: Create Standard Windows Forms Print Jobs](../../../../docs/framework/winforms/advanced/how-to-create-standard-windows-forms-print-jobs.md)   
 [How to: Capture User Input from a PrintDialog at Run Time](../../../../docs/framework/winforms/advanced/how-to-capture-user-input-from-a-printdialog-at-run-time.md)   
 [Controllo PrintPreviewDialog](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)   
 [Componente PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md)   
 [Windows Forms Print Support](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)   
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)