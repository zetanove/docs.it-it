---
title: Routine di operatore (Visual Basic) | Documenti di Microsoft
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
- Visual Basic code, procedures
- procedures, operator
- Visual Basic code, operators
- syntax, Operator procedures
- operators [Visual Basic], overloading
- overloaded operators
- operator overloading
- operator procedures
ms.assetid: 8c513d38-246b-4fb7-8b75-29e1364e555b
caps.latest.revision: 17
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
ms.openlocfilehash: a9e86c9c466ba236cc33153f2f341af35c622de6
ms.lasthandoff: 03/13/2017

---
# <a name="operator-procedures-visual-basic"></a>Routine di operatore (Visual Basic)
Una routine di operatore è una serie di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] le istruzioni che definiscono il comportamento di un operatore standard (ad esempio `*`, `<>`, o `And`) su una classe o una struttura definita. Detta anche *l'overload degli operatori*.  
  
## <a name="when-to-define-operator-procedures"></a>Quando definire una routine di operatore  
 Dopo aver definito una classe o struttura, è possibile dichiarare variabili di tipo di classe o struttura. A volte tale variabile deve far parte di un'operazione come parte di un'espressione. A tale scopo, deve essere un operando di un operatore.  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Definisce gli operatori solo sui tipi di dati più importanti. È possibile definire il comportamento di un operatore quando uno o entrambi gli operandi sono di tipo di classe o struttura.  
  
 Per ulteriori informazioni, vedere [Operator (istruzione)](../../../../visual-basic/language-reference/statements/operator-statement.md).  
  
## <a name="types-of-operator-procedure"></a>Tipi di routine di operatore  
 Una routine di operatore può essere uno dei seguenti tipi:  
  
-   Definizione di un operatore unario in cui l'argomento è del tipo di classe o struttura.  
  
-   Una definizione di un operatore binario in cui almeno uno degli argomenti è del tipo di classe o struttura.  
  
-   Definizione di un operatore di conversione in cui l'argomento è del tipo di classe o struttura.  
  
-   Definizione di un operatore di conversione che restituisce il tipo di classe o struttura.  
  
 Operatori di conversione sono sempre unari e utilizzare sempre `CType` come l'operatore che si sta definendo.  
  
## <a name="declaration-syntax"></a>Sintassi di dichiarazione  
 La sintassi per dichiarare una routine di operatore è come segue:  
  
 `Public Shared`   `[Widening | Narrowing]`   `Operator`  *operatorsymbol*  `(` *operand1*  `[,`  *operand2* `]) As`  *datatype*  
  
 `' Statements of the operator procedure.`  
  
 `End Operator`  
  
 Utilizzare il `Widening` o `Narrowing` parola chiave solo su un operatore di conversione del tipo. Il simbolo dell'operatore è sempre [funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) per un operatore di conversione di tipi.  
  
 Dichiarare due operandi per definire un operatore binario, e si dichiara un operando per definire un operatore unario, incluso un operatore di conversione del tipo. Tutti gli operandi devono essere dichiarati `ByVal`.  
  
 Dichiarare ogni operando esattamente alla dichiarazione dei parametri per [Sub (routine)](./sub-procedures.md).  
  
### <a name="data-type"></a>Tipo di dati  
 Poiché si sta definendo un operatore su una classe o una struttura definita, almeno uno degli operandi deve essere del tipo di dati di tale classe o struttura. Per un operatore di conversione di tipo, l'operando o il tipo restituito deve essere del tipo di dati della classe o struttura.  
  
 Per ulteriori informazioni, vedere [Operator (istruzione)](../../../../visual-basic/language-reference/statements/operator-statement.md).  
  
## <a name="calling-syntax"></a>Sintassi di chiamata  
 Richiamare una routine di operatore in modo implicito utilizzando il simbolo di operatore in un'espressione. Gli operandi vengono forniti il così come avviene per gli operatori predefiniti.  
  
 La sintassi per una chiamata implicita a una routine di operatore è come segue:  
  
 `Dim testStruct As`  *structurename*  
  
 `Dim testNewStruct As`  *structurename*`= testStruct`*operatorsymbol    *  `10`  
  
### <a name="illustration-of-declaration-and-call"></a>Illustrazione di dichiarazione e chiamata  
 La seguente struttura archivia un valore intero con segno a 128 bit come le parti costitutive in alto e basso. Definisce il `+` operatore per aggiungere due `veryLong` valori e generare una risultante `veryLong` valore.  
  
 [!code-vb[VbVbcnProcedures&#23;](./codesnippet/VisualBasic/operator-procedures_1.vb)]  
  
 Nell'esempio seguente viene illustrata una tipica chiamata per il `+` operatore definito in `veryLong`.  
  
 [!code-vb[VbVbcnProcedures&#24;](./codesnippet/VisualBasic/operator-procedures_2.vb)]  
  
 Per ulteriori informazioni ed esempi, vedere [overload degli operatori in Visual Basic 2005](http://go.microsoft.com/fwlink/?LinkId=101703).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Sub (routine)](./sub-procedures.md)   
 [Routine di funzione](./function-procedures.md)   
 [Proprietà (routine)](./property-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Operator (istruzione)](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Procedura: definire un operatore](./how-to-define-an-operator.md)   
 [Procedura: definire un operatore di conversione](./how-to-define-a-conversion-operator.md)   
 [Procedura: chiamare una routine di operatore](./how-to-call-an-operator-procedure.md)   
 [Procedura: Usare una classe che definisce gli operatori](./how-to-use-a-class-that-defines-operators.md)
