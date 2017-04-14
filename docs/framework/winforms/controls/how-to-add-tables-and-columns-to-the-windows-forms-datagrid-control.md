---
title: "Procedura: aggiungere tabelle e colonne al controllo DataGrid Windows Form | Microsoft Docs"
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
  - "colonne [Windows Form], aggiunta al controllo DataGrid"
  - "DataGrid (controllo) [Windows Form], aggiunta di tabelle e colonne"
  - "tabelle [Windows Form], aggiunta al controllo DataGrid"
ms.assetid: 2fe661b9-aa06-49b9-a314-a0d3cbfdcb4d
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: aggiungere tabelle e colonne al controllo DataGrid Windows Form
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 È possibile visualizzare i dati del controllo <xref:System.Windows.Forms.DataGrid> Windows Form in tabelle e colonne creando oggetti **DataGridTableStyle** e aggiungendoli all'oggetto **GridTableStylesCollection**, a cui si accede mediante la proprietà **TableStyles** del controllo <xref:System.Windows.Forms.DataGrid>.  Ogni stile di tabella visualizza il contenuto di qualsiasi tabella di dati specificata nella proprietà **MappingName** dell'oggetto **DataGridTableStyle**.  Per impostazione predefinita, uno stile di tabella per il quale non sono stati specificati stili di colonna visualizzerà tutte le colonne presenti nella tabella di dati corrispondente.  È possibile limitare il numero di colonne della tabella da visualizzare aggiungendo oggetti **DataGridColumnStyle** all'oggetto **GridColumnStylesCollection**, a cui si accede mediante la proprietà **GridColumnStyles** di ciascun oggetto **DataGridTableStyle**.  
  
### Per aggiungere una tabella e una colonna a un controllo DataGrid a livello di codice  
  
1.  Per visualizzare i dati nella tabella è innanzitutto necessario associare il controllo <xref:System.Windows.Forms.DataGrid> a un dataset.  Per ulteriori informazioni, vedere [Procedura: associare il controllo DataGrid Windows Form a un'origine dati](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md).  
  
    > [!CAUTION]
    >  Quando si specificano gli stili di colonna a livello di codice, prima di aggiungere oggetti **DataGridTableStyle** all'oggetto **GridTableStylesCollection** è necessario creare sempre oggetti **DataGridColumnStyle** e aggiungerli all'oggetto **GridColumnStylesCollection**.  Quando si aggiunge alla raccolta un oggetto **DataGridTableStyle** vuoto, gli oggetti **DataGridColumnStyle** vengono generati automaticamente.  Di conseguenza, se si tenta di aggiungere all'oggetto **GridColumnStylesCollection** nuovi oggetti **DataGridColumnStyle** con valori di **MappingName** duplicati, verrà generata un'eccezione.  
  
2.  Dichiarare un nuovo stile di tabella e impostarne il nome di associazione.  
  
    ```vb  
    Dim ts1 As New DataGridTableStyle()  
    ts1.MappingName = "Customers"  
  
    ```  
  
    ```csharp  
    DataGridTableStyle ts1 = new DataGridTableStyle();  
    ts1.MappingName = "Customers";  
  
    ```  
  
    ```cpp  
    DataGridTableStyle* ts1 = new DataGridTableStyle();  
    ts1->MappingName = S"Customers";  
    ```  
  
3.  Dichiarare un nuovo stile di colonna e impostarne il nome di associazione e altre proprietà.  
  
    ```vb  
    Dim myDataCol As New DataGridBoolColumn()  
    myDataCol.HeaderText = "My New Column"  
    myDataCol.MappingName = "Current"  
  
    ```  
  
    ```csharp  
    DataGridBoolColumn myDataCol = new DataGridBoolColumn();  
    myDataCol.HeaderText = "My New Column";  
    myDataCol.MappingName = "Current";  
  
    ```  
  
    ```cpp  
    DataGridBoolColumn^ myDataCol = gcnew DataGridBoolColumn();  
    myDataCol->HeaderText = "My New Column";  
    myDataCol->MappingName = "Current";  
    ```  
  
4.  Chiamare il metodo **Add** dell'oggetto **GridColumnStylesCollection** per aggiungere la colonna allo stile di tabella.  
  
    ```vb  
    ts1.GridColumnStyles.Add(myDataCol)  
  
    ```  
  
    ```csharp  
    ts1.GridColumnStyles.Add(myDataCol);  
  
    ```  
  
    ```cpp  
    ts1->GridColumnStyles->Add(myDataCol);  
    ```  
  
5.  Chiamare il metodo **Add** dell'oggetto **GridTableStylesCollection** per aggiungere lo stile di tabella alla griglia di dati.  
  
    ```vb  
    DataGrid1.TableStyles.Add(ts1)  
  
    ```  
  
    ```csharp  
    dataGrid1.TableStyles.Add(ts1);  
  
    ```  
  
    ```cpp  
    dataGrid1->TableStyles->Add(ts1);  
    ```  
  
## Vedere anche  
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Procedura: eliminare o nascondere colonne nel controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)