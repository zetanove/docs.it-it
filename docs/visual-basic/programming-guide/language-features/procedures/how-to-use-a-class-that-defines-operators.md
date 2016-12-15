---
title: "How to: Use a Class that Defines Operators (Visual Basic) | Microsoft Docs"
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
  - "procedures, calling"
  - "examples [Visual Basic], CType"
  - "syntax, Operator procedures"
  - "operators [Visual Basic], overloading"
  - "return values, Operator procedures"
  - "operator overloading"
ms.assetid: 7ccce94a-6ca0-47d1-9f3f-13385d34f5d5
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Use a Class that Defines Operators (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Se si utilizza una classe o una struttura che definisce i propri operatori, è possibile accedere a questi ultimi da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 La definizione di un operatore su una classe o una struttura viene anche detta *overload* dell'operatore.  
  
## Esempio  
 Nell'esempio seguente si accede alla struttura SQL <xref:System.Data.SqlTypes.SqlString>, che definisce gli operatori di conversione \([Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md)\) in entrambe le direzioni tra una stringa SQL e una stringa [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  Utilizzare `CType(`*espressione stringa SQL*, `String)` per convertire una stringa SQL in una stringa di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] e `CType(`*espressione stringa Visual Basic*, <xref:System.Data.SqlTypes.SqlString>`)` per la conversione opposta.  
  
 [!code-vb[VbVbcnProcedures#30](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-use-a-class-that-defines-operators_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#31](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-use-a-class-that-defines-operators_2.vb)]  
  
 La struttura <xref:System.Data.SqlTypes.SqlString> definisce un operatore di conversione \([Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md)\) da `String` a <xref:System.Data.SqlTypes.SqlString> e un altro da <xref:System.Data.SqlTypes.SqlString> a `String`.  L'istruzione che assegna `title` a `jobTitle` utilizza il primo operatore, e la chiamata di funzione <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> utilizza il secondo.  
  
## Compilazione del codice  
 Accertarsi che la classe o la struttura attiva definisca l'operatore che si desidera utilizzare.  Non presupporre che nella classe o struttura siano stati definiti tutti gli operatori disponibili per l'overload.  Per un elenco di operatori disponibili, vedere [Operator Statement](../../../../visual-basic/language-reference/statements/operator-statement.md).  
  
 Includere l'istruzione `Imports` appropriata per la stringa SQL all'inizio del file di origine \(in questo caso <xref:System.Data.SqlTypes>\).  
  
 Il progetto deve includere riferimenti a System.Data e System.XML.  
  
## Vedere anche  
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [How to: Define an Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [How to: Define a Conversion Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [How to: Call an Operator Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [Widening](../../../../visual-basic/language-reference/modifiers/widening.md)   
 [Narrowing](../../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Structure Statement](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [How to: Declare a Structure](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Implicit and Explicit Conversions](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)