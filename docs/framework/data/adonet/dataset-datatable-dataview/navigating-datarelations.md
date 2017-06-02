---
title: "Navigazione in DataRelations | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5e673f4-9b44-45ae-aaea-c504d1cc5d3e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Navigazione in DataRelations
Una delle funzioni principali di un oggetto <xref:System.Data.DataRelation> è di consentire la navigazione da una <xref:System.Data.DataTable> all'altra all'interno di un <xref:System.Data.DataSet>.  In questo modo è possibile recuperare tutti gli oggetti <xref:System.Data.DataRow> correlati all'interno di una **DataTable** nel caso in cui venga dato un singolo oggetto **DataRow** proveniente da una **DataTable** correlata.  Dopo aver ad esempio stabilito una **DataRelation** tra una tabella di clienti e una tabella di ordini, è possibile recuperare tutte le righe di ordine relative a un particolare cliente usando **GetChildRows**.  
  
 Nell'esempio di codice seguente viene creata una **DataRelation** tra la tabella **Customers** e la tabella **Orders** di un **DataSet** e vengono restituiti tutti gli ordini per ogni cliente.  
  
 [!code-csharp[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/VB/source.vb#1)]  
  
 Nell'esempio successivo, basato su quello precedente, vengono correlate quattro tabelle e vengono esplorate tali relazioni.  Come mostrato nell'esempio precedente, **CustomerID** consente di correlare la tabella **Customers** alla tabella **Orders**.  Per ogni cliente della tabella **Customers** vengono determinate tutte le righe figlio della tabella **Orders**, in modo da restituire il numero di ordini associati a un determinato cliente e i relativi valori **OrderID**.  
  
 Nell'esempio ampliato, inoltre, vengono restituiti i valori delle tabelle **OrderDetails** e **Products**.  La tabella **Orders** è correlata alla tabella **OrderDetails** tramite **OrderID**, che consente di determinare i prodotti e le quantità ordinate per ogni ordine cliente.  Poiché la tabella **OrderDetails** contiene solo il **ProductID** di un prodotto ordinato, la tabella **OrderDetails** è correlata alla tabella **Products** tramite **ProductID**, in modo da restituire il valore **ProductName**.  In questo tipo di relazione, **Products** è la tabella padre mentre **Order Details** è la tabella figlio.  Di conseguenza, quando si esegue una reiterazione della tabella **OrderDetails**, **GetParentRow** viene chiamato per consentire il recupero del valore **ProductName** correlato.  
  
 Notare che al momento della creazione dell'oggetto **DataRelation** per le tabelle **Customers** e **Orders** non viene specificato alcun valore per il flag **createConstraints** \(il valore predefinito è **true**\).  Si presuppone che tutte le righe della tabella **Orders** dispongano di un valore **CustomerID** esistente nella tabella padre **Customers**.  Se la tabella **Orders** contiene un valore **CustomerID** non presente nella tabella **Customers**, un vincolo <xref:System.Data.ForeignKeyConstraint> provocherà un'eccezione.  
  
 Se è possibile che nella colonna figlio siano presenti valori non contenuti nella colonna padre, impostare il flag **createConstraints** su **false** quando si aggiunge l'oggetto **DataRelation**.  Nell'esempio seguente il flag **createConstraints** viene impostato su **false** per l'oggetto **DataRelation** tra la tabella **Orders** e la tabella **OrderDetails**.  Ciò consente all'applicazione di restituire tutti i record della tabella **OrderDetails** e solo un subset di record della tabella **Orders**, senza che venga generata alcuna eccezione in fase di esecuzione.  Nell'esempio ampliato viene generato un output con il seguente formato.  
  
```  
Customer ID: NORTS  
  Order ID: 10517  
        Order Date: 4/24/1997 12:00:00 AM  
           Product: Filo Mix  
          Quantity: 6  
           Product: Raclette Courdavault  
          Quantity: 4  
           Product: Outback Lager  
          Quantity: 6  
  Order ID: 11057  
        Order Date: 4/29/1998 12:00:00 AM  
           Product: Outback Lager  
          Quantity: 3  
```  
  
 L'esempio di codice seguente è un esempio ampliato, in cui vengono restituiti i valori delle tabelle **OrderDetails** e **Products** e solo un subset di record della tabella **Orders**.  
  
 [!code-csharp[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/VB/source.vb#1)]  
  
## Vedere anche  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)