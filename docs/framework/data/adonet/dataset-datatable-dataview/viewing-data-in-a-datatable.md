---
title: "Visualizzazione dei dati in DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d26e0fb-f6e0-4afa-9a9c-b8d55b8f20dc
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Visualizzazione dei dati in DataTable
Le raccolte **Rows** e **Columns** della **DataTable** consentono di accedere al contenuto di un tipo <xref:System.Data.DataTable>.  È inoltre possibile usare il metodo <xref:System.Data.DataTable.Select%2A> per restituire subset dei dati in una **DataTable** in base a determinati criteri, inclusi i criteri di ricerca, l'ordinamento e lo stato della riga.  È inoltre possibile usare il metodo <xref:System.Data.DataRowCollection.Find%2A> di **DataRowCollection** quando si cerca una particolare riga mediante un valore di chiave primaria.  
  
 Il metodo **Select** dell'oggetto **DataTable** restituisce un set di oggetti <xref:System.Data.DataRow> che corrispondono ai criteri specificati.  **Select** accetta gli argomenti facoltativi di un'espressione di filtro, di un'espressione di ordinamento e di **DataViewRowState**.  L'espressione di filtro consente di identificare le righe da restituire in base ai valori **DataColumn**, quali `LastName = 'Smith'`.  Per l'espressione di ordinamento vengono usate le convenzioni SQL standard per l'ordinamento di colonne, ad esempio `LastName ASC, FirstName ASC`.  Per le regole sulla scrittura di espressioni, vedere la proprietà <xref:System.Data.DataColumn.Expression%2A> della classe **DataColumn**.  
  
> [!TIP]
>  Se si eseguono più chiamate al metodo **Select** di un oggetto **DataTable**, è possibile migliorare le prestazioni creando un tipo <xref:System.Data.DataView> per l'oggetto **DataTable**.  Tramite la creazione di **DataView** vengono indicizzate le righe della tabella.  L'indice creato verrà usato dal metodo **Select**, riducendo in modo significativo il tempo necessario per generare il risultato della query.  Per informazioni sulla creazione di un **DataView** per una **DataTable**, vedere [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md).  
  
 Il metodo **Select** determina la versione delle righe da visualizzare o modificare in base a un tipo <xref:System.Data.DataViewRowState>.  Nella tabella seguente vengono descritti i valori di enumerazione possibili di **DataViewRowState**.  
  
|Valore di DataViewRowState|Descrizione|  
|--------------------------------|-----------------|  
|**CurrentRows**|Righe correnti, incluse le righe non modificate, aggiunte e modificate.|  
|**Eliminato**|Riga eliminata.|  
|**ModifiedCurrent**|Una versione corrente, ovvero una versione modificata dei dati originali.  Vedere **ModifiedOriginal**.|  
|**ModifiedOriginal**|La versione originale di tutte le righe modificate.  La versione corrente è disponibile tramite **ModifiedCurrent**.|  
|**Added**|Nuova riga.|  
|**None**|Nessuno.|  
|**OriginalRows**|Righe originali, tra cui righe non modificate ed eliminate.|  
|**Unchanged**|Riga non modificata.|  
  
 Nell'esempio seguente viene applicato un filtro all'oggetto **DataSet** in modo da poter usare le righe il cui valore di **DataViewRowState** è impostato su **CurrentRows**.  
  
```vb  
Dim column As DataColumn  
Dim row As DataRow  
  
Dim currentRows() As DataRow = _  
    workTable.Select(Nothing, Nothing, DataViewRowState.CurrentRows)  
  
If (currentRows.Length < 1 ) Then  
  Console.WriteLine("No Current Rows Found")  
Else  
  For Each column in workTable.Columns  
    Console.Write(vbTab & column.ColumnName)  
  Next  
  
  Console.WriteLine(vbTab & "RowState")  
  
  For Each row In currentRows  
    For Each column In workTable.Columns  
      Console.Write(vbTab & row(column).ToString())  
    Next  
  
    Dim rowState As String = _  
        System.Enum.GetName(row.RowState.GetType(), row.RowState)  
    Console.WriteLine(vbTab & rowState)  
  Next  
End If  
  
```  
  
```csharp  
DataRow[] currentRows = workTable.Select(  
    null, null, DataViewRowState.CurrentRows);  
  
if (currentRows.Length < 1 )  
  Console.WriteLine("No Current Rows Found");  
else  
{  
  foreach (DataColumn column in workTable.Columns)  
    Console.Write("\t{0}", column.ColumnName);  
  
  Console.WriteLine("\tRowState");  
  
  foreach (DataRow row in currentRows)  
  {  
    foreach (DataColumn column in workTable.Columns)  
      Console.Write("\t{0}", row[column]);  
  
    Console.WriteLine("\t" + row.RowState);  
  }  
}  
```  
  
 È possibile usare il metodo **Select** per restituire righe con diversi valori **RowState** o valori di campo.  Nell'esempio seguente vengono restituite una matrice **DataRow** contenente riferimenti a tutte le righe che sono state eliminate e una matrice **DataRow** contenente riferimenti a tutte le righe, ordinate per **CustLName**, in cui il valore della colonna **CustID** è superiore a 5.  Per informazioni su come visualizzare le informazioni nella riga **Deleted**, vedere [Stati delle righe e versioni delle righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md).  
  
```vb  
' Retrieve all deleted rows.  
Dim deletedRows() As DataRow = workTable.Select(Nothing, Nothing, DataViewRowState.Deleted)  
  
' Retrieve rows where CustID > 5, and order by CustLName.  
Dim custRows() As DataRow = workTable.Select( _  
    "CustID > 5", "CustLName ASC")  
  
```  
  
```csharp  
// Retrieve all deleted rows.  
DataRow[] deletedRows = workTable.Select(  
    null, null, DataViewRowState.Deleted);  
  
// Retrieve rows where CustID > 5, and order by CustLName.  
DataRow[] custRows = workTable.Select("CustID > 5", "CustLName ASC");  
```  
  
## Vedere anche  
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataSet>   
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataViewRowState>   
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Stati delle righe e versioni delle righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)