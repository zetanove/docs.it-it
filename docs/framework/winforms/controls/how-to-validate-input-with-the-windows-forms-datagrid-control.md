---
title: "Procedura: convalidare l&#39;input con il controllo DataGrid Windows Form | Microsoft Docs"
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
  - "DataGrid (controllo) [Windows Form], esempi"
  - "DataGrid (controllo) [Windows Form], convalida dell'input"
  - "esempi [Windows Form], controllo DataGrid"
  - "input utente, convalida"
  - "convalida, input utente"
ms.assetid: f1e9c3a0-d0a1-4893-a615-b4b0db046c63
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: convalidare l&#39;input con il controllo DataGrid Windows Form
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Sono disponibili due tipi di convalida dell'input per il controllo <xref:System.Windows.Forms.DataGrid> Windows Form.  Se l'utente tenta di immettere un valore relativo a un tipo di dati inaccettabile per la cella, ad esempio una stringa anziché un intero, il nuovo valore non valido verrà sostituito con il valore precedente.  Questa convalida dell'input viene eseguita automaticamente e non può essere personalizzata.  
  
 L'altro tipo di convalida dell'input può essere utilizzato per rifiutare tutti i dati inaccettabili, ad esempio un valore 0 in un campo che deve essere maggiore o uguale a 1 oppure una stringa non corretta.  Questa operazione viene eseguita nel dataset mediante la scrittura di un gestore eventi per l'evento <xref:System.Data.DataTable.ColumnChanging> o <xref:System.Data.DataTable.RowChanging>.  Nell'esempio qui di seguito viene utilizzato l'evento <xref:System.Data.DataTable.ColumnChanging>, poiché il valore non accettabile non viene ammesso specificamente per la colonna "Product".  È possibile utilizzare l'evento <xref:System.Data.DataTable.RowChanging> per verificare che il valore di una colonna "End Date" sia successivo a quello della colonna "Start Date", presente nella stessa riga.  
  
### Per convalidare l'input dell'utente  
  
1.  Scrivere il codice per gestire l'evento <xref:System.Data.DataTable.ColumnChanging> della tabella interessata.  Quando viene rilevato un input non corretto, chiamare il metodo <xref:System.Data.DataRow.SetColumnError%2A> dell'oggetto <xref:System.Data.DataRow>.  
  
    ```vb  
    Private Sub Customers_ColumnChanging(ByVal sender As Object, _  
    ByVal e As System.Data.DataColumnChangeEventArgs)  
       ' Only check for errors in the Product column  
       If (e.Column.ColumnName.Equals("Product")) Then  
          ' Do not allow "Automobile" as a product.  
          If CType(e.ProposedValue, String) = "Automobile" Then  
             Dim badValue As Object = e.ProposedValue  
             e.ProposedValue = "Bad Data"  
             e.Row.RowError = "The Product column contians an error"  
             e.Row.SetColumnError(e.Column, "Product cannot be " & _  
             CType(badValue, String))  
          End If  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    //Handle column changing events on the Customers table  
    private void Customers_ColumnChanging(object sender, System.Data.DataColumnChangeEventArgs e) {  
  
       //Only check for errors in the Product column  
       if (e.Column.ColumnName.Equals("Product")) {  
  
          //Do not allow "Automobile" as a product  
          if (e.ProposedValue.Equals("Automobile")) {  
             object badValue = e.ProposedValue;  
             e.ProposedValue = "Bad Data";  
             e.Row.RowError = "The Product column contains an error";  
             e.Row.SetColumnError(e.Column, "Product cannot be " + badValue);  
          }  
       }  
    }  
  
    ```  
  
2.  Connettere il gestore eventi all'evento in questione.  
  
     Inserire il codice qui di seguito nell'evento <xref:System.Windows.Forms.Form.Load> del form o nel relativo costruttore.  
  
    ```vb  
    ' Assumes the grid is bound to a dataset called customersDataSet1  
    ' with a table called Customers.  
    ' Put this code in the form's Load event or its constructor.  
    AddHandler customersDataSet1.Tables("Customers").ColumnChanging, AddressOf Customers_ColumnChanging  
  
    ```  
  
    ```csharp  
    // Assumes the grid is bound to a dataset called customersDataSet1  
    // with a table called Customers.  
    // Put this code in the form's Load event or its constructor.  
    customersDataSet1.Tables["Customers"].ColumnChanging += new DataColumnChangeEventHandler(this.Customers_ColumnChanging);  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGrid>   
 <xref:System.Data.DataTable.ColumnChanging>   
 <xref:System.Data.DataRow.SetColumnError%2A>   
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)