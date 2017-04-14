---
title: "Procedura: riutilizzare una connessione tra un comando ADO.NET e DataContext | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7e26c7eb-c18a-43b5-a8f0-28fd8b04b0f0
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: riutilizzare una connessione tra un comando ADO.NET e DataContext
Poiché [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fa parte della famiglia di tecnologie [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] ed è basato sui servizi forniti da [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)], è possibile riutilizzare una connessione tra un comando [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] e <xref:System.Data.Linq.DataContext>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come riutilizzare la stessa connessione tra un comando [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] e <xref:System.Data.Linq.DataContext>.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#4)]
 [!code-vb[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#4)]  
  
## Vedere anche  
 [Informazioni complementari](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [ADO.NET e LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/ado-net-and-linq-to-sql.md)   
 [Comunicazioni con il database](../../../../../../docs/framework/data/adonet/sql/linq/communicating-with-the-database.md)