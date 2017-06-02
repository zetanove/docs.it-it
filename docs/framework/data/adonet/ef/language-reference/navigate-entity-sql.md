---
title: "NAVIGATE (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: f107f29d-005f-4e39-a898-17f163abb1d0
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# NAVIGATE (Entity SQL)
Consente di eseguire la navigazione nella relazione stabilita tra le entità.  
  
## Sintassi  
  
```  
  
navigate(instance-expresssion, [relationship-type], [to-end [, from-end] ])  
```  
  
## Argomenti  
 `instance-expresssion`  
 Istanza di un'entità.  
  
 `relationship-type`  
 Nome del tipo della relazione, dal file CSDL \(Conceptual Schema Definition Language\).`relationship-type` è qualificato come \<spazio dei nomi\> \<nome tipo relazione\>  
  
 `to`  
 Entità finale della relazione.  
  
 `from`  
 Inizio della relazione.  
  
## Valore restituito  
 Se la cardinalità dell'entità finale è 1, il valore restituito è `Ref<T>`. Se la cardinalità dell'entità finale è n, il valore restituito è `Collection<Ref<T>>`.  
  
## Note  
 Le relazioni sono costrutti di primaria importanza in [!INCLUDE[adonet_edm](../../../../../../includes/adonet-edm-md.md)] \(EDM\). È possibile stabilire relazioni tra due o più tipi di entità e navigare nella relazione da un'entità finale all'altra. I parametri `from` e `to` sono condizionatamente facoltativi in assenza di ambiguità nella risoluzione dei nomi all'interno della relazione.  
  
 NAVIGATE è valido nello spazio O e C.  
  
 Il formato generale di un costrutto di navigazione è il seguente:  
  
 navigate\(`instance-expresssion`, `relationship-type`, \[ `to-end` \[, `from-end` \] \] \)  
  
 Ad esempio:  
  
```  
Select o.Id, navigate(o, OrderCustomer, Customer, Order)  
From LOB.Orders as o  
```  
  
 Dove OrderCustomer è l'oggetto `relationship`, mentre Customer e Order rappresentano l'oggetto `to-end` \(Customer\) e l'oggetto `from-end` \(Order\) della relazione. Se OrderCustomer è una relazione n:1, il tipo di risultato dell'espressione di navigazione è Ref\<Customer\>.  
  
 La forma più semplice di questa espressione è la seguente:  
  
```  
Select o.Id, navigate(o, OrderCustomer)  
From LOB.Orders as o  
```  
  
 Analogamente, in una query nel formato seguente, l'espressione di navigazione produrrebbe come risultato Collection\<Ref\<Order\>\>.  
  
```  
Select c.Id, navigate(c, OrderCustomer, Order, Customer)  
From LOB.Customers as c  
```  
  
 L'espressione dell'istanza deve essere un tipo di entità\/riferimento.  
  
## Esempio  
 Nella query Entity SQL seguente viene usato l'operatore NAVIGATE per eseguire la navigazione nella relazione stabilita tra i tipi di entità Address e SalesOrderHeader. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#NAVIGATE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#navigate)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [How to: Navigate Relationships with Navigate Operator](../../../../../../docs/framework/data/adonet/ef/language-reference/navigate-entity-sql.md)