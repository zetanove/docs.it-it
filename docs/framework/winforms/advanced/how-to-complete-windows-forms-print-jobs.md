---
title: "How to: Complete Windows Forms Print Jobs | Microsoft Docs"
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
  - "print jobs, completing in Windows Forms"
  - "printing [Windows Forms], print jobs"
ms.assetid: 23ec74f7-34c5-4710-82a0-ee2914518548
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# How to: Complete Windows Forms Print Jobs
Spesso gli elaboratori di testo e altre applicazioni che eseguono processi di stampa offrono la possibilità di visualizzare un messaggio per informare l'utente che il processo di stampa è stato completato.  È possibile offrire questa funzionalità in Windows Form tramite la gestione dell'evento <xref:System.Drawing.Printing.PrintDocument.EndPrint> del componente <xref:System.Drawing.Printing.PrintDocument>.  
  
 La procedura seguente richiede la creazione di un'applicazione di Windows inclusiva di un componente <xref:System.Drawing.Printing.PrintDocument>, che rappresenta la modalità standard per consentire la stampa da un'applicazione di Windows.  Per ulteriori informazioni sulla stampa da Windows Form utilizzando il componente <xref:System.Drawing.Printing.PrintDocument>, vedere [How to: Create Standard Windows Forms Print Jobs](../../../../docs/framework/winforms/advanced/how-to-create-standard-windows-forms-print-jobs.md).  
  
### Per completare un processo di stampa  
  
1.  Impostare la proprietà <xref:System.Drawing.Printing.PrintDocument.DocumentName%2A> del componente <xref:System.Drawing.Printing.PrintDocument>.  
  
    ```vb  
    PrintDocument1.DocumentName = "MyTextFile"  
  
    ```  
  
    ```csharp  
    printDocument1.DocumentName = "MyTextFile";  
  
    ```  
  
    ```cpp  
    printDocument1->DocumentName = "MyTextFile";  
    ```  
  
2.  Scrivere il codice per gestire l'evento <xref:System.Drawing.Printing.PrintDocument.EndPrint>.  
  
     Nell'esempio seguente viene visualizzata una finestra di testo per segnalare che la stampa del documento è terminata.  
  
    ```vb  
    Private Sub PrintDocument1_EndPrint(ByVal sender As Object, ByVal e As System.Drawing.Printing.PrintEventArgs) Handles PrintDocument1.EndPrint  
       MessageBox.Show(PrintDocument1.DocumentName + " has finished printing.")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void printDocument1_EndPrint(object sender,   
    System.Drawing.Printing.PrintEventArgs e)  
    {  
       MessageBox.Show(printDocument1.DocumentName +   
          " has finished printing.");  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void printDocument1_EndPrint(System::Object ^ sender,  
          System::Drawing::Printing::PrintEventArgs ^ e)  
       {  
          MessageBox::Show(String::Concat(printDocument1->DocumentName,  
             " has finished printing."));  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore dell'evento.  
  
    ```csharp  
    this.printDocument1.EndPrint += new  
       System.Drawing.Printing.PrintEventHandler  
       (this.printDocument1_EndPrint);  
  
    ```  
  
    ```cpp  
    this->printDocument1->EndPrint += gcnew  
       System::Drawing::Printing::PrintEventHandler  
       (this, &Form1::printDocument1_EndPrint);  
    ```  
  
## Vedere anche  
 <xref:System.Drawing.Printing.PrintDocument>   
 [Windows Forms Print Support](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)