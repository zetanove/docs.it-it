---
title: "Windows Forms Print Support | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Windows Forms, printing"
  - "printing [Windows Forms]"
  - "forms, printing (using designer)"
  - "printing, Windows Forms, support"
  - "printing [Windows Forms], print support"
ms.assetid: a4a2960c-eb70-48e2-b641-cfb222704e46
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Windows Forms Print Support
La stampa in Windows Form consiste principalmente nell'utilizzo del componente [Componente PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md), che consente all'utente di stampare, e del controllo [Controllo PrintPreviewDialog](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md) e dei componenti [Componente PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md) e [Componente PageSetupDialog](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md) che forniscono un'interfaccia grafica di semplice utilizzo per gli utenti abituati al sistema operativo Windows.  
  
 In genere viene creata un nuova istanza del componente <xref:System.Drawing.Printing.PrintDocument>, vengono impostate le proprietà che descrivono il materiale da stampare utilizzando le classi <xref:System.Drawing.Printing.PrinterSettings> e <xref:System.Drawing.Printing.PageSettings> e viene chiamato il metodo <xref:System.Drawing.Printing.PrintDocument.Print%2A> per stampare il documento.  
  
 Durante la stampa da un'applicazione basata su Windows, il componente <xref:System.Drawing.Printing.PrintDocument> consentirà di visualizzare una finestra di dialogo di interruzione di stampa per avvisare che il processo di stampa è in esecuzione e può essere eventualmente annullato.  
  
## In questa sezione  
 [How to: Create Standard Windows Forms Print Jobs](../../../../docs/framework/winforms/advanced/how-to-create-standard-windows-forms-print-jobs.md)  
 Vengono fornite informazioni su come utilizzare il componente <xref:System.Drawing.Printing.PrintDocument> per stampare da un Windows Form.  
  
 [How to: Capture User Input from a PrintDialog at Run Time](../../../../docs/framework/winforms/advanced/how-to-capture-user-input-from-a-printdialog-at-run-time.md)  
 Viene illustrato come modificare a livello di codice le opzioni di stampa selezionate utilizzando il componente <xref:System.Windows.Forms.PrintDialog>.  
  
 [Procedura: selezionare le stampanti connesse al computer dell'utente in Windows Form](../../../../docs/framework/winforms/advanced/how-to-choose-the-printers-attached-to-user-computer-in-windows-forms.md)  
 Viene descritto come selezionare la stampante utilizzando il componente <xref:System.Windows.Forms.PrintDialog> in fase di esecuzione.  
  
 [How to: Print Graphics in Windows Forms](../../../../docs/framework/winforms/advanced/how-to-print-graphics-in-windows-forms.md)  
 Viene fornita una descrizione relativa all'invio di grafica alla stampante.  
  
 [How to: Print a Multi\-Page Text File in Windows Forms](../../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)  
 Viene fornita una descrizione relativa all'invio di testo alla stampante.  
  
 [How to: Complete Windows Forms Print Jobs](../../../../docs/framework/winforms/advanced/how-to-complete-windows-forms-print-jobs.md)  
 Vengono fornite informazioni su come notificare agli utenti il completamento di un processo di stampa.  
  
 [How to: Print a Windows Form](../../../../docs/framework/winforms/advanced/how-to-print-a-windows-form.md)  
 Viene illustrato come stampare una copia del form corrente.  
  
 [Procedura: stampare in Windows Form tramite l'anteprima di stampa](../../../../docs/framework/winforms/advanced/how-to-print-in-windows-forms-using-print-preview.md)  
 Viene illustrato come utilizzare una classe <xref:System.Windows.Forms.PrintPreviewDialog> per la stampa di un documento.  
  
## Sezioni correlate  
 [Componente PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md)  
 Vengono fornite informazioni sull'utilizzo del componente <xref:System.Drawing.Printing.PrintDocument>.  
  
 [Componente PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md)  
 Vengono fornite informazioni sull'utilizzo del componente <xref:System.Windows.Forms.PrintDialog>.  
  
 [Controllo PrintPreviewDialog](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)  
 Vengono fornite informazioni sull'utilizzo del controllo <xref:System.Windows.Forms.PrintPreviewDialog>.  
  
 [Componente PageSetupDialog](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md)  
 Vengono fornite informazioni sull'utilizzo del componente <xref:System.Windows.Forms.PageSetupDialog>.  
  
 <xref:System.Drawing.Printing>  
 Vengono descritte le classi dello spazio dei nomi <xref:System.Drawing.Printing>.