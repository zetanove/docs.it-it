---
title: "Valori letterali Null e inferenza dei tipi (Entity SQL) | Microsoft Docs"
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
ms.assetid: edd56afb-af1b-4e7d-b210-cb8998143426
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Valori letterali Null e inferenza dei tipi (Entity SQL)
I valori letterali null sono compatibili con qualsiasi tipo nel sistema di tipi [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  Per consentire, tuttavia, la corretta inferenza del tipo di un valore letterale null, in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] vengono imposti determinati vincoli sulle posizioni in cui è possibile usare un valore letterale null.  
  
## Valori null tipizzati  
 I valori null tipizzati possono essere usati in qualsiasi posizione.  L'inferenza dei tipi non è richiesta per i valori null tipizzati in quanto il tipo è noto.  È ad esempio possibile costruire un valore null di tipo Int16 con il costrutto [!INCLUDE[esql](../../../../../../includes/esql-md.md)] seguente:  
  
 `(cast(null as Int16))`  
  
## Valori letterali null mobili  
 I valori letterali null mobili possono essere usati nei contesti seguenti:  
  
-   Come argomento di un'espressione CAST o TREAT.  Questa è la modalità consigliata per produrre un'espressione null tipizzata.  
  
-   Come argomento di un metodo o di una funzione.  In questo caso si applicano le regole di overload standard.  
  
-   Come uno degli argomenti di un'espressione aritmetica, ad esempio \+, \- o \/.  Gli altri argomenti non possono essere valori letterali null. In caso contrario, l'inferenza dei tipi non è possibile.  
  
-   Come qualsiasi argomento di un'espressione logica \(AND, OR o NOT\).  Tutti gli argomenti sono noti come tipo Boolean.  
  
-   Come argomento di un'espressione IS NULL o IS NOT NULL.  
  
-   Come uno o più argomenti di un'espressione LIKE.  Per tutti gli argomenti è previsto il tipo String.  
  
-   Come uno o più argomenti di un costruttore di tipo denominato.  
  
-   Come uno o più argomenti di un costruttore multiset.  Almeno un argomento del costruttore multiset deve essere un'espressione non costituita da un valore letterale null.  
  
-   Come una o più espressioni THEN o ELSE in un'espressione CASE.  Almeno una delle espressioni THEN o ELSE nell'espressione CASE deve essere un'espressione diversa da un valore letterale null.  
  
 I valori letterali null mobili non possono essere usati in altri scenari.  Non possono ad esempio essere usati come argomenti di un costruttore ROW.  
  
## Vedere anche  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)