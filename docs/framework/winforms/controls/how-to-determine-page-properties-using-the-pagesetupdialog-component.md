---
title: "Procedura: definire le propriet&#224; della pagina con il componente PageSetupDialog | Microsoft Docs"
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
  - "proprietà della pagina"
  - "impostazione di pagina"
  - "PageSetupDialog (componente)"
ms.assetid: 6dae05bc-c0fd-4357-bb93-841a1631d98f
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: definire le propriet&#224; della pagina con il componente PageSetupDialog
Il componente [PageSetupDialog](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md) presenta layout, dimensioni del foglio e altre opzioni relative al layout di pagina per un documento.  
  
 È necessario specificare un'istanza della classe <xref:System.Drawing.Printing.PrintDocument>, che rappresenta il documento da stampare. È inoltre necessario che sul computer dell'utente sia installata una stampante, locale o di rete, tramite la quale il componente <xref:System.Windows.Forms.PageSetupDialog> determina in parte le scelte di formattazione della pagina presentate all'utente.  
  
 Un aspetto importante dell'uso del componente <xref:System.Windows.Forms.PageSetupDialog> è dato dalla modalità di interazione con la classe <xref:System.Drawing.Printing.PageSettings>. La classe <xref:System.Drawing.Printing.PageSettings> viene usata per specificare le impostazioni che modificano la modalità di stampa di una pagina, come l'orientamento, le dimensioni e i margini. Ciascuna di queste impostazioni è rappresentata come una proprietà della classe <xref:System.Drawing.Printing.PageSettings>. La classe <xref:System.Windows.Forms.PageSetupDialog> modifica i valori delle proprietà per una determinata istanza della classe <xref:System.Drawing.Printing.PageSettings>, che è associata al documento ed è rappresentata come proprietà <xref:System.Drawing.Printing.PrintDocument.DefaultPageSettings%2A>.  
  
### Per impostare le proprietà della pagina mediante il componente PageSetupDialog  
  
1.  Usare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> per aprire la finestra di dialogo, specificando l'oggetto <xref:System.Drawing.Printing.PrintDocument> desiderato.  
  
     Nell'esempio seguente il gestore eventi <xref:System.Windows.Forms.Control.Click> del controllo <xref:System.Windows.Forms.Button> apre un'istanza del componente <xref:System.Windows.Forms.PageSetupDialog>. Un documento esistente è specificato nella proprietà <xref:System.Windows.Forms.PageSetupDialog.Document%2A> e la relativa proprietà <xref:System.Drawing.Printing.PageSettings.Color%2A?displayProperty=fullName> è impostata su `false`.  
  
     Nell'esempio si presuppone che il form contenga un controllo <xref:System.Windows.Forms.Button>, un componente <xref:System.Drawing.Printing.PrintDocument> denominato `myDocument` e un componente <xref:System.Windows.Forms.PageSetupDialog>.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles Button1.Click  
       ' The print document 'myDocument' used below  
       ' is merely for an example.  
       'You will have to specify your own print document.  
       PageSetupDialog1.Document = myDocument  
       ' Sets the print document's color setting to false,  
       ' so that the page will not be printed in color.  
       PageSetupDialog1.Document.DefaultPageSettings.Color = False  
       PageSetupDialog1.ShowDialog()  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       // The print document 'myDocument' used below  
       // is merely for an example.  
       // You will have to specify your own print document.  
       pageSetupDialog1.Document = myDocument;  
       // Sets the print document's color setting to false,  
       // so that the page will not be printed in color.  
       pageSetupDialog1.Document.DefaultPageSettings.Color = false;  
       pageSetupDialog1.ShowDialog();  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void button1_Click(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // The print document 'myDocument' used below  
          // is merely for an example.  
          // You will have to specify your own print document.  
          pageSetupDialog1->Document = myDocument;  
          // Sets the print document's color setting to false,  
          // so that the page will not be printed in color.  
          pageSetupDialog1->Document->DefaultPageSettings->Color = false;  
          pageSetupDialog1->ShowDialog();  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click += gcnew   
       System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.PageSetupDialog>   
 [How to: Create Standard Windows Forms Print Jobs](../../../../docs/framework/winforms/advanced/how-to-create-standard-windows-forms-print-jobs.md)   
 [Componente PageSetupDialog](../../../../docs/framework/winforms/controls/pagesetupdialog-component-windows-forms.md)