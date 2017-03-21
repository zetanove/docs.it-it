---
title: Tipi di dati costanti e letterali (Visual Basic) | Documenti di Microsoft
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
- declaring constants, literal data types
- data types [Visual Basic], declaring
- constants, declaring
- explicit declarations
- literals, coercing data type
- declarations, data types
ms.assetid: 057206d2-3a5b-40b9-b3af-57446f9b52fa
caps.latest.revision: 19
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
ms.openlocfilehash: 22ad31415ab560b7fd0180a6dadd6d2dcd7ec77a
ms.lasthandoff: 03/13/2017

---
# <a name="constant-and-literal-data-types-visual-basic"></a>Tipi di dati costanti e letterali (Visual Basic)
Un valore letterale è un valore che viene espresso come stesso anziché come valore della variabile o il risultato di un'espressione, ad esempio il numero 3 oppure la stringa "Hello". Una costante è un nome significativo che prende il posto di un valore letterale e mantiene lo stesso valore in tutto il programma, anziché una variabile, il cui valore può essere modificato.  
  
 Quando [Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md) è `Off` e [Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) è `On`, è necessario dichiarare tutte le costanti in modo esplicito con un tipo di dati. Nell'esempio seguente, il tipo di dati `MyByte` viene dichiarato esplicitamente come tipo di dati `Byte`:  
  
 [!code-vb[VbVbalrConstants n.&1;](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/constant-and-literal-data-types_1.vb)]  
  
 Quando `Option Infer` è `On` o `Option Strict` è `Off`, è possibile dichiarare una costante senza specificare un tipo di dati con un `As` clausola. Il compilatore determina il tipo della costante dal tipo dell'espressione. Viene eseguito il cast di un valore letterale integer numerico per impostazione predefinita per il `Integer` tipo di dati. Tipo di dati predefinito per numeri a virgola mobile sono `Double`e le parole chiave `True` e `False` specificare un `Boolean` costante.  
  
## <a name="literals-and-type-coercion"></a>Coercizione di tipi e valori letterali  
 In alcuni casi, potrebbe essere necessario forzare un valore letterale a un tipo di dati specifico. ad esempio, quando si assegna un valore letterale integrale particolarmente elevato a una variabile di tipo `Decimal`. Nell'esempio seguente genera un errore:  
  
```  
Dim myDecimal as Decimal  
myDecimal = 100000000000000000000   ' This causes a compiler error.  
```  
  
 L'errore deriva dalla rappresentazione del valore letterale. Il `Decimal` tipo di dati può contenere un valore così elevato, ma il valore letterale è rappresentato in modo implicito come una `Long`, che non può.  
  
 È possibile assegnare un valore letterale in un particolare tipo di dati in due modi: aggiungendovi un carattere di tipo o inserendolo all'interno di caratteri di contenimento. Un carattere di tipo caratteri di contenimento devono immediatamente precedere o seguire il valore letterale, senza spazi o caratteri di qualsiasi tipo.  
  
 Per correggere l'esempio precedente, è possibile aggiungere il `D` tipo di carattere per il valore letterale, in modo che essere rappresentato come un `Decimal`:  
  
 [!code-vb[VbVbalrConstants n.&2;](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/constant-and-literal-data-types_2.vb)]  
  
 Nell'esempio seguente viene illustrato l'uso corretto di caratteri di tipo e che lo contiene:  
  
 [!code-vb[VbVbalrConstants n.&3;](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/VisualBasic/constant-and-literal-data-types_3.vb)]  
  
 Nella tabella seguente, i caratteri di inclusione e tipo di caratteri disponibili in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
|Tipo di dati|Carattere di inclusione|Carattere di tipo aggiunto|  
|---|---|---|  
|`Boolean`|(nessuno)|(nessuno)|  
|`Byte`|(nessuno)|(nessuno)|  
|`Char`|"|C|  
|`Date`|#|(nessuno)|  
|`Decimal`|(nessuno)|D o @|  
|`Double`|(nessuno)|R o #|  
|`Integer`|(nessuno)|Non è o %|  
|`Long`|(nessuno)|L o /|  
|`Short`|(nessuno)|S|  
|`Single`|(nessuno)|F o!|  
|`String`|"|(nessuno)|  
  
## <a name="see-also"></a>Vedere anche  
 [Costanti definite dall'utente](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)   
 [Procedura: dichiarare una costante](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)   
 [Cenni preliminari sulle costanti](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [Istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Istruzione Option Explicit](../../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Cenni preliminari sulle enumerazioni](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [Procedura: dichiarare un'enumerazione](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [Qualifica di nomi ed enumerazioni](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Costanti ed enumerazioni](../../../../visual-basic/language-reference/constants-and-enumerations.md)
