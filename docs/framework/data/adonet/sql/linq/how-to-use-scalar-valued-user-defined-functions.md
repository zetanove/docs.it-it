---
title: "Procedura: utilizzare le funzioni con valori scalari definite dall&#39;utente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 714e252f-c053-4bbb-b1f3-924111cd4d97
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: utilizzare le funzioni con valori scalari definite dall&#39;utente
È possibile eseguire il mapping di un metodo client definito in una classe a una funzione definita dall'utente usando l'attributo <xref:System.Data.Linq.Mapping.FunctionAttribute>.  Notare che nel corpo del metodo viene costruita un'espressione che acquisisce lo scopo della chiamata al metodo e passa quell'espressione a <xref:System.Data.Linq.DataContext> per la conversione e l'esecuzione.  
  
> [!NOTE]
>  Si verifica l'esecuzione diretta solo se la funzione viene chiamata all'esterno di una query.  Per altre informazioni, vedere [Procedura: chiamare funzioni inline definite dall'utente](../../../../../../docs/framework/data/adonet/sql/linq/how-to-call-user-defined-functions-inline.md).  
  
## Esempio  
 Nel codice SQL seguente viene presentata una funzione con valori scalari definita dall'utente `ReverseCustName()`.  
  
```  
CREATE FUNCTION ReverseCustName(@string varchar(100))  
RETURNS varchar(100)  
AS  
BEGIN  
    DECLARE @custName varchar(100)  
    -- Implementation left as exercise for users.  
    RETURN @custName  
END  
```  
  
 Per questo codice si eseguirà il mapping di un metodo client come il seguente:  
  
 [!code-csharp[DLinqUDFS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/northwind-tfunc.cs#3)]
 [!code-vb[DLinqUDFS#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/northwind-tfunc.vb#3)]  
  
## Vedere anche  
 [Funzioni definite dall'utente](../../../../../../docs/framework/data/adonet/sql/linq/user-defined-functions.md)