---
title: "How to: Capture User Input from a PrintDialog at Run Time | Microsoft Docs"
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
  - "print options, changing at run time"
  - "printing [Windows Forms], options"
  - "print options"
  - "run time, changing print options"
ms.assetid: 438501d8-9a70-4fb3-aae6-e46579aba0c6
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# How to: Capture User Input from a PrintDialog at Run Time
Sebbene sia possibile impostare le opzioni connesse alla stampa in fase di progettazione, in determinati casi potrebbe essere necessario modificarle in fase di esecuzione, di solito in conseguenza di scelte dell'utente.  È possibile acquisire l'input dell'utente per la stampa di un documento utilizzando i componenti <xref:System.Windows.Forms.PrintDialog> e <xref:System.Drawing.Printing.PrintDocument>.  
  
### Per modificare le opzioni di stampa a livello di codice  
  
1.  Aggiungere un componente <xref:System.Windows.Forms.PrintDialog> e un componente <xref:System.Drawing.Printing.PrintDocument> al form.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.PrintDialog.Document%2A> dell'elemento <xref:System.Windows.Forms.PrintDialog> sul componente <xref:System.Drawing.Printing.PrintDocument> aggiunto al form.  
  
    ```vb  
    PrintDialog1.Document = PrintDocument1  
  
    ```  
  
    ```csharp  
    printDialog1.Document = PrintDocument1;  
  
    ```  
  
    ```cpp  
    printDialog1->Document = PrintDocument1;  
    ```  
  
3.  Visualizzare il componente <xref:System.Windows.Forms.PrintDialog> utilizzando il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>.  
  
    ```vb  
    PrintDialog1.ShowDialog()  
  
    ```  
  
    ```csharp  
    printDialog1.ShowDialog();  
  
    ```  
  
    ```cpp  
    printDialog1->ShowDialog();  
    ```  
  
4.  Le opzioni di stampa scelte dall'utente nella finestra di dialogo verranno copiate nella proprietà <xref:System.Drawing.Printing.PrinterSettings> del componente <xref:System.Drawing.Printing.PrintDocument>.  
  
## Vedere anche  
 [How to: Print a Multi\-Page Text File in Windows Forms](../../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)   
 [Windows Forms Print Support](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)