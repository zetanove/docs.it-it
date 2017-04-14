---
title: "Operazioni eseguibili con LINQ to SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 061d98b2-baa7-4336-8ad2-c14de8134d91
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Operazioni eseguibili con LINQ to SQL
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sono supportare tutte le funzionalità principali usate dagli sviluppatori SQL. È possibile creare query per ottenere informazioni ed eseguire operazioni di inserimento, aggiornamento ed eliminazione di dati dalle tabelle.  
  
## Selezione  
 Per eseguire una selezione \(*proiezione*\) è sufficiente scrivere una query [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] nel proprio linguaggio di programmazione e successivamente eseguirla per recuperare i risultati. In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tutte le operazioni indispensabili vengono convertite nelle operazioni SQL necessarie con cui si ha dimestichezza. Per altre informazioni, vedere [LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/index.md).  
  
 Nell'esempio seguente i nomi di società dei clienti dell'area londinese vengono recuperati e visualizzati nella finestra della console.  
  
 [!code-csharp[DLinqGettingStarted#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#1)]
 [!code-vb[DLinqGettingStarted#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#1)]  
  
## Inserimento  
 Per eseguire un'operazione `Insert` SQL, aggiungere semplicemente oggetti al modello a oggetti creato e chiamare <xref:System.Data.Linq.DataContext.SubmitChanges%2A> su <xref:System.Data.Linq.DataContext>.  
  
 Nell'esempio seguente vengono aggiunti un nuovo cliente e informazioni sul cliente alla tabella `Customers` usando <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>.  
  
 [!code-csharp[DLinqGettingStarted#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#2)]
 [!code-vb[DLinqGettingStarted#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#2)]  
  
## Updating  
 Per eseguire un'operazione `Update` per una voce del database, recuperare innanzitutto tale voce e modificarla direttamente nel modello a oggetti. Dopo avere modificato l'oggetto, chiamare <xref:System.Data.Linq.DataContext.SubmitChanges%2A> su <xref:System.Data.Linq.DataContext> per aggiornare il database.  
  
 Nell'esempio seguente vengono recuperati tutti i clienti dell'area londinese. Il nome della città viene quindi modificato da "London" in "London \- Metro", infine viene chiamato <xref:System.Data.Linq.DataContext.SubmitChanges%2A> per inviare le modifiche al database.  
  
 [!code-csharp[DLinqGettingStarted#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#3)]
 [!code-vb[DLinqGettingStarted#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#3)]  
  
## Eliminazione  
 Per eseguire un'operazione `Delete` per un elemento, rimuovere l'elemento dalla raccolta a cui appartiene, quindi chiamare <xref:System.Data.Linq.DataContext.SubmitChanges%2A> su <xref:System.Data.Linq.DataContext> per eseguire il commit della modifica.  
  
> [!NOTE]
>  In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non vengono riconosciute le operazioni di eliminazione a sovrapposizione. Per eliminare una riga in una tabella contenente vincoli, vedere [Procedura: eliminare righe dal database](../../../../../../docs/framework/data/adonet/sql/linq/how-to-delete-rows-from-the-database.md).  
  
 Nell'esempio seguente il cliente con il codice `CustomerID``98128` viene recuperato dal database. Quindi, dopo la conferma che la riga del cliente è stata recuperata, viene chiamato <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> per rimuovere quell'oggetto dalla raccolta. Infine viene chiamato <xref:System.Data.Linq.DataContext.SubmitChanges%2A> per inoltrare l'operazione di eliminazione al database.  
  
 [!code-csharp[DLinqGettingStarted#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#4)]
 [!code-vb[DLinqGettingStarted#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#4)]  
  
## Vedere anche  
 [Guida per programmatori](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)   
 [Il modello a oggetti LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)   
 [Introduzione](../../../../../../docs/framework/data/adonet/sql/linq/getting-started.md)