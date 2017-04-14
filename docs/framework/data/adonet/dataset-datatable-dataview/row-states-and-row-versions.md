---
title: "Stati delle righe e versioni delle righe | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e6642c9-bfc6-425c-b3a7-e4912ffa6c1f
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Stati delle righe e versioni delle righe
In ADO.NET le righe delle tabelle vengono gestite tramite gli stati e le versioni delle righe.  Lo stato di una riga indica lo stato corrente di una particolare riga. Le versioni delle righe consentono di mantenere i valori archiviati in una riga durante le modifiche. Vengono conservati anche i valori correnti, originali e predefiniti.  Ad esempio, dopo aver apportato una modifica in una colonna di una riga, lo stato della riga sarà impostato su `Modified` e saranno disponibili due versioni, ovvero `Current`, che contiene i valori correnti della riga, e `Original`, che contiene i valori della riga prima della modifica della colonna.  
  
 A ogni oggetto <xref:System.Data.DataRow> è assegnata una proprietà <xref:System.Data.DataRow.RowState%2A>, che è possibile esaminare per determinare lo stato corrente della riga.  Nella tabella seguente viene fornita una breve descrizione di ogni valore dell'enumerazione `RowState`.  
  
|Valore di RowState|Descrizione|  
|------------------------|-----------------|  
|<xref:System.Data.DataRowState>|Non è stata apportata alcuna modifica rispetto all'ultima chiamata a `AcceptChanges` o alla creazione della riga da parte di `DataAdapter.Fill`.|  
|<xref:System.Data.DataRowState>|La riga è stata aggiunta alla tabella, ma `AcceptChanges` non è stato chiamato.|  
|<xref:System.Data.DataRowState>|Alcuni elementi della riga sono stati modificati.|  
|<xref:System.Data.DataRowState>|La riga è stata eliminata da una tabella e `AcceptChanges` non è stato chiamato.|  
|<xref:System.Data.DataRowState>|La riga non fa parte di alcun oggetto `DataRowCollection`.  Il valore di `RowState` di una riga appena creata viene impostato su `Detached`.  Dopo l'aggiunta della nuova `DataRow` al `DataRowCollection` tramite la chiamata al metodo `Add`, il valore della proprietà `RowState` viene impostato su `Added`.<br /><br /> Il valore `Detached` viene impostato anche per una riga rimossa da un `DataRowCollection` mediante il metodo `Remove` oppure mediante il metodo `Delete` seguito dal metodo `AcceptChanges`.|  
  
 Quando `AcceptChanges` viene chiamato su un oggetto <xref:System.Data.DataSet>, <xref:System.Data.DataTable> o <xref:System.Data.DataRow>, tutte le righe il cui stato corrisponde a `Deleted` vengono rimosse.  Alle righe rimanenti viene assegnato lo stato `Unchanged` e i valori con versione di riga `Original` vengono sovrascritti dai valori con versione di riga `Current`.  Quando `RejectChanges` viene chiamato, tutte le righe il cui stato corrisponde a `Added` vengono rimosse.  Alle righe rimanenti viene assegnato lo stato `Unchanged` e i valori con versione di riga `Current` vengono sovrascritti dai valori con versione di riga `Original`.  
  
 È possibile visualizzare le diverse versioni di una riga passando un parametro <xref:System.Data.DataRowVersion> contenente il riferimento alla colonna, come illustrato nell'esempio seguente.  
  
```vb  
Dim custRow As DataRow = custTable.Rows(0)  
Dim custID As String = custRow("CustomerID", DataRowVersion.Original).ToString()  
  
```  
  
```csharp  
DataRow custRow = custTable.Rows[0];  
string custID = custRow["CustomerID", DataRowVersion.Original].ToString();  
```  
  
 Nella tabella seguente viene fornita una breve descrizione di ogni valore dell'enumerazione `DataRowVersion`.  
  
|Valore di DataRowVersion|Descrizione|  
|------------------------------|-----------------|  
|<xref:System.Data.DataRowVersion>|Valori correnti della riga.  Questa versione di riga non è disponibile per le righe in cui il valore di `RowState` è `Deleted`.|  
|<xref:System.Data.DataRowVersion>|Versione di riga predefinita per una particolare riga.  La versione predefinita per una riga `Added`, `Modified` o `Unchanged` è `Current`.  La versione predefinita per una riga `Deleted` è `Original`.  La versione predefinita per una riga `Detached` è `Proposed`.|  
|<xref:System.Data.DataRowVersion>|Valori originali della riga.  Questa versione di riga non è disponibile per le righe in cui il valore di `RowState` è `Added`.|  
|<xref:System.Data.DataRowVersion>|Valori proposti per la riga.  Questa versione di riga è disponibile durante un'operazione di modifica di una riga o per una riga che non fa parte di un `DataRowCollection`.|  
  
 Per verificare se a `DataRow` è associata una particolare versione di riga, è possibile chiamare il metodo <xref:System.Data.DataRow.HasVersion%2A> e passare `DataRowVersion` come argomento.  `DataRow.HasVersion(DataRowVersion.Original)`, ad esempio, restituirà `false` per le nuove righe aggiunte prima della chiamata a `AcceptChanges`.  
  
 Nell'esempio di codice seguente vengono visualizzati i valori in tutte le righe eliminate di una tabella.  Le righe `Deleted` non dispongono di una versione della riga `Current`, pertanto è necessario passare `DataRowVersion.Original` quando si accede ai valori della colonna.  
  
```vb  
Dim catTable As DataTable = catDS.Tables("Categories")  
  
Dim delRows() As DataRow = catTable.Select(Nothing, Nothing, DataViewRowState.Deleted)  
  
Console.WriteLine("Deleted rows:" & vbCrLf)  
  
Dim catCol As DataColumn  
Dim delRow As DataRow  
  
For Each catCol In catTable.Columns  
  Console.Write(catCol.ColumnName & vbTab)  
Next  
Console.WriteLine()  
  
For Each delRow In delRows  
  For Each catCol In catTable.Columns  
    Console.Write(delRow(catCol, DataRowVersion.Original) & vbTab)  
  Next  
  Console.WriteLine()  
Next  
  
```  
  
```csharp  
DataTable catTable = catDS.Tables["Categories"];  
  
DataRow[] delRows = catTable.Select(null, null, DataViewRowState.Deleted);  
  
Console.WriteLine("Deleted rows:\n");  
  
foreach (DataColumn catCol in catTable.Columns)  
  Console.Write(catCol.ColumnName + "\t");  
Console.WriteLine();  
  
foreach (DataRow delRow in delRows)  
{  
  foreach (DataColumn catCol in catTable.Columns)  
    Console.Write(delRow[catCol, DataRowVersion.Original] + "\t");  
  Console.WriteLine();  
}  
```  
  
## Vedere anche  
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [DataAdapter e DataReader](../../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)