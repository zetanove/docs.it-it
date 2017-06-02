---
title: "GROUP BY (Entity SQL) | Microsoft Docs"
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
ms.assetid: cf4f4972-4724-4945-ba44-943a08549139
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# GROUP BY (Entity SQL)
Specifica i gruppi nei quali devono essere inseriti gli oggetti restituiti da un'espressione \([SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)\) di query.  
  
## Sintassi  
  
```  
  
[ GROUP BY aliasedExpression [ ,...n ] ]  
```  
  
## Argomenti  
 `aliasedExpression`  
 Qualsiasi espressione di query valida sulla quale viene eseguito il raggruppamento.`expression` può essere una proprietà o un'espressione non di aggregazione che fa riferimento a una proprietà restituita dalla clausola FROM. Ogni espressione in una clausola GROUP BY deve restituire un tipo che può essere confrontato per verificare l'uguaglianza. Questi tipi sono in genere tipi primitivi scalari ad esempio numeri, stringhe e date. Non è possibile eseguire un raggruppamento in base a una raccolta.  
  
## Note  
 Se nell'argomento \<select list\> della clausola SELECT sono incluse funzioni di aggregazione, tramite GROUP BY viene calcolato un valore di riepilogo per ogni gruppo. Quando si specifica GROUP BY, è necessario che l'elenco GROUP BY includa ogni nome di proprietà di qualsiasi espressione non di aggregazione nell'elenco di selezione oppure che l'espressione GROUP BY corrisponda esattamente all'espressione dell'elenco di selezione.  
  
> [!NOTE]
>  Se la clausola ORDER BY non viene specificata, i gruppi restituiti dalla clausola GROUP BY non sono in un ordine preciso. Per specificare un particolare ordinamento dei dati, è consigliabile usare sempre la clausola ORDER BY.  
  
 Quando una clausola GROUP BY viene specificata, in modo esplicito o implicito \(ad esempio da una clausola HAVING nella query\), l'ambito corrente viene nascosto e viene introdotto un nuovo ambito.  
  
 La clausola SELECT, la clausola HAVING e la clausola ORDER BY non potranno più fare riferimento ai nomi di elementi specificati nella clausola FROM. È possibile fare riferimento solo alle espressioni di raggruppamento stesse. A tale scopo, è possibile assegnare nuovi nomi \(alias\) a ogni espressione di raggruppamento. Se per un'espressione di raggruppamento non viene specificato alcun alias, in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] viene eseguito un tentativo di generarne uno usando le regole di generazione di alias, come illustrato nell'esempio seguente.  
  
 `SELECT g1, g2, ...gn FROM c as c1`  
  
 `GROUP BY e1 as g1, e2 as g2, ...en as gn`  
  
 Le espressioni nella clausola GROUP BY non possono fare riferimento a nomi definiti in precedenza nella stessa clausola GROUP BY.  
  
 Oltre ai nomi dei raggruppamenti, nella clausola SELECT, nella clausola HAVING e nella clausola ORDER BY è possibile specificare anche aggregazioni. Un'aggregazione contiene un'espressione valutata per ogni elemento del gruppo. L'operatore di aggregazione riduce i valori di tutte queste espressioni, in genere, ma non sempre, in un singolo valore. L'espressione di aggregazione può fare riferimento ai nomi degli elementi originali visibili nell'ambito padre o ai nuovi nomi introdotti dalla clausola GROUP BY stessa. Sebbene le aggregazioni siano presenti nella clausola SELECT, nella clausola HAVING e nella clausola ORDER BY, vengono effettivamente valutate nello stesso ambito delle espressioni di raggruppamento, come illustrato nell'esempio seguente.  
  
 `SELECT name, sum(o.Price * o.Quantity) as total`  
  
 `FROM orderLines as o`  
  
 `GROUP BY o.Product as name`  
  
 In questa query viene usata la clausola GROUP BY per produrre un rapporto del costo di tutti i prodotti ordinati, suddiviso in base al prodotto. Viene assegnato il nome `name` al prodotto come parte dell'espressione di raggruppamento, quindi viene fatto riferimento a tale nome nell'elenco SELECT. Viene inoltre specificata la funzione `sum` di aggregazione nell'elenco SELECT, che fa riferimento internamente al prezzo e alla quantità della riga dell'ordine.  
  
 Ogni espressione chiave GROUP BY deve includere almeno un riferimento all'ambito di input:  
  
```  
SELECT FROM Persons as P  
GROUP BY Q + P   -- GOOD  
GROUP BY Q   -- BAD  
GROUP BY 1   -- BAD, a constant is not allowed  
```  
  
 Per un esempio dell'uso di GROUP BY, vedere [HAVING](../../../../../../docs/framework/data/adonet/ef/language-reference/having-entity-sql.md).  
  
## Esempio  
 Nella query Entity SQL seguente viene usato l'operatore GROUP BY per specificare i gruppi in cui gli oggetti vengono restituiti da una query. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati PrimitiveType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecutePrimitiveTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#GROUPBY](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#groupby)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Espressioni di query](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expressions-entity-sql.md)