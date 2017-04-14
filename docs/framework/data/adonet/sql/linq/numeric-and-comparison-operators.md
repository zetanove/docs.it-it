---
title: "Operatori numerici e di confronto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 25b4a26a-06f2-4f80-87a9-76705ed46197
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Operatori numerici e di confronto
Gli operatori aritmetici e di confronto funzionano correttamente in Common Language Runtime \(CLR\), ad eccezione di quanto descritto di seguito:  
  
-   In SQL non è supportato l'operatore modulo per i numeri a virgola mobile.  
  
-   In SQL non è supportato l'operatore aritmetico unchecked.  
  
-   Gli operatori di incremento e decremento provocano effetti collaterali quando vengono usati in espressioni che non possono essere replicate in SQL e, di conseguenza, non sono supportati.  
  
## Operatori supportati  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sono supportati gli operatori riportati di seguito.  
  
-   Operatori aritmetici di base:  
  
    -   `+`  
  
    -   `-` \(sottrazione\)  
  
    -   `*`  
  
    -   `/`  
  
    -   Divisione con valori integer di Visual Basic \(`\`\)  
  
    -   `%` \(`Mod` di Visual Basic\)  
  
    -   `<<`  
  
    -   `>>`  
  
    -   `-` \(negazione unaria\)  
  
-   Operatori di confronto di base:  
  
    -   `=` di Visual Basic e `==` di C\#  
  
    -   `<>` di Visual Basic e `!=` di C\#  
  
    -   `Is/IsNot` Visual Basic  
  
    -   `<`  
  
    -   `<=`  
  
    -   `>`  
  
    -   `>=`  
  
## Vedere anche  
 [Tipi di dati e funzioni](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)   
 [Operatori](../Topic/C%23%20Operators.md)   
 [Operators](../Topic/Operators%20\(Visual%20Basic\).md)