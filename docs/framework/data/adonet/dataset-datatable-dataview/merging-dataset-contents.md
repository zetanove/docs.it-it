---
title: "Unione del contenuto di un DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5e9309a-3ebb-4a9c-9d78-21c4e2bafc5b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Unione del contenuto di un DataSet
È possibile usare il metodo <xref:System.Data.DataSet.Merge%2A> per unire il contenuto di un oggetto <xref:System.Data.DataSet>, <xref:System.Data.DataTable> o una matrice <xref:System.Data.DataRow> in un `DataSet` esistente.  L'unione di nuovi dati in un `DataSet` esistente è influenzata da diversi fattori e opzioni.  
  
## Chiavi primarie  
 Se la tabella che riceve i nuovi dati e lo schema da un'operazione di unione dispone di una chiave primaria, le nuove righe dei dati in arrivo verranno associate alle righe esistenti i cui valori di chiave primaria <xref:System.Data.DataRowVersion> corrispondono a quelli presenti nei dati in arrivo.  Se le colonne dello schema in arrivo corrispondono alle colonne dello schema esistente, i dati delle righe esistenti verranno modificati.  Le colonne che non corrispondono allo schema esistente verranno ignorate o aggiunte in base al parametro <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A>.  Le nuove righe contenenti valori di chiave primaria non corrispondenti a nessuna delle righe esistenti verranno aggiunte alla tabella esistente.  
  
 Se alle righe in arrivo o esistenti è associato uno stato di riga <xref:System.Data.DataRowState>, i relativi valori di chiave primaria verranno associati tramite il valore di chiave primaria <xref:System.Data.DataRowVersion> della riga `Added`, poiché non è presente nessuna versione di riga `Original`.  
  
 Se in una tabella in arrivo e una tabella esistente è contenuta una colonna con lo stesso nome ma con tipi di dati diversi, verranno generati un'eccezione e l'evento <xref:System.Data.DataSet.MergeFailed> del `DataSet`.  Se nella tabella in arrivo e nella tabella esistente sono state definite chiavi, ma le chiavi primarie sono relative a colonne diverse, verranno generati un'eccezione e l'evento `MergeFailed` del `DataSet`.  
  
 Se la tabella che riceve i nuovi dati da un'operazione di unione non dispone di alcuna chiave primaria, non sarà possibile associare i nuovi valori relativi ai dati in arrivo alle righe esistenti della tabella. Tali valori verranno quindi aggiunti alla tabella esistente.  
  
## Nomi di tabella e spazi dei nomi  
 Se necessario, agli oggetti <xref:System.Data.DataTable> è possibile assegnare un valore della proprietà <xref:System.Data.DataTable.Namespace%2A>.  Quando vengono assegnati i valori di <xref:System.Data.DataTable.Namespace%2A>, un oggetto <xref:System.Data.DataSet> può contenere più oggetti <xref:System.Data.DataTable> con lo stesso valore <xref:System.Data.DataTable.TableName%2A>.  Durante le operazioni di unione vengono usati <xref:System.Data.DataTable.TableName%2A> e <xref:System.Data.DataTable.Namespace%2A> per identificare la destinazione di un'unione.  Se è stato assegnato <xref:System.Data.DataTable.Namespace%2A>, per identificare la destinazione di un'unione viene usato <xref:System.Data.DataTable.TableName%2A>.  
  
> [!NOTE]
>  Questo comportamento è stato modificato in .NET Framework versione 2.0.  Nella versione 1.1 gli spazi dei nomi sono supportati ma vengono ignorati durante le operazioni di unione.  Per questo motivo il comportamento di un oggetto <xref:System.Data.DataSet> che usa i valori della proprietà <xref:System.Data.DataTable.Namespace%2A> a seconda della versione di .NET Framework in esecuzione.  Ad esempio, si supponga di disporre di due `DataSets` contenenti `DataTables` con lo stesso valore della proprietà <xref:System.Data.DataTable.TableName%2A> ma valori diversi della proprietà <xref:System.Data.DataTable.Namespace%2A>.  Nella versione 1.1 di .NET Framework, i diversi nomi di <xref:System.Data.DataTable.Namespace%2A> verranno ignorati durante l'unione dei due oggetti <xref:System.Data.DataSet>.  A partire dalla versione 2.0, invece, in seguito all'unione vengono creati due nuovi oggetti `DataTables` nell'oggetto <xref:System.Data.DataSet> di destinazione.  I `DataTables` originali non verranno interessati dall'unione.  
  
## PreserveChanges  
 Quando si passa una matrice `DataSet`, `DataTable` o `DataRow` al metodo `Merge`, è possibile includere parametri facoltativi che consentano di specificare se mantenere o meno le modifiche nel `DataSet` esistente e come gestire i nuovi elementi dello schema individuati nei dati in arrivo.  Il primo di tali parametri successivi ai dati in arrivo è un flag booleano, <xref:System.Data.LoadOption>, che consente di specificare se conservare o meno le modifiche nel `DataSet` esistente.  Se il flag `PreserveChanges` è impostato su `true`, i valori esistenti nella versione di riga `Current` della riga esistente non verranno sovrascritti dai valori in arrivo.  Se il flag `PreserveChanges` è impostato su `false`, i valori esistenti nella versione di riga `Current` della riga esistente verranno sovrascritti dai valori in arrivo.  Se non è specificato, il flag `PreserveChanges` viene impostato su `false` per impostazione predefinita.  Per altre informazioni sulle versioni delle righe, vedere [Stati delle righe e versioni delle righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md).  
  
 Se `PreserveChanges` è `true`, i dati della riga esistente verranno mantenuti nella versione di riga <xref:System.Data.DataRowVersion> della riga esistente, mentre i dati della versione di riga <xref:System.Data.DataRowVersion> della riga esistente verranno sovrascritti dai dati della versione di riga `Original` della riga in arrivo.  La proprietà <xref:System.Data.DataRow.RowState%2A> della riga esistente è impostata su <xref:System.Data.DataRowState>.  Vengono applicate le seguenti eccezioni:  
  
-   Se il valore di `RowState` per la riga esistente è `Deleted`, il valore di `RowState` rimane `Deleted` e non viene impostato su `Modified`.  In questo caso i dati contenuti nella riga in arrivo verranno archiviati comunque nella versione di riga `Original` della riga esistente, sovrascrivendo la versione di riga `Original` della riga esistente \(a meno che il valore di `RowState` per la riga in arrivo non sia `Added`\).  
  
-   Se il valore di `RowState` per la riga in arrivo è `Added`, i dati della versione di riga `Original` della riga esistente non verranno sovrascritti con i dati della riga in arrivo, poiché a tale riga non è associata nessuna versione di riga `Original`.  
  
 Se `PreserveChanges` è `false`, le versioni di riga `Current` e `Original` della riga esistente verranno sovrascritte con i dati della riga in arrivo e il valore di `RowState` della riga esistente verrà impostato sul valore di `RowState` della riga in arrivo.  Vengono applicate le seguenti eccezioni:  
  
-   Se il valore di `RowState` per la riga in arrivo è `Unchanged` e il valore di `RowState` per la riga esistente è `Modified`, `Deleted`o `Added`, il valore di `RowState` per la riga esistente verrà impostato su `Modified`.  
  
-   Se il valore di `RowState` per la riga in arrivo è `Added` e il valore di `RowState` per la riga esistente è `Unchanged`, `Modified` o `Deleted`, il valore di `RowState` per la riga esistente verrà impostato su `Modified`.  I dati contenuti nella versione di riga `Original` della riga esistente non verranno inoltre sovrascritti con i dati della riga in arrivo, poiché a tale riga non è associata nessuna versione di riga `Original`.  
  
## MissingSchemaAction  
 È possibile usare il parametro facoltativo <xref:System.Data.MissingSchemaAction> del metodo `Merge` per specificare in che modo `Merge` gestirà gli elementi dello schema nei dati in arrivo che non fanno parte del `DataSet` esistente.  
  
 Nella tabella seguente vengono descritte le opzioni per `MissingSchemaAction`.  
  
|Opzione MissingSchemaAction|Descrizione|  
|---------------------------------|-----------------|  
|<xref:System.Data.MissingSchemaAction>|Aggiunge le nuove informazioni dello schema al `DataSet` e popola le nuove colonne usando i valori in arrivo.  Questa è l'impostazione predefinita.|  
|<xref:System.Data.MissingSchemaAction>|Aggiunge le nuove informazioni sullo schema e sulla chiave primaria al `DataSet` e popola le nuove colonne usando i valori in arrivo.|  
|<xref:System.Data.MissingSchemaAction>|Genera un'eccezione nel caso in cui vengano rilevate delle informazioni relative allo schema non associate correttamente.|  
|<xref:System.Data.MissingSchemaAction>|Ignora le nuove informazioni relative allo schema.|  
  
## Vincoli  
 Se si usa il metodo `Merge`, la verifica dei vincoli viene eseguita solo quando tutti i nuovi dati sono stati aggiunti al `DataSet` esistente.  Una volta aggiunti i dati, i vincoli vengono applicati ai valori correnti del `DataSet`.  È necessario assicurarsi che il codice sia in grado di gestire eventuali eccezioni generate a causa di violazioni dei vincoli.  
  
 Si consideri il caso in cui una riga esistente di un `DataSet` è una riga `Unchanged` con un valore di chiave primaria di 1.  Durante un'operazione di unione con una riga in arrivo `Modified` in cui il valore di chiave primaria `Original` è 2 il valore di chiave primaria `Current` è 1, la riga esistente e la riga in arrivo non vengono considerate corrispondenti perché i valori della chiave primaria di `Original` sono diversi.  Tuttavia, una volta completata l'unione e verificati i vincoli, verrà generata un'eccezione, poiché i valori di chiave primaria `Current` violano il vincolo univoco per la colonna di chiave primaria.  
  
> [!NOTE]
>  Quando si inseriscono righe in una tabella di database contenente una colonna a incremento automatico ad esempio una colonna Identity, è possibile che il valore della colonna Identity restituito dall'inserimento non corrisponda al valore di `DataSet`, pertanto le righe restituite verranno aggiunte anziché unite.  Per altre informazioni, vedere [Recupero dei valori di identità o del contatore](../../../../../docs/framework/data/adonet/retrieving-identity-or-autonumber-values.md).  
  
 Nell'esempio di codice seguente viene eseguito il merge di due oggetti `DataSet` con schemi diversi in un unico `DataSet` contenente una combinazione degli schemi dei due oggetti `DataSet` in arrivo.  
  
 [!code-csharp[DataWorks DataSet.Merge#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.Merge/CS/source.cs#1)]
 [!code-vb[DataWorks DataSet.Merge#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.Merge/VB/source.vb#1)]  
  
 Nell'esempio di codice seguente viene selezionato un `DataSet` esistente con aggiornamenti e tali aggiornamenti vengono passati a un `DataAdapter` per l'elaborazione nell'origine dati.  I risultati vengono quindi uniti nel `DataSet` originale.  Dopo aver rifiutato le modifiche che causavano un errore, le modifiche unite vengono confermate tramite `AcceptChanges`.  
  
 [!code-csharp[DataWorks DataSet.MergeAcceptChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/CS/source.cs#1)]
 [!code-vb[DataWorks DataSet.MergeAcceptChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/VB/source.vb#1)]  
  
 [!code-csharp[DataWorks DataSet.MergeAcceptChanges#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/CS/source.cs#2)]
 [!code-vb[DataWorks DataSet.MergeAcceptChanges#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/VB/source.vb#2)]  
  
## Vedere anche  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Stati delle righe e versioni delle righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)   
 [DataAdapter e DataReader](../../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Recupero dei valori di identità o del contatore](../../../../../docs/framework/data/adonet/retrieving-identity-or-autonumber-values.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)