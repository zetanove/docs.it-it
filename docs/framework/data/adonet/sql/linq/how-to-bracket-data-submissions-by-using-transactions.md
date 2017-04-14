---
title: "Procedura: raggruppare gli invii dei dati mediante le transazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 94044a31-de90-479b-935a-8159b4ae5c5a
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: raggruppare gli invii dei dati mediante le transazioni
È possibile usare <xref:System.Transactions.TransactionScope> per raggruppare gli invii al database.  Per altre informazioni, vedere [Supporto di transazioni](../../../../../../docs/framework/data/adonet/sql/linq/transaction-support.md).  
  
## Esempio  
 Nel codice seguente l'invio al database viene incluso in <xref:System.Transactions.TransactionScope>.  
  
 [!code-csharp[DLinqSubmittingChanges#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#3)]
 [!code-vb[DLinqSubmittingChanges#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#3)]  
  
## Vedere anche  
 [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)   
 [Scrittura e invio di modifiche di dati](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)   
 [Supporto di transazioni](../../../../../../docs/framework/data/adonet/sql/linq/transaction-support.md)