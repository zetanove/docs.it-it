---
title: "Calcolare la somma di valori in una sequenza numerica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24e335b0-984e-4825-8721-0a91b533b7c3
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Calcolare la somma di valori in una sequenza numerica
Per calcolare la somma di valori numerici in una sequenza, usare l'operatore <xref:System.Linq.Enumerable.Sum%2A>.  
  
 Di seguito sono riportate le caratteristiche dell'operatore `Sum` in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]:  
  
-   L'operatore di aggregazione `Sum` dell'operatore di query standard restituisce valori zero per tutte le sequenze vuote o che contengono solo valori null.  In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] la semantica di SQL rimane invariata.  Per questo motivo `Sum` restituisce null anziché zero per una sequenza vuota o per una sequenza che contiene solo valori null.  
  
-   Le limitazioni di SQL sui risultati intermedi vengono applicate agli aggregati in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  La somma delle quantità di valori integer a 32 bit non viene calcolata usando risultati a 64 bit ed è possibile che si verifichi un overflow per la conversione [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] di `Sum`.  Questa possibilità esiste anche se l'implementazione dell'operatore di query standard non provoca un overflow per la corrispondente sequenza in memoria.  
  
## Esempio  
 Nell'esempio seguente viene cercato il costo di trasporto complessivo di tutti gli ordini contenuti nella tabella `Order`.  
  
 Se si esegue questa query sul database di esempio Northwind, l'output sarà: `64942.6900`.  
  
 [!code-csharp[DLinqQueryExamples#12](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#12)]
 [!code-vb[DLinqQueryExamples#12](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#12)]  
  
## Esempio  
 Nell'esempio seguente viene cercato il numero complessivo di unità ordinate per tutti i prodotti.  
  
 Se si esegue questa query sul database di esempio Northwind, l'output sarà: `780`.  
  
 Notare che è necessario eseguire il cast dei tipi `short`, ad esempio `UnitsOnOrder`, in quanto in `Sum` non è disponibile alcun overload per tali tipi.  
  
 [!code-csharp[DLinqQueryExamples#13](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#13)]
 [!code-vb[DLinqQueryExamples#13](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#13)]  
  
## Vedere anche  
 [Query di aggregazione](../../../../../../docs/framework/data/adonet/sql/linq/aggregate-queries.md)   
 [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)