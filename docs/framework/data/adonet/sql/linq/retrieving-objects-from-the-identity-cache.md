---
title: "Recupero di oggetti dalla cache delle identit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96c13903-ccb6-4a0e-ab6a-8ca955ca314d
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Recupero di oggetti dalla cache delle identit&#224;
In questo argomento vengono descritti i tipi di query LINQ to SQL che restituiscono un oggetto dalla cache delle identità gestita dall'oggetto <xref:System.Data.Linq.DataContext>.  
  
 In LINQ to SQL, uno dei modi in cui l'oggetto <xref:System.Data.Linq.DataContext> gestisce gli oggetti prevede la registrazione delle identità degli oggetti in una cache delle identità durante l'esecuzione delle query.  In alcuni casi, LINQ to SQL tenterà di recuperare un oggetto dalla cache delle identità prima di eseguire una query nel database.  
  
 In generale, affinché una query LINQ to SQL restituisca un oggetto dalla cache delle identità, la query deve essere basata sulla chiave primaria di un oggetto e deve restituire un unico oggetto.  In particolare, il formato della query deve essere uno di quelli illustrati di seguito.  
  
> [!NOTE]
>  Le query precompilate non restituiranno oggetti dalla cache delle identità.  Per altre informazioni sulle query precompilate, vedere <xref:System.Data.Linq.CompiledQuery> e [Procedura: archiviare e riutilizzare le query](../../../../../../docs/framework/data/adonet/sql/linq/how-to-store-and-reuse-queries.md).  
  
 Il formato di una query deve essere uno dei formati generali riportati di seguito per poter recuperare un oggetto dalla cache delle identità:  
  
-   <xref:System.Data.Linq.Table%601> `.Function1(` `predicate` `)`  
  
-   <xref:System.Data.Linq.Table%601> `.Function1(` `predicate` `).Function2()`  
  
 In questi formati generali, `Function1`, `Function2` e `predicate` vengono definiti nel modo seguente.  
  
 `Function1` può essere uno degli elementi seguenti:  
  
-   <xref:System.Linq.Queryable.Where%2A>  
  
-   <xref:System.Linq.Queryable.First%2A>  
  
-   <xref:System.Linq.Queryable.FirstOrDefault%2A>  
  
-   <xref:System.Linq.Queryable.Single%2A>  
  
-   <xref:System.Linq.Queryable.SingleOrDefault%2A>  
  
 `Function2` può essere uno degli elementi seguenti:  
  
-   <xref:System.Linq.Queryable.First%2A>  
  
-   <xref:System.Linq.Queryable.FirstOrDefault%2A>  
  
-   <xref:System.Linq.Queryable.Single%2A>  
  
-   <xref:System.Linq.Queryable.SingleOrDefault%2A>  
  
 `predicate` deve essere un'espressione in cui la proprietà della chiave primaria dell'oggetto è impostata su un valore costante.  Se un oggetto dispone di una chiave primaria definita da più proprietà, ogni proprietà della chiave primaria deve essere impostata su un valore costante.  Di seguito sono riportati esempi del formato che deve essere adottato da `predicate`:  
  
-   `c => c.PK == constant_value`  
  
-   `c => c.PK1 == constant_value1 && c=> c.PK2 == constant_value2`  
  
## Esempio  
 Nel codice seguente vengono forniti esempi di tipi di query LINQ to SQL che recuperano un oggetto dalla cache delle identità.  
  
 [!code-csharp[L2S_QueryCache#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/l2s_querycache/cs/program.cs#1)]
 [!code-vb[L2S_QueryCache#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/l2s_querycache/vb/module1.vb#1)]  
  
## Vedere anche  
 [Concetti relativi alle query](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)   
 [Identità di oggetti](../../../../../../docs/framework/data/adonet/sql/linq/object-identity.md)   
 [Informazioni complementari](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [Identità di oggetti](../../../../../../docs/framework/data/adonet/sql/linq/object-identity.md)