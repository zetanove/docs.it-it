---
title: "Gestione degli eventi di DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 62f404a5-13ea-4b93-a29f-55b74a16c9d3
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Gestione degli eventi di DataTable
Nell'oggetto <xref:System.Data.DataTable> sono disponibili diversi eventi che possono essere elaborati da un'applicazione.  Nella tabella seguente vengono descritti gli eventi di `DataTable`.  
  
|Evento|Descrizione|  
|------------|-----------------|  
|<xref:System.Data.DataTable.Initialized>|Viene generato dopo la chiamata al metodo <xref:System.Data.DataTable.EndInit%2A> di `DataTable`.  Questo evento è progettato principalmente per supportare gli scenari in fase di progettazione.|  
|<xref:System.Data.DataTable.ColumnChanged>|Viene generato dopo la modifica di un valore in <xref:System.Data.DataColumn>.|  
|<xref:System.Data.DataTable.ColumnChanging>|Viene generato quando un valore è stato inviato per una `DataColumn`.|  
|<xref:System.Data.DataTable.RowChanged>|Viene generato dopo la modifica di un valore `DataColumn` o di <xref:System.Data.DataRow.RowState%2A> di <xref:System.Data.DataRow> nella `DataTable`.|  
|<xref:System.Data.DataTable.RowChanging>|Viene generato quando è stata inviata una modifica per un valore `DataColumn` o per `RowState` di `DataRow` nella `DataTable`.|  
|<xref:System.Data.DataTable.RowDeleted>|Viene generato dopo che una `DataRow` nella `DataTable` è stata contrassegnata come `Deleted`.|  
|<xref:System.Data.DataTable.RowDeleting>|Viene generato prima che una `DataRow` nella `DataTable` venga contrassegnata come `Deleted`.|  
|<xref:System.Data.DataTable.TableCleared>|Viene generato dopo che una chiamata al metodo <xref:System.Data.DataTable.Clear%2A> di `DataTable` ha cancellato correttamente ogni `DataRow`.|  
|<xref:System.Data.DataTable.TableClearing>|Viene generato dopo una chiamata al metodo `Clear` ma prima dell'inizio dell'operazione `Clear`.|  
|<xref:System.Data.DataTable.TableNewRow>|Viene generato dopo la creazione di una nuova `DataRow` tramite una chiamata al metodo `NewRow` della `DataTable`.|  
|<xref:System.ComponentModel.MarshalByValueComponent.Disposed>|Viene generato quando `DataTable` è `Disposed`.  La proprietà viene ereditata da <xref:System.ComponentModel.MarshalByValueComponent>.|  
  
> [!NOTE]
>  La maggior parte delle operazioni che aggiungono o eliminano righe non generano gli eventi `ColumnChanged` e `ColumnChanging`.  Tuttavia, il metodo `ReadXml` genera gli eventi `ColumnChanged` e `ColumnChanging`, a meno che `XmlReadMode` non sia impostato su `DiffGram` o su `Auto` quando il documento XML da leggere è un `DiffGram`.  
  
> [!WARNING]
>  I dati possono venire danneggiati se vengono modificati in un oggetto `DataSet` da cui viene generato l'evento `RowChanged`.  In caso di danneggiamento dei dati, non viene generata alcuna eccezione.  
  
## Eventi correlati aggiuntivi  
 La proprietà <xref:System.Data.DataTable.Constraints%2A> contiene un'istanza di <xref:System.Data.ConstraintCollection>.  La classe <xref:System.Data.ConstraintCollection> espone un evento <xref:System.Data.ConstraintCollection.CollectionChanged>.  Questo evento viene attivato quando un vincolo viene aggiunto, modificato o rimosso da `ConstraintCollection`.  
  
 La proprietà <xref:System.Data.DataTable.Columns%2A> contiene un'istanza di <xref:System.Data.DataColumnCollection>.  La classe `DataColumnCollection` espone un evento <xref:System.Data.DataColumnCollection.CollectionChanged>.  Questo evento viene attivato quando una `DataColumn` viene aggiunta, modificata o rimossa da `DataColumnCollection`.  Le modifiche che causano l'attivazione dell'evento includono le modifiche al nome, tipo, espressione o posizione ordinale di una colonna.  
  
 La proprietà <xref:System.Data.DataSet.Tables%2A> di <xref:System.Data.DataSet> contiene un'istanza di <xref:System.Data.DataTableCollection>.  La classe `DataTableCollection` espone sia un evento `CollectionChanged` sia un evento `CollectionChanging`.  Questi eventi vengono attivati quando una `DataTable` viene aggiunta, modificata o rimossa dal `DataSet`.  
  
 Le modifiche a `DataRows` possono attivare anche eventi per un oggetto <xref:System.Data.DataView> associato.  La classe `DataView` espone un evento <xref:System.Data.DataView.ListChanged> che viene attivato quando viene modificato un valore `DataColumn` oppure la composizione o l'ordine della visualizzazione.  La classe <xref:System.Data.DataRowView> espone un evento <xref:System.Data.DataRowView.PropertyChanged> che viene attivato quando viene modificato valore `DataColumn` associato.  
  
## Sequenza delle operazioni  
 Di seguito è riportata la sequenza delle operazioni che si verificano quando una `DataRow` viene aggiunta, modificata o eliminata:  
  
1.  Creare il record proposto e applicare eventuali modifiche.  
  
2.  Verificare i vincoli per le colonne non espressioni.  
  
3.  Generare gli eventi `RowChanging` o `RowDeleting` come applicabile.  
  
4.  Impostare il record proposto come record corrente.  
  
5.  Aggiornare gli eventuali indici associati.  
  
6.  Generare gli eventi `ListChanged` per gli oggetti `DataView` associati e gli eventi `PropertyChanged` per gli oggetti `DataRowView` associati.  
  
7.  Valutare tutte le colonne espressioni, ma rimandare la verifica della presenza di vincoli su queste colonne.  
  
8.  Generare gli eventi `ListChanged` per gli oggetti `DataView` associati e gli eventi `PropertyChanged` per gli oggetti `DataRowView` associati interessati dalle valutazioni delle colonne espressioni.  
  
9. Generare gli eventi `RowChanged` o `RowDeleted` come applicabile.  
  
10. Verificare i vincoli per le colonne espressioni.  
  
> [!NOTE]
>  Le modifiche alle colonne espressioni non generano mai eventi `DataTable`,  ma generano solo eventi `DataView` e `DataRowView`,  Le colonne espressioni possono avere dipendenze su molte altre colonne e possono essere valutate più volte durante una singola operazione `DataRow`.  Ogni valutazione di espressione genera eventi e una singola operazione `DataRow` può generare più eventi `ListChanged` e `PropertyChanged` quando sono interessate colonne espressioni, magari con più eventi per la stessa colonna espressioni.  
  
> [!WARNING]
>  Non generare un'eccezione <xref:System.NullReferenceException> all'interno del gestore eventi `RowChanged`.  Se viene generata un'eccezione <xref:System.NullReferenceException> all'interno dell'evento `RowChanged` di un oggetto `DataTable`, quest'ultimo sarà danneggiato.  
  
### Esempio  
 Nell'esempio seguente viene illustrato come creare gestori per gli eventi `RowChanged`, `RowChanging`, `RowDeleted`, `RowDeleting`, `ColumnChanged`, `ColumnChanging`, `TableNewRow`, `TableCleared` e `TableClearing`.  Ogni gestore evento visualizza l'output nella finestra della console quando viene attivato.  
  
 [!code-csharp[DataWorks DataTable.Events#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataTable.Events/CS/source.cs#1)]
 [!code-vb[DataWorks DataTable.Events#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataTable.Events/VB/source.vb#1)]  
  
## Vedere anche  
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Gestione degli eventi di DataAdapter](../../../../../docs/framework/data/adonet/handling-dataadapter-events.md)   
 [Gestione di eventi dataset](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-dataset-events.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)