---
title: "Definizioni dei tipi (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 306b204a-ade5-47ef-95b5-c785d2da4a7e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Definizioni dei tipi (Entity SQL)
Una definizione del tipo viene usata nell'istruzione per la dichiarazione di una funzione inline [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
## Note  
 L'istruzione per la dichiarazione per una funzione inline consiste della parola chiave [FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md) seguita dall'identificatore che rappresenta il nome della funzione \(ad esempio, "MyAvg"\) seguito da un elenco di definizioni dei parametri tra parentesi \(ad esempio, "dues Collection\(Decimal\)"\).  
  
 L'elenco di definizioni dei parametri è costituito da zero o più definizioni di parametri.  Ogni definizione di parametro consiste di un identificatore \(il nome del parametro alla funzione, ad esempio, "dues"\) seguito da una definizione del tipo \(ad esempio, "Collection\(Decimal\)"\).  
  
 Le definizioni del tipo possono essere:  
  
-   Il tipo dell'identificatore \(ad esempio, "Int32" o "AdventureWorks.Order"\).  
  
-   La parola chiave `COLLECTION` seguita da un'altra definizione del tipo tra parentesi \(ad esempio "Collection\(AdventureWorks.Order\)"\).  
  
-   La parola chiave ROW seguita da un elenco di definizioni di proprietà tra parentesi \(ad esempio "Row\(x AdventureWorks.Order\)"\).  Le definizioni di proprietà dispongono del formato "`identifier type_definition`, `identifier type_definition`, ... ".  
  
-   La parola chiave REF seguita dal tipo dell'identificatore tra parentesi \(ad esempio "Ref\(AdventureWorks.Order\)"\).  L'operatore della definizione del tipo Ref richiede un tipo di entità come argomento.  Non è possibile specificare un tipo primitivo come argomento.  
  
 È inoltre possibile annidare definizioni del tipo \(ad esempio "Collection\(Row\(x Ref\(AdventureWorks.Order\)\)\)"\).  
  
 Le opzioni di definizione del tipo sono:  
  
-   `IdentifierName supported_type` o  
  
-   `IdentifierName` COLLECTION\(`type_definition`\) o  
  
-   `IdentifierName` ROW\(`property_definition`\) o  
  
-   `IdentifierName` REF\(`supported_entity_type`\)  
  
 L'opzione di definizione delle proprietà è `IdentifierName type_definition`.  
  
 I tipi supportati sono qualsiasi tipo nello spazio dei nomi corrente.  Questi includono sia i tipi primitivi che i tipi di entità.  
  
 Tipi di entità supportati si riferiscono solo a tipi di entità nello spazio dei nomi corrente.  Non includono i tipi primitivi.  
  
## Esempi  
 Di seguito è riportato un esempio di definizione del tipo semplice.  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 EDM.Decimal) AS (  
   Round(p1)  
)  
MyRound(CAST(1.7 as EDM.Decimal))  
```  
  
 Di seguito è riportato un esempio di definizione del tipo COLLECTION.  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Collection(EDM.Decimal)) AS (  
   Select Round(p1) from p1  
)  
MyRound({CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)})  
```  
  
 Di seguito è riportato un esempio di definizione del tipo ROW.  
  
```  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Row(x EDM.Decimal)) AS (  
   Round(p1.x)  
)  
select MyRound(row(a as x)) from {CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)} as a  
```  
  
 Di seguito è riportato un esempio di definizione del tipo REF.  
  
```  
USING Microsoft.Samples.Entity  
Function UnReference(p1 Ref(AdventureWorks.Order)) AS (  
   Deref(p1)  
)  
select Ref(x) from AdventureWorksEntities.SalesOrderHeaders as x  
```  
  
## Vedere anche  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)