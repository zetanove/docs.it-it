---
title: "Procedura: eliminare o nascondere colonne nel controllo DataGrid Windows Form | Microsoft Docs"
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
  - "colonne [Windows Form], eliminazione nelle griglie dei dati"
  - "colonne [Windows Form], nascondere"
  - "griglie dei dati, eliminazione di colonne"
  - "griglie dei dati, nascondere colonne"
  - "DataGrid (controllo) [Windows Form], eliminazione di colonne"
  - "DataGrid (controllo) [Windows Form], nascondere colonne"
ms.assetid: bcd0dd96-6687-4c48-b0e1-d5287b93ac91
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: eliminare o nascondere colonne nel controllo DataGrid Windows Form
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 È possibile eliminare o nascondere le colonne nel controllo <xref:System.Windows.Forms.DataGrid> Windows Forms a livello di codice utilizzando le proprietà e i metodi degli oggetti <xref:System.Windows.Forms.GridColumnStylesCollection> e <xref:System.Windows.Forms.DataGridColumnStyle>, membri della classe <xref:System.Windows.Forms.DataGridTableStyle>.  
  
 Le colonne eliminate o nascoste sono ancora presenti nell'origine dati alla quale è associata la griglia ed è ancora possibile accedervi a livello di codice.  Non sono tuttavia più visibili nel controllo DataGrid.  
  
> [!NOTE]
>  Se l'applicazione non consente di accedere ad alcune colonne di dati e non si desidera visualizzarle nel controllo DataGrid, potrebbe non essere necessario includerle nella parte iniziale dell'origine dati.  
  
### Per eliminare una colonna da DataGrid a livello di codice  
  
1.  Nella sezione Dichiarazioni del form dichiarare una nuova istanza della classe <xref:System.Windows.Forms.DataGridTableStyle>.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A?displayProperty=fullName> sulla tabella dell'origine dati alla quale applicare lo stile.  Nell'esempio seguente viene utilizzata la proprietà <xref:System.Windows.Forms.DataGrid.DataMember%2A?displayProperty=fullName> e si presuppone sia già impostata.  
  
3.  Aggiungere il nuovo oggetto <xref:System.Windows.Forms.DataGridTableStyle> alla raccolta degli stili di tabella della griglia.  
  
4.  Chiamare il metodo <xref:System.Windows.Forms.GridColumnStylesCollection.RemoveAt%2A> della raccolta <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> di <xref:System.Windows.Forms.DataGrid> specificando l'indice della colonna da eliminare.  
  
    ```vb  
    ' Declare a new DataGridTableStyle in the  
    ' declarations area of your form.  
    Dim ts As DataGridTableStyle = New DataGridTableStyle()  
  
    Sub DeleteColumn()  
       ' Set the DataGridTableStyle.MappingName property  
       ' to the table in the data source to map to.  
       ts.MappingName = DataGrid1.DataMember  
  
       ' Add it to the datagrid's TableStyles collection  
       DataGrid1.TableStyles.Add(ts)  
  
       ' Delete the first column (index 0)  
       DataGrid1.TableStyles(0).GridColumnStyles.RemoveAt(0)  
    End Sub  
  
    ```  
  
    ```csharp  
    // Declare a new DataGridTableStyle in the  
    // declarations area of your form.  
    DataGridTableStyle ts = new DataGridTableStyle();  
  
    private void deleteColumn()  
    {  
       // Set the DataGridTableStyle.MappingName property  
       // to the table in the data source to map to.  
       ts.MappingName = dataGrid1.DataMember;  
  
       // Add it to the datagrid's TableStyles collection  
       dataGrid1.TableStyles.Add(ts);  
  
       // Delete the first column (index 0)  
       dataGrid1.TableStyles[0].GridColumnStyles.RemoveAt(0);  
    }  
    ```  
  
### Per nascondere una colonna in DataGrid a livello di codice  
  
1.  Nella sezione Dichiarazioni del form dichiarare una nuova istanza della classe <xref:System.Windows.Forms.DataGridTableStyle>.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> del controllo <xref:System.Windows.Forms.DataGridTableStyle> sulla tabella dell'origine dati alla quale applicare lo stile.  Nell'esempio di codice seguente viene utilizzata la proprietà <xref:System.Windows.Forms.DataGrid.DataMember%2A?displayProperty=fullName> e si presuppone sia già impostata.  
  
3.  Aggiungere il nuovo oggetto <xref:System.Windows.Forms.DataGridTableStyle> alla raccolta degli stili di tabella della griglia.  
  
4.  Per nascondere la colonna, impostarne su 0 la proprietà `Width` , specificando l'indice della colonna da nascondere.  
  
    ```vb  
    ' Declare a new DataGridTableStyle in the  
    ' declarations area of your form.  
    Dim ts As DataGridTableStyle = New DataGridTableStyle()  
  
    Sub HideColumn()  
       ' Set the DataGridTableStyle.MappingName property  
       ' to the table in the data source to map to.  
       ts.MappingName = DataGrid1.DataMember  
  
       ' Add it to the datagrid's TableStyles collection  
       DataGrid1.TableStyles.Add(ts)  
  
       ' Hide the first column (index 0)  
       DataGrid1.TableStyles(0).GridColumnStyles(0).Width = 0  
    End Sub  
  
    ```  
  
    ```csharp  
    // Declare a new DataGridTableStyle in the  
    // declarations area of your form.  
    DataGridTableStyle ts = new DataGridTableStyle();  
  
    private void hideColumn()  
    {  
       // Set the DataGridTableStyle.MappingName property  
       // to the table in the data source to map to.  
       ts.MappingName = dataGrid1.DataMember;  
  
       // Add it to the datagrid's TableStyles collection  
       dataGrid1.TableStyles.Add(ts);  
  
       // Hide the first column (index 0)  
       dataGrid1.TableStyles[0].GridColumnStyles[0].Width = 0;  
    }  
    ```  
  
## Vedere anche  
 [Procedura: modificare i dati visualizzati in fase di esecuzione nel controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/change-displayed-data-at-run-time-wf-datagrid-control.md)   
 [Procedura: aggiungere tabelle e colonne al controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)