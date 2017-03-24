---
title: "Narrowing (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.narrowing"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "conversions, type"
  - "type conversion"
  - "conversions, data type"
  - "Narrowing keyword"
  - "data type conversion"
ms.assetid: a207ee91-aca4-4771-b4e2-713f029bf2bb
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Narrowing (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica che un operatore di conversione \(`CType`\) converte una classe o una struttura in un tipo che potrebbe non contenere alcuni dei possibili valori della classe o della struttura originale.  
  
## Conversione con la parola chiave Narrowing  
 Nella routine di conversione è necessario specificare `Public Shared` oltre a `Narrowing`.  
  
 Le conversioni di restrizione non vengono sempre eseguite correttamente in fase di esecuzione e possono causare una perdita di dati.  Alcuni esempi sono le conversioni di `Long` in `Integer`, di `String` in `Date` e di un tipo base in un tipo derivato.  L'ultima conversione viene eseguita verso un tipo di dati più piccolo poiché il tipo base potrebbe non contenere tutti i membri del tipo derivato e pertanto non rappresentare un'istanza di quest'ultimo.  
  
 Se `Option Strict` è `On`, il codice utilizzato dovrà impiegare `CType` per tutte le conversioni verso un tipo di dati più piccolo.  
  
 È possibile utilizzare la parola chiave `Narrowing` nel seguente contesto:  
  
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
## Vedere anche  
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Widening](../../../visual-basic/language-reference/modifiers/widening.md)   
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [How to: Define an Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [Funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)