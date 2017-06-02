---
title: "Query su una singola tabella (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b74bcf8-3f87-449f-bff7-6bcb0d69d212
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Query su una singola tabella (LINQ to DataSet)
Le query [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] possono essere eseguite su origini dati che implementano l'interfaccia  <xref:System.Collections.Generic.IEnumerable%601> o l'interfaccia <xref:System.Query.IQueryable%601>.  Poiché la classe <xref:System.Data.DataTable>non implementa nessuna di queste due interfacce, è necessario chiamare il metodo <xref:System.Data.DataTableExtensions.AsEnumerable%2A> se si desidera usare <xref:System.Data.DataTable> come origine nella clausola `From` della query [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)].  
  
 Nell'esempio seguente vengono ottenuti tutti gli ordini online della tabella SalesOrderHeader e l'output costituito da ID ordine, data dell'ordine e numero di ordine viene inviato alla console.  
  
 [!code-csharp[dp linq to dataset examples#Where1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#where1)]
 [!code-vb[dp linq to dataset examples#Where1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#where1)]  
  
 La query con variabili locali viene inizializzata con un'espressione di query, che opera su una o più fonti di informazione applicando uno o più operatori di query di tipo standard o, nel caso di [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], specifici della classe <xref:System.Data.DataSet>.  Nell'espressione di query dell'esempio precedente vengono usati due operatori di query standard: `Where` e `Select`.  
  
 La clausola `Where` filtra la sequenza in base a una condizione, in questo caso che `OnlineOrderFlag` sia impostato su `true`.  L'operatore `Select` alloca e restituisce un oggetto enumerabile che acquisisce gli argomenti passati all'operatore.  Nell'esempio precedente viene creato un tipo anonimo con tre proprietà: `SalesOrderID`, `OrderDate` e `SalesOrderNumber`.  I valori di queste tre proprietà vengono impostati sui valori delle colonne `SalesOrderID`, `OrderDate` e `SalesOrderNumber` della tabella `SalesOrderHeader`.  
  
 Il ciclo `foreach` enumera quindi gli oggetti enumerabili restituiti da `Select` e produce i risultati della query.  Poiché la query è un tipo <xref:System.Linq.Enumerable>, che implementa <xref:System.Collections.Generic.IEnumerable%601>, la valutazione della query viene posticipata finché non viene eseguita un'iterazione della variabile di query in un ciclo `foreach`.  La valutazione posticipata della query consente di mantenere le query come valori che è possibile valutare più volte, ogni volta con un risultato potenzialmente diverso.  
  
 Il metodo <xref:System.Data.DataRowExtensions.Field%2A> fornisce l'accesso ai valori di colonna di un oggetto <xref:System.Data.DataRow> e <xref:System.Data.DataRowExtensions.SetField%2A> \(non illustrato nell'esempio precedente\) imposta i valori di colonna in <xref:System.Data.DataRow>.  Poiché i metodi <xref:System.Data.DataRowExtensions.Field%2A> e <xref:System.Data.DataRowExtensions.SetField%2A> gestiscono tipi nullable, non è necessario verificare in modo esplicito la presenza di valori Null.  Entrambi metodi sono inoltre generici, quindi non è necessario eseguire i cast del tipo restituito.  È possibile usare la funzione di accesso della colonna preesistente in <xref:System.Data.DataRow> \(ad esempio, `o["OrderDate"]`\), ma in questo caso è necessario eseguire il cast dell'oggetto restituito nel tipo appropriato.  Se la colonna è nullable, è necessario verificare se il valore è Null usando il metodo <xref:System.Data.DataRow.IsNull%2A>.  Per altre informazioni, vedere [Metodi generici Field e SetField](../../../../docs/framework/data/adonet/generic-field-and-setfield-methods-linq-to-dataset.md).  
  
 Si noti che il tipo di dati specificato nel parametro `T` generico del metodo <xref:System.Data.DataRowExtensions.Field%2A> e del metodo <xref:System.Data.DataRowExtensions.SetField%2A> deve corrispondere al tipo del valore sottostante; in caso contrario, verrà generata un'eccezione <xref:System.InvalidCastException>.  Il nome di colonna specificato deve inoltre corrispondere al nome di una colonna presente in <xref:System.Data.DataSet>; in caso contrario, verrà generata un'eccezione <xref:System.ArgumentException>.  In entrambi casi, l'eccezione viene generata in fase di esecuzione durante l'enumerazione dei dati quando viene eseguita la query.  
  
## Vedere anche  
 [Query tra tabelle](../../../../docs/framework/data/adonet/cross-table-queries-linq-to-dataset.md)   
 [Esecuzione di query su DataSet tipizzati](../../../../docs/framework/data/adonet/querying-typed-datasets.md)   
 [Metodi generici Field e SetField](../../../../docs/framework/data/adonet/generic-field-and-setfield-methods-linq-to-dataset.md)