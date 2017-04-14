---
title: "Procedura: utilizzare stored procedure mappate per forme di risultati multipli | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2b84dfe-7fec-489a-92de-45215cec4518
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: utilizzare stored procedure mappate per forme di risultati multipli
Quando una stored procedure consente di restituire più forme di risultati, il tipo restituito non può essere fortemente tipizzato a una singola forma di proiezione.  Anche se in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] possono essere generati tutti i tipi di proiezione possibili, non è possibile conoscere l'ordine in cui saranno restituiti.  
  
 Si consideri questo scenario rispetto a stored procedure che producono più forme di risultati in sequenza.  Per altre informazioni, vedere [Procedura: utilizzare stored procedure mappate per forme di risultati sequenziali](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-mapped-for-sequential-result-shapes.md).  
  
 L'attributo <xref:System.Data.Linq.Mapping.ResultTypeAttribute> viene applicato a stored procedure che restituiscono più tipi di risultati per specificare il set di tipi che la stored procedure può restituire.  
  
## Esempio  
 Nell'esempio di codice SQL riportato di seguito la forma dei risultati dipende dall'input \(`shape =1` o `shape = 2`\).  Non si conosce la proiezione che verrà restituita per prima.  
  
```  
CREATE PROCEDURE VariableResultShapes(@shape int)  
AS  
if(@shape = 1)  
    select CustomerID, ContactTitle, CompanyName from customers  
else if(@shape = 2)  
    select OrderID, ShipName from orders  
```  
  
 [!code-csharp[DLinqSprox#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#4)]
 [!code-vb[DLinqSprox#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#4)]  
  
## Esempio  
 Per eseguire questa stored procedure si utilizzerà codice simile al seguente.  
  
> [!NOTE]
>  È necessario usare il modello <xref:System.Data.Linq.IMultipleResults.GetResult%2A> per ottenere un enumeratore di tipo corretto, in base alla propria conoscenza della stored procedure.  
  
 [!code-csharp[DLinqSprox#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#5)]
 [!code-vb[DLinqSprox#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#5)]  
  
## Vedere anche  
 [Stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)