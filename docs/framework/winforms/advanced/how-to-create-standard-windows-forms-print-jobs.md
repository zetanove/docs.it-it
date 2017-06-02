---
title: "How to: Create Standard Windows Forms Print Jobs | Microsoft Docs"
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
  - "printing [Windows Forms]"
  - "printing [Windows Forms], creating print jobs"
  - "printing [Visual Basic], in Windows applications"
ms.assetid: 03342b90-9cfe-40b2-838b-b479a13c5dea
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# How to: Create Standard Windows Forms Print Jobs
Alla base del concetto di stampa in Windows Form c'è il componente <xref:System.Drawing.Printing.PrintDocument>, più specificatamente l'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage>.  Tramite la scrittura di codice per la gestione dell'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage> è possibile specificare il materiale da stampare e la modalità di stampa da utilizzare.  
  
### Per creare un processo di stampa  
  
1.  Aggiungere un componente <xref:System.Drawing.Printing.PrintDocument> al form.  
  
2.  Scrivere il codice per gestire l'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage>.  
  
     È necessario codificare la logica di stampa personalizzata.  e specificare il materiale da stampare.  
  
     Nell'esempio di codice seguente viene creato un elemento grafico di esempio \(un rettangolo rosso\) nel gestore eventi <xref:System.Drawing.Printing.PrintDocument.PrintPage> che viene specificato come materiale da stampare.  
  
    ```vb  
    Private Sub PrintDocument1_PrintPage(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintPageEventArgs) Handles PrintDocument1.PrintPage  
       e.Graphics.FillRectangle(Brushes.Red, New Rectangle(500, 500, 500, 500))  
    End Sub  
  
    ```  
  
    ```csharp  
    private void printDocument1_PrintPage(object sender,   
    System.Drawing.Printing.PrintPageEventArgs e)  
    {  
       e.Graphics.FillRectangle(Brushes.Red,   
         new Rectangle(500, 500, 500, 500));  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_PrintPage(System::Object ^ sender,  
          System::Drawing::Printing::PrintPageEventArgs ^ e)  
       {  
          e->Graphics->FillRectangle(Brushes::Red,  
             Rectangle(500, 500, 500, 500));  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore dell'evento.  
  
    ```csharp  
    this.printDocument1.PrintPage += new  
       System.Drawing.Printing.PrintPageEventHandler  
       (this.printDocument1_PrintPage);  
  
    ```  
  
    ```cpp  
    printDocument1->PrintPage += gcnew  
       System::Drawing::Printing::PrintPageEventHandler  
       (this, &Form1::printDocument1_PrintPage);  
    ```  
  
     È inoltre possibile scrivere codice per gli eventi <xref:System.Drawing.Printing.PrintDocument.BeginPrint> e <xref:System.Drawing.Printing.PrintDocument.EndPrint>, includendo eventualmente un intero che rappresenta il numero totale di pagine da stampare e che diminuisce man mano che vengono stampate le pagine.  
  
    > [!NOTE]
    >  È possibile aggiungere un componente <xref:System.Windows.Forms.PrintDialog> al form, per fornire un'interfaccia utente chiara ed efficiente.  Impostando la proprietà <xref:System.Windows.Forms.PrintDialog.Document%2A> del componente <xref:System.Windows.Forms.PrintDialog> è possibile impostare le proprietà correlate al documento da stampare utilizzato nel form.  Per ulteriori informazioni sul componente <xref:System.Windows.Forms.PrintDialog>, vedere [Componente PrintDialog](../../../../docs/framework/winforms/controls/printdialog-component-windows-forms.md).  
  
     Per ulteriori informazioni sulle specifiche relative ai processi di stampa nei Windows Form, incluse le modalità di creazione di un processo di stampa a livello di codice, vedere <xref:System.Drawing.Printing.PrintPageEventArgs>.  
  
## Vedere anche  
 <xref:System.Drawing.Printing.PrintDocument>   
 [Windows Forms Print Support](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)