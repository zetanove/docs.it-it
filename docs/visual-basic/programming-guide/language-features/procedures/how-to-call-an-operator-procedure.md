---
title: "How to: Call an Operator Procedure (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "operator procedures, calling"
  - "procedures, operator"
  - "procedure calls, operator overloading"
  - "syntax, Operator procedures"
  - "operators [Visual Basic], overloading"
  - "return values, Operator procedures"
  - "overloaded operators, calling"
  - "operator overloading"
ms.assetid: 0dce42cc-f0b0-4c14-9f62-018b21f33497
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Call an Operator Procedure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per chiamare una routine con operatore, è possibile utilizzare il simbolo dell'operatore in un'espressione.  Nel caso di un operatore di conversione, è necessario chiamare la [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) che consente di convertire un valore da un tipo di dati a un altro.  
  
 Non è possibile chiamare le routine con operatore in modo esplicito.  È sufficiente utilizzare l'operatore o la funzione `CType` in un'espressione o un'istruzione di assegnazione, allo stesso modo in cui si utilizza normalmente un operatore.  La chiamata alla routine di operatore viene effettuata da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 La definizione di un operatore su una classe o una struttura viene anche detta *overload* dell'operatore.  
  
### Per chiamare una routine con operatore  
  
1.  Utilizzare normalmente il simbolo dell'operatore in un'espressione.  
  
2.  Accertarsi che i tipi di dati degli operandi siano appropriati per l'operatore e si trovino nell'ordine corretto.  
  
3.  L'operatore contribuirà al valore dell'espressione come previsto.  
  
### Per chiamare una routine con operatore di conversione  
  
1.  Utilizzare `CType` all'interno di un'espressione.  
  
2.  Accertarsi che i tipi di dati degli operandi siano appropriati per la conversione e si trovino nell'ordine corretto.  
  
3.  `CType` chiama la routine con operatore di conversione e restituisce il valore convertito.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono create due strutture <xref:System.TimeSpan> che vengono aggiunte insieme e i relativi risultati vengono memorizzati in una terza struttura <xref:System.TimeSpan>.  La struttura <xref:System.TimeSpan> definisce le routine con operatore per eseguire l'overload di diversi operatori standard.  
  
 [!code-vb[VbVbcnProcedures#29](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-call-an-operator-procedure_1.vb)]  
  
 Dal momento che <xref:System.TimeSpan> esegue l'overload dell'operatore standard `+`, nell'esempio precedente viene richiamata una routine di operatore quando si calcola il valore di `combinedSpan`.  
  
 Per un esempio di chiamata a una routine con operatore di conversione, vedere [How to: Use a Class that Defines Operators](../../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md).  
  
## Compilazione del codice  
 Accertarsi che la classe o la struttura attiva definisca l'operatore che si desidera utilizzare.  
  
## Vedere anche  
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [How to: Define an Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [How to: Define a Conversion Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [Operator Statement](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Widening](../../../../visual-basic/language-reference/modifiers/widening.md)   
 [Narrowing](../../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Structure Statement](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [How to: Declare a Structure](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Implicit and Explicit Conversions](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)