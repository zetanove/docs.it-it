---
title: "Procedura: utilizzare le stored procedure che accettano parametri | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b935fd84-cb9c-4205-8c48-658d5db2ec93
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: utilizzare le stored procedure che accettano parametri
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene eseguito il mapping dei parametri di output ai parametri di riferimento, mentre per i tipi di valori il parametro viene dichiarato come nullable.  
  
 Per un esempio di come usare un parametro di input in una query che restituisce un rowset, vedere [Procedura: restituire rowset](../../../../../../docs/framework/data/adonet/sql/linq/how-to-return-rowsets.md).  
  
## Esempio  
 Nell'esempio seguente viene accettato un solo parametro di input \(l'ID del cliente\) e viene restituito un parametro out \(le vendite totali per quel cliente\).  
  
```  
CREATE PROCEDURE [dbo].[CustOrderTotal]   
@CustomerID nchar(5),  
@TotalSales money OUTPUT  
AS  
SELECT @TotalSales = SUM(OD.UNITPRICE*(1-OD.DISCOUNT) * OD.QUANTITY)  
FROM ORDERS O, "ORDER DETAILS" OD  
where O.CUSTOMERID = @CustomerID AND O.ORDERID = OD.ORDERID  
```  
  
 [!code-csharp[DLinqSprox#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#2)]
 [!code-vb[DLinqSprox#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#2)]  
  
## Esempio  
 Chiamare questa stored procedure come segue:  
  
 [!code-csharp[DLinqSprox#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#3)]
 [!code-vb[DLinqSprox#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#3)]  
  
## Vedere anche  
 [Stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)   
 [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)   
 [Utilizzo dei tipi nullable](../Topic/Using%20Nullable%20Types%20\(C%23%20Programming%20Guide\).md)   
 [Nullable Value Types](../Topic/Nullable%20Value%20Types%20\(Visual%20Basic\).md)