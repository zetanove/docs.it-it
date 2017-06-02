---
title: "OFTYPE (Entity SQL) | Microsoft Docs"
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
ms.assetid: 6d259ca7-bbf0-40f8-a154-181d25c0d67e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# OFTYPE (Entity SQL)
Restituisce una raccolta di oggetti da un'espressione di query appartenente a un tipo specifico.  
  
## Sintassi  
  
```  
  
OFTYPE (expression, [ONLY] test_type)  
```  
  
## Argomenti  
 `expression`  
 Qualsiasi espressione di query valida che restituisca una raccolta di oggetti.  
  
 `test_type`  
 Il tipo rispetto al quale testare ogni oggetto restituito da `expression`. Il tipo deve essere qualificato da uno spazio dei nomi.  
  
## Valore restituito  
 Raccolta di oggetti appartenenti al tipo `test_type` o un tipo di base o un tipo derivato di `test_type`. Se si specifica ONLY, verranno restituite solo le istanze di `test_type` o una raccolta vuota.  
  
## Note  
 Un'espressione `OFTYPE` specifica un'espressione del tipo usata per eseguire un test del tipo rispetto a ogni elemento di una raccolta.  L'espressione `OFTYPE` produce una nuova raccolta del tipo specificato, contenente solo gli elementi equivalenti o al tipo o al relativo sottotipo.  
  
 Un'espressione `OFTYPE` è un'abbreviazione dell'espressione di query seguente:  
  
```  
select value treat(t as T) from ts as t where t is of (T)  
```  
  
 Dal momento che Manager è un sottotipo di Employee, l'espressione seguente produce una raccolta dei soli manager da una raccolta di dipendenti:  
  
```  
OfType(employees, NamespaceName.Manager)  
```  
  
 È inoltre possibile eseguire l'upcast di una raccolta usando il filtro del tipo:  
  
```  
OfType(executives, NamespaceName.Manager)  
```  
  
 Poiché tutti i dirigenti sono manager, la raccolta risultante contiene ancora tutti i dirigenti d'azienda originali, sebbene la raccolta sia ora indicata come una raccolta di manager.  
  
 Nella tabella seguente viene illustrato il comportamento dell'operatore `OFTYPE` con alcuni modelli. Tutte le eccezioni vengono generate sul lato client prima che il provider venga richiamato:  
  
|Criterio|Comportamento|  
|--------------|-------------------|  
|OFTYPE\(Collection\(EntityType\), EntityType\)|Collection\(EntityType\)|  
|OFTYPE\(Collection\(ComplexType\), ComplexType\)|Genera un'eccezione|  
|OFTYPE\(Collection\(RowType\), RowType\)|Genera un'eccezione|  
  
## Esempio  
 Nella query [!INCLUDE[esql](../../../../../../includes/esql-md.md)] seguente viene usato l'operatore OFTYPE per restituire una raccolta di oggetti OnsiteCourse da una raccolta di oggetti Course. La query è basata sul [modello School](http://msdn.microsoft.com/it-it/859a9587-81ea-4a45-9bc0-f8d330e1adac).  
  
 [!code-csharp[DP EntityServices Concepts 2#OFTYPE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#oftype)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)