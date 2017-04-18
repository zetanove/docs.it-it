---
title: 'Procedura: chiamare una routine di operatore (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- operator procedures, calling
- procedures, operator
- procedure calls, operator overloading
- syntax, Operator procedures
- operators [Visual Basic], overloading
- return values, Operator procedures
- overloaded operators, calling
- operator overloading
ms.assetid: 0dce42cc-f0b0-4c14-9f62-018b21f33497
caps.latest.revision: 16
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2403e7a8270c17a8db5417cd8394fd47c373d493
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-an-operator-procedure-visual-basic"></a>Procedura: chiamare una routine di operatore (Visual Basic)
Chiamare una routine di operatore utilizzando il simbolo di operatore in un'espressione. Nel caso di un operatore di conversione, si chiama il [funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) per convertire un valore da un tipo a altro.  
  
 Non è necessario chiamare routine di operatore in modo esplicito. È sufficiente utilizzare l'operatore o `CType` funzione in un'istruzione di assegnazione o un'espressione, diverso da quello in cui si utilizza normalmente un operatore. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]effettua la chiamata alla routine di operatore.  
  
 Definisce un operatore su una classe o struttura viene anche chiamato *overload* l'operatore.  
  
### <a name="to-call-an-operator-procedure"></a>Per chiamare una routine di operatore  
  
1.  Utilizzare il simbolo di operatore in un'espressione in modo normale.  
  
2.  Verificare che i tipi di dati degli operandi siano appropriati per l'operatore e nell'ordine corretto.  
  
3.  L'operatore contribuisce al valore dell'espressione come previsto.  
  
### <a name="to-call-a-conversion-operator-procedure"></a>Per chiamare una routine di operatore di conversione  
  
1.  Utilizzare `CType` all'interno di un'espressione.  
  
2.  Verificare che i tipi di dati degli operandi siano appropriati per la conversione e nell'ordine corretto.  
  
3.  `CType`chiama la routine di operatore di conversione e restituisce il valore convertito.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono create due <xref:System.TimeSpan>strutture, li somma e archivia il risultato in un terzo <xref:System.TimeSpan>struttura.</xref:System.TimeSpan> </xref:System.TimeSpan> Il <xref:System.TimeSpan>struttura definisce le routine di operatore per eseguire l'overload di diversi operatori standard.</xref:System.TimeSpan>  
  
 [!code-vb[VbVbcnProcedures&#29;](./codesnippet/VisualBasic/how-to-call-an-operator-procedure_1.vb)]  
  
 Poiché <xref:System.TimeSpan>overload standard `+` operatore, nell'esempio precedente chiama una routine di operatore quando si calcola il valore di `combinedSpan`.</xref:System.TimeSpan>  
  
 Per un esempio di chiamata una routine di operatore di conversione, vedere [procedura: utilizzare una classe che definisce operatori](./how-to-use-a-class-that-defines-operators.md).  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Assicurarsi che la classe o struttura in uso definisce l'operatore da utilizzare.  
  
## <a name="see-also"></a>Vedere anche  
 [Routine di operatore](./operator-procedures.md)   
 [Procedura: definire un operatore](./how-to-define-an-operator.md)   
 [Procedura: definire un operatore di conversione](./how-to-define-a-conversion-operator.md)   
 [Operator (istruzione)](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Ampliamento](../../../../visual-basic/language-reference/modifiers/widening.md)   
 [Restrizione](../../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Istruzione Structure](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Procedura: dichiarare una struttura](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Conversioni implicite ed esplicite](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Conversioni di ampliamento e restrizione](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
