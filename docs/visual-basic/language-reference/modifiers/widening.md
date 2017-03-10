---
title: "Widening (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.widening"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "conversions, type"
  - "type conversion"
  - "conversions, data type"
  - "Widening keyword"
  - "data type conversion"
ms.assetid: 646ae263-94d3-40a2-b0cc-64f619292f56
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Widening (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica che un operatore di conversione \(`CType`\) converte una classe o una struttura in un tipo che può contenere tutti i valori possibili della classe o della struttura originale.  
  
## Conversione con la parola chiave Widening  
 Nella routine di conversione è necessario specificare `Public Shared` oltre a `Widening`.  
  
 Le conversioni di ampliamento vengono sempre eseguite correttamente in fase di esecuzione e non comportano mai una perdita di dati.  Alcuni esempi sono le conversioni di un tipo `Single` in `Double`, di un tipo `Char` in `String` e di un tipo derivato nel relativo tipo base.  L'ultima conversione è verso un tipo di dati più grande in quanto il tipo derivato contiene tutti i membri del tipo base e pertanto rappresenta un'istanza di questo.  
  
 Il codice che la utilizza non deve includere `CType` per le conversioni verso un tipo di dati più grande, anche se `Option Strict` è `On`.  
  
 È possibile utilizzare la parola chiave `Widening` nel seguente contesto:  
  
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 Per definizioni di esempio di operatori di conversione di ampliamento e restrizione, vedere [How to: Define a Conversion Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md).  
  
## Vedere anche  
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [How to: Define an Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [Funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [How to: Define a Conversion Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)