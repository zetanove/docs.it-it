---
title: "Procedura: modificare i dati visualizzati in fase di esecuzione nel controllo DataGrid Windows Form | Microsoft Docs"
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
  - "celle, modifica di valori di celle DataGrid"
  - "DataGrid (controllo) [Windows Form], associazione dati"
  - "DataGrid (controllo) [Windows Form], modifica dinamica in fase di esecuzione"
ms.assetid: 0c7a6d00-30de-416e-8223-0a81ddb4c1f8
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: modificare i dati visualizzati in fase di esecuzione nel controllo DataGrid Windows Form
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Una volta creato un controllo <xref:System.Windows.Forms.DataGrid> Windows Form utilizzando le funzionalità disponibili in fase di progettazione, può rivelarsi necessario modificare dinamicamente gli elementi dell'oggetto <xref:System.Data.DataSet> della griglia in fase di esecuzione.  Questa operazione può comprendere modifiche dei singoli valori della tabella oppure dell'origine dati associata al controllo <xref:System.Windows.Forms.DataGrid>.  Le modifiche ai singoli valori vengono apportate mediante l'oggetto <xref:System.Data.DataSet> e non tramite il controllo <xref:System.Windows.Forms.DataGrid>.  
  
### Per modificare i dati a livello di codice  
  
1.  Specificare la tabella desiderata dell'oggetto <xref:System.Data.DataSet> e la riga e il campo desiderati della tabella, quindi impostare la cella sul nuovo valore.  
  
    > [!NOTE]
    >  Per specificare la prima tabella di <xref:System.Data.DataSet> o la prima riga della tabella, utilizzare 0.  
  
     Nell'esempio qui di seguito viene illustrato come modificare la seconda voce della prima riga della prima tabella di un dataset facendo clic su `Button1`.  L'oggetto <xref:System.Data.DataSet> \(`ds`\) e le tabelle \(`0`  e `1`\) sono stati creati precedentemente.  
  
    ```vb  
    Protected Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       ds.tables(0).rows(0)(1) = "NewEntry"  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       ds.Tables[0].Rows[0][1]="NewEntry";  
    }  
  
    ```  
  
    ```cpp  
    private:   
       void button1_Click(System::Object^ sender, System::EventArgs^ e)  
       {  
          dataSet1->Tables[0]->Rows[0][1] = "NewEntry";  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click +=  
       gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
     In fase di esecuzione è possibile utilizzare il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> per associare il controllo <xref:System.Windows.Forms.DataGrid> a una diversa origine dati.  È ad esempio possibile disporre di più controlli dati [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)], ciascuno connesso a un diverso database.  
  
### Per modificare l'origine dati a livello di codice  
  
1.  Impostare il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> sul nome dell'origine dati e della tabella a cui si desidera effettuare l'associazione.  
  
     Nell'esempio qui seguito viene illustrato come modificare l'origine dati utilizzando il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> su un controllo dati [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] \(adoPubsAuthors\) connesso alla tabella Authors del database Pubs.  
  
    ```vb  
    Private Sub ResetSource()  
       DataGrid1.SetDataBinding(adoPubsAuthors, "Authors")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void ResetSource()  
    {  
       DataGrid1.SetDataBinding(adoPubsAuthors, "Authors");  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void ResetSource()  
       {  
          dataGrid1->SetDataBinding(adoPubsAuthors, "Authors");  
       }  
    ```  
  
## Vedere anche  
 [DataSet ADO.NET](../../../../docs/framework/data/adonet/ado-net-datasets.md)   
 [Procedura: eliminare o nascondere colonne nel controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)   
 [Procedura: aggiungere tabelle e colonne al controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)   
 [Procedura: associare il controllo DataGrid Windows Form a un'origine dati](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)