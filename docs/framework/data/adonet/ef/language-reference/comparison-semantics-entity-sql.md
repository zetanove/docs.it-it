---
title: "Semantica di confronto (Entity SQL) | Microsoft Docs"
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
ms.assetid: b36ce28a-2fe4-4236-b782-e5f7c054deae
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Semantica di confronto (Entity SQL)
L'esecuzione di uno degli operatori [!INCLUDE[esql](../../../../../../includes/esql-md.md)] seguenti comporta un confronto tra istanze di tipi:  
  
## Confronto esplicito  
 Operazioni di uguaglianza:  
  
-   \=  
  
-   \!\=  
  
 Operazioni di ordinamento:  
  
-   \<  
  
-   \<\=  
  
-   \>  
  
-   \>\=  
  
 Operazioni di impostazione del supporto dei valori Null:  
  
-   IS NULL  
  
-   IS NOT NULL  
  
## Distinzione esplicita  
 Distinzione di uguaglianza:  
  
-   DISTINCT  
  
-   GROUP BY  
  
 Distinzione di ordinamento:  
  
-   ORDER BY  
  
## Distinzione implicita  
 Predicati e operazioni sui set \(uguaglianza\):  
  
-   UNION  
  
-   INTERSECT  
  
-   EXCEPT  
  
-   SET  
  
-   OVERLAPS  
  
 Predicati degli elementi \(uguaglianza\):  
  
-   IN  
  
## Combinazioni supportate  
 Nella tabella seguente sono illustrate tutte le combinazioni supportate di operatori di confronto per ognuno dei tipi:  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**Tipo**|**\=**<br /><br /> **\!\=**|**GROUP BY**<br /><br /> **DISTINCT**|**UNION**<br /><br /> **INTERSECT**<br /><br /> **EXCEPT**<br /><br /> **SET**<br /><br /> **OVERLAPS**|**IN**|**\<   \<\=**<br /><br /> **\>   \>\=**|**ORDER BY**|**IS NULL**<br /><br /> **IS NOT NULL**|  
|Tipo di entità|Rif<sup>1</sup>|Tutte le proprietà<sup>2</sup>|Tutte le proprietà<sup>2</sup>|Tutte le proprietà<sup>2</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Rif<sup>1</sup>|  
|Tipo complesso|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|  
|Riga|Tutte le proprietà<sup>4</sup>|Tutte le proprietà<sup>4</sup>|Tutte le proprietà<sup>4</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Tutte le proprietà<sup>4</sup>|Eccezione generata<sup>3</sup>|  
|Tipo primitivo|Specifico del provider|Specifico del provider|Specifico del provider|Specifico del provider|Specifico del provider|Specifico del provider|Specifico del provider|  
|Multiset|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|  
|Rif|Sì <sup>5</sup>|Sì <sup>5</sup>|Sì <sup>5</sup>|Sì <sup>5</sup>|Throw|Throw|Sì <sup>5</sup>|  
|Associazione<br /><br /> tipo|Eccezione generata<sup>3</sup>|Throw|Throw|Throw|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|Eccezione generata<sup>3</sup>|  
  
 <sup>1</sup>I riferimenti delle istanze del tipo di entità specificato vengono confrontati in modo implicito, come illustrato nell'esempio seguente:  
  
```  
SELECT p1, p2   
FROM AdventureWorksEntities.Product AS p1   
     JOIN AdventureWorksEntities.Product AS p2   
WHERE p1 != p2 OR p1 IS NULL  
```  
  
 Un'istanza di entità non può essere confrontata con un riferimento esplicito.  Se viene eseguito un tentativo di questo tipo, viene generata un'eccezione.  La query seguente comporta, ad esempio, la generazione di un'eccezione:  
  
```  
SELECT p1, p2   
FROM AdventureWorksEntities.Product AS p1   
     JOIN AdventureWorksEntities.Product AS p2   
WHERE p1 != REF(p2)  
```  
  
 <sup>2</sup>Le proprietà dei tipi complessi sono impostate come bidimensionali prima di essere inviate all'archivio, pertanto è possibile eseguirne il confronto \(a condizione che tutte le relative proprietà possano essere confrontate\).  Vedere anche <sup>4.</sup>  
  
 <sup>3</sup>Il runtime di Entity Framework rileva il caso non supportato e genera un'eccezione significativa senza ricorrere al provider o all'archivio.  
  
 <sup>4</sup>Viene eseguito un tentativo di confrontare tutte le proprietà.  Se è presente una proprietà che non è possibile confrontare, ad esempio un tipo text, ntext o image, viene generata un'eccezione nel server.  
  
 <sup>5</sup>Vengono confrontati tutti i singoli elementi dei riferimenti \(inclusi il nome del set di entità e tutte le proprietà chiave del tipo di entità\).  
  
## Vedere anche  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)