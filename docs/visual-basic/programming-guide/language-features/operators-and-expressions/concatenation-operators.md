---
title: Operatori di concatenazione in Visual Basic | Documenti di Microsoft
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
- '& operator [Visual Basic], concatenation'
- concatenation operators
- operators [Visual Basic], concatenation
- Visual Basic code, operators
- + operator [Visual Basic], concatenation
- concatenation operators, Visual Basic strings
ms.assetid: e59908c3-89e0-41ae-933d-3e8826c16a04
caps.latest.revision: 18
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: fa11f1dcff2c333861596cbac03391403cf962c1
ms.lasthandoff: 03/13/2017

---
# <a name="concatenation-operators-in-visual-basic"></a>Operatori di concatenazione in Visual Basic
Gli operatori di concatenazione consentono di unire più stringhe in un'unica stringa. Sono disponibili due operatori di concatenazione: `+` e `&`. Entrambi eseguono operazioni di concatenazione di base, come illustrato nell'esempio seguente.  
  
```vb
Dim x As String = "Mic" & "ro" & "soft" 
Dim y As String = "Mic" + "ro" + "soft" 
' The preceding statements set both x and y to "Microsoft".
```  
  
 Questi operatori possono concatenare anche variabili di tipo `String`, come nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators&#76;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/concatenation-operators_1.vb)]  
  
## <a name="differences-between-the-two-concatenation-operators"></a>Differenze tra i due operatori di concatenazione  
 Il [+ (operatore)](../../../../visual-basic/language-reference/operators/addition-operator.md) ha lo scopo principale di aggiunta di due numeri. Questo operatore consente però anche di concatenare operandi numerici con operandi stringa. Il `+` operatore include un insieme complesso di regole che determinano se aggiungere, concatenare, segnalare un errore del compilatore o generare in fase di esecuzione <xref:System.InvalidCastException>(eccezione).</xref:System.InvalidCastException>  
  
 Il [/ operatore](../../../../visual-basic/language-reference/operators/concatenation-operator.md) viene definito solo per `String` operandi e amplia sempre i propri operandi in `String`, indipendentemente dall'impostazione di `Option Strict`. L'operatore `&` rappresenta la scelta consigliata per la concatenazione delle stringhe poiché viene definito solo per le stringhe e riduce la possibilità di generare conversioni non intenzionali.  
  
## <a name="performance-string-and-stringbuilder"></a>Prestazioni: String e StringBuilder  
 Se si esegue un numero significativo di modifiche in una stringa, ad esempio concatenazioni, eliminazioni e sostituzioni, le prestazioni potrebbero profitto ottenuto la <xref:System.Text.StringBuilder>classe il <xref:System.Text>dello spazio dei nomi.</xref:System.Text> </xref:System.Text.StringBuilder> Accetta un'istruzione aggiuntiva per creare e inizializzare un <xref:System.Text.StringBuilder>oggetto e un'altra istruzione per convertire il valore finale per un `String`, ma sarà possibile recuperare il momento perché <xref:System.Text.StringBuilder>offre migliori prestazioni.</xref:System.Text.StringBuilder> </xref:System.Text.StringBuilder>  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Tipi di metodi di manipolazione delle stringhe in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/types-of-string-manipulation-methods.md)   
 [Operatori aritmetici in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Operatori di confronto in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Operatori logici e bit per bit in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
