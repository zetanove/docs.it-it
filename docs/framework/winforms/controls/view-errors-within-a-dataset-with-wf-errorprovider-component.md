---
title: "Procedura: visualizzare errori in un dataset tramite il componente ErrorProvider di Windows Form | Microsoft Docs"
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
  - "messaggi di errore, visualizzazione in dataset"
  - "ErrorProvider (componente) [Windows Form], errori dataset"
  - "errori [Windows Form], errori dataset"
ms.assetid: cbae023f-d651-4210-bdea-bcc5f037e321
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: visualizzare errori in un dataset tramite il componente ErrorProvider di Windows Form
È possibile utilizzare il componente <xref:System.Windows.Forms.ErrorProvider> di Windows Form per visualizzare errori di colonna in un dataset o in altre origini dati.  Perché un componente <xref:System.Windows.Forms.ErrorProvider> visualizzi errori dei dati in un form, non deve essere associato direttamente a un altro controllo.  Una volta associato a un'origine dati, è in grado di visualizzare un'icona di errore accanto a qualsiasi controllo associato alla stessa origine dati.  
  
> [!NOTE]
>  Se si modificano le proprietà <xref:System.Windows.Forms.ErrorProvider.DataSource%2A> e <xref:System.Windows.Forms.ErrorProvider.DataMember%2A> del provider degli errori in fase di esecuzione, è necessario utilizzare il metodo <xref:System.Windows.Forms.ErrorProvider.BindToDataAndErrors%2A> per evitare conflitti.  
  
### Per visualizzare errori di dati  
  
1.  Associare il componente a una specifica colonna in una tabella di dati.  
  
    ```vb  
    ' Assumes existence of DataSet1, DataTable1  
    TextBox1.DataBindings.Add("Text", DataSet1, "Customers.Name")  
    ErrorProvider1.DataSource = DataSet1  
    ErrorProvider1.DataMember = "Customers"  
  
    ```  
  
    ```csharp  
    // Assumes existence of DataSet1, DataTable1  
    textBox1.DataBindings.Add("Text", DataSet1, "Customers.Name");  
    errorProvider1.DataSource = DataSet1;  
    errorProvider1.DataMember = "Customers";  
  
    ```  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> sul form.  
  
    ```vb  
    ErrorProvider1.ContainerControl = Me  
  
    ```  
  
    ```csharp  
    errorProvider1.ContainerControl = this;  
  
    ```  
  
3.  Impostare il percorso del record corrente su una riga che contenga un errore di colonna.  
  
    ```vb  
    DataTable1.Rows(5).SetColumnError("Name", "Bad data in this row.")  
    Me.BindingContext(DataTable1).Position = 5  
  
    ```  
  
    ```csharp  
    DataTable1.Rows[5].SetColumnError("Name", "Bad data in this row.");  
    this.BindingContext [DataTable1].Position = 5;  
  
    ```  
  
## Vedere anche  
 [Cenni preliminari sul componente ErrorProvider](../../../../docs/framework/winforms/controls/errorprovider-component-overview-windows-forms.md)   
 [Procedura: visualizzare le icone di errori per la convalida dei form con il componente ErrorProvider di Windows Form](../../../../docs/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider.md)