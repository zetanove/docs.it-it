---
title: "Cenni preliminari sul componente PrintDocument (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "PrintDocument"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "PrintDocument (componente) [Windows Form], informazioni sul componente PrintDocument"
  - "stampa [Windows Form], PrintDocument (componente)"
ms.assetid: b59b4b60-dce5-42ca-8421-3a54a2f7bab0
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Cenni preliminari sul componente PrintDocument (Windows Form)
Il componente [PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md) di Windows Form viene utilizzato per impostare le proprietà che descrivono cosa stampare e per stampare il documento nelle applicazioni Windows.  Può essere usato insieme al componente [PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md) per controllare tutti gli aspetti della stampa dei documenti.  
  
## Utilizzo del componente PrintDocument  
 Due degli scenari principali che prevedono l'utilizzo del componente <xref:System.Drawing.Printing.PrintDocument> sono:  
  
-   Processi di stampa semplici, come la stampa di un singolo file di testo.  In questo caso aggiungere il componente <xref:System.Drawing.Printing.PrintDocument> a un Windows Form, quindi aggiungere la logica di programmazione per stampare un file nel gestore eventi <xref:System.Drawing.Printing.PrintDocument.PrintPage>.  La logica di programmazione deve culminare con il metodo <xref:System.Drawing.Printing.PrintDocument.Print%2A> per la stampa del documento.  Questo metodo invia alla stampante un oggetto <xref:System.Drawing.Graphics>, contenuto nella proprietà <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> della classe <xref:System.Drawing.Printing.PrintPageEventArgs>.  Per un esempio che mostra come stampare un documento di testo utilizzando il componente <xref:System.Drawing.Printing.PrintDocument>, vedere [How to: Print a Multi\-Page Text File in Windows Forms](../../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md).  
  
-   Processi di stampa più complessi, come i casi in cui è necessario riutilizzare la logica di stampa creata.  In questo caso derivare un nuovo componente dal componente <xref:System.Drawing.Printing.PrintDocument> ed eseguire l'override dell'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage> \(vedere [Overrides](../Topic/Overrides%20\(Visual%20Basic\).md) per Visual Basic o [override](../Topic/override%20\(C%23%20Reference\).md) per C\#\).  
  
 Quando viene aggiunto a un form, il componente <xref:System.Drawing.Printing.PrintDocument> è visualizzato nella barra delle applicazioni nella parte inferiore di Progettazione Windows Form.  
  
## Vedere anche  
 <xref:System.Drawing.Graphics>   
 <xref:System.Drawing.Printing.PrintDocument>   
 [Windows Forms Print Support](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)   
 [Componente PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md)