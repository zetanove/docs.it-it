---
title: "Introduzione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: db8a557a-fef8-4f4f-bb91-8cff7250ee25
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Introduzione
Usando [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è possibile avvalersi della tecnologia [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] per accedere ai database SQL come se si trattasse di una raccolta in memoria.  
  
 Ad esempio, l'oggetto `nw` nel codice seguente viene creato per rappresentare il database `Northwind`, viene usata `Customers` come tabella di destinazione, le righe vengono filtrate in base a `Customers` residenti a `London` e viene selezionata una stringa da recuperare relativa a `CompanyName`.  
  
 Quando viene eseguito il ciclo, viene recuperata la raccolta di valori `CompanyName`.  
  
 [!code-csharp[DLinqGettingStarted#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#1)]
 [!code-vb[DLinqGettingStarted#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#1)]  
  
## Passaggi successivi  
 Per alcuni esempi aggiuntivi, inclusi quelli relativi alle operazioni di inserimento e aggiornamento, vedere [Operazioni eseguibili con LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/what-you-can-do-with-linq-to-sql.md).  
  
 Provare quindi a eseguire alcune procedure dettagliate ed esercitazioni per acquisire un'esperienza pratica relativa all'utilizzo di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Vedere [Apprendimento tramite le procedure dettagliate](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md).  
  
 Apprendere infine come iniziare a usare un progetto [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] personalizzato leggendo [Passaggi comuni per l'utilizzo di LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/typical-steps-for-using-linq-to-sql.md).  
  
## Vedere anche  
 [LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/index.md)   
 [Introduction to LINQ](../../../../../../ocs/visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Il modello a oggetti LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)