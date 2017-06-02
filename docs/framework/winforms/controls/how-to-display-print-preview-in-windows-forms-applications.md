---
title: "Procedura: visualizzare l&#39;anteprima di stampa nelle applicazioni di Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], anteprima di stampa"
  - "anteprima di stampa, visualizzazione"
  - "stampa [Windows Form], anteprima di stampa"
ms.assetid: e394134c-0886-4517-bd8d-edc4a3749eb5
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: visualizzare l&#39;anteprima di stampa nelle applicazioni di Windows Form
È possibile utilizzare il controllo <xref:System.Windows.Forms.PrintPreviewDialog> per consentire agli utenti di visualizzare un documento, spesso prima che questo venga stampato.  
  
 A tale scopo, è necessario specificare un'istanza della classe <xref:System.Drawing.Printing.PrintDocument>, che rappresenta il documento da stampare.  Per ulteriori informazioni sull'utilizzo dell'anteprima di stampa con il componente <xref:System.Drawing.Printing.PrintDocument>, vedere [Procedura: stampare in Windows Form tramite l'anteprima di stampa](../../../../docs/framework/winforms/advanced/how-to-print-in-windows-forms-using-print-preview.md).  
  
> [!NOTE]
>  Per utilizzare il controllo <xref:System.Windows.Forms.PrintPreviewDialog> in fase di esecuzione, è necessario che gli utenti dispongano di una stampante installata sul computer, sia locale che di rete, poiché ciò, parzialmente, consente al componente <xref:System.Windows.Forms.PrintPreviewDialog> di determinare in che modo verrà stampato un documento.  
  
 Il controllo <xref:System.Windows.Forms.PrintPreviewDialog> utilizza la classe <xref:System.Drawing.Printing.PrinterSettings>.  Inoltre il controllo <xref:System.Windows.Forms.PrintPreviewDialog> utilizza la classe <xref:System.Drawing.Printing.PageSettings>, proprio come il componente <xref:System.Windows.Forms.PrintPreviewDialog>.  Il documento di stampa specificato nella proprietà <xref:System.Windows.Forms.PrintPreviewControl.Document%2A> del controllo <xref:System.Windows.Forms.PrintPreviewDialog> fa riferimento alle istanze di entrambe le classi <xref:System.Drawing.Printing.PrinterSettings> e <xref:System.Drawing.Printing.PageSettings>, che vengono utilizzate per eseguire il rendering del documento nella finestra di anteprima.  
  
### Per visualizzare le pagine con il controllo PrintPreviewDialog  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> per aprire la finestra di dialogo, specificando quale <xref:System.Drawing.Printing.PrintDocument> utilizzare.  
  
     Nell'esempio di codice seguente il gestore dell'evento <xref:System.Windows.Forms.Control.Click> del controllo <xref:System.Windows.Forms.Button> apre un'istanza del controllo <xref:System.Windows.Forms.PrintPreviewDialog>.  Il documento di stampa è specificato nella proprietà <xref:System.Windows.Forms.PrintDialog.Document%2A>.  Nell'esempio seguente non viene specificato alcun documento.  
  
     Nell'esempio il form deve contenere un controllo <xref:System.Windows.Forms.Button>, un componente <xref:System.Drawing.Printing.PrintDocument> denominato `myDocument` e un controllo <xref:System.Windows.Forms.PrintPreviewDialog>.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles Button1.Click  
       ' The print document 'myDocument' used below  
       ' is merely for an example.  
       ' You will have to specify your own print document.  
       PrintPreviewDialog1.Document = myDocument  
       PrintPreviewDialog1.ShowDialog()  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // The print document 'myDocument' used below  
       // is merely for an example.  
       // You will have to specify your own print document.  
       printPreviewDialog1.Document = myDocument;  
       printPreviewDialog1.ShowDialog();  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void button1_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // The print document 'myDocument' used below  
          // is merely for an example.  
          // You will have to specify your own print document.  
          printPreviewDialog1->Document = myDocument;  
          printPreviewDialog1->ShowDialog();  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew  
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## Vedere anche  
 [Componente PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md)   
 [Controllo PrintPreviewDialog](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)   
 [Windows Forms Print Support](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)   
 [Windows Form](../../../../docs/framework/winforms/index.md)