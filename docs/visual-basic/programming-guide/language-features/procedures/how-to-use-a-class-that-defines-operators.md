---
title: 'Procedura: utilizzare una classe che definisce gli operatori (Visual Basic) | Documenti di Microsoft'
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
- procedures, calling
- examples [Visual Basic], CType
- syntax, Operator procedures
- operators [Visual Basic], overloading
- return values, Operator procedures
- operator overloading
ms.assetid: 7ccce94a-6ca0-47d1-9f3f-13385d34f5d5
caps.latest.revision: 21
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
ms.openlocfilehash: b1db7c0b2a6fd8160baa48892b5f2214df24674e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-use-a-class-that-defines-operators-visual-basic"></a>Procedura: utilizzare una classe che definisce gli operatori (Visual Basic)
Se si utilizza una classe o struttura che definisce i propri operatori, è possibile accedere a tali operatori da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 Definisce un operatore su una classe o struttura viene anche chiamato *overload* l'operatore.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente consente di accedere alla struttura SQL <xref:System.Data.SqlTypes.SqlString>, che definisce gli operatori di conversione ([funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md)) in entrambe le direzioni tra una stringa SQL e un [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] stringa.</xref:System.Data.SqlTypes.SqlString> Utilizzare `CType(` *espressione stringa SQL*, `String)` per convertire una stringa SQL a un [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] stringa, e `CType(` *espressione stringa Visual Basic*, <xref:System.Data.SqlTypes.SqlString> `)` da convertire in altra direzione.</xref:System.Data.SqlTypes.SqlString>  
  
 [!code-vb[&#30; VbVbcnProcedures](./codesnippet/VisualBasic/how-to-use-a-class-that-defines-operators_1.vb)]  
  
 [!code-vb[VbVbcnProcedures&#31;](./codesnippet/VisualBasic/how-to-use-a-class-that-defines-operators_2.vb)]  
  
 Il <xref:System.Data.SqlTypes.SqlString>struttura definisce un operatore di conversione ([CType (funzione)](../../../../visual-basic/language-reference/functions/ctype-function.md)) da `String` a <xref:System.Data.SqlTypes.SqlString>e un altro da <xref:System.Data.SqlTypes.SqlString>a `String`.</xref:System.Data.SqlTypes.SqlString> </xref:System.Data.SqlTypes.SqlString> </xref:System.Data.SqlTypes.SqlString> L'istruzione che assegna `title` a `jobTitle` utilizza il primo operatore e <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>chiamata di funzione utilizza il secondo.</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Assicurarsi che la classe o struttura in uso definisce l'operatore da utilizzare. Non presupporre che la classe o struttura è definita tutti gli operatori disponibili per eseguire l'overload. Per un elenco di operatori disponibili, vedere [Operator (istruzione)](../../../../visual-basic/language-reference/statements/operator-statement.md).  
  
 Includere l'appropriata `Imports` istruzione per la stringa SQL all'inizio del file di origine (in questo caso <xref:System.Data.SqlTypes>).</xref:System.Data.SqlTypes>  
  
 Il progetto deve disporre di riferimenti a System. Data e System. Xml.  
  
## <a name="see-also"></a>Vedere anche  
 [Routine di operatore](./operator-procedures.md)   
 [Procedura: definire un operatore](./how-to-define-an-operator.md)   
 [Procedura: definire un operatore di conversione](./how-to-define-a-conversion-operator.md)   
 [Procedura: chiamare una routine di operatore](./how-to-call-an-operator-procedure.md)   
 [Ampliamento](../../../../visual-basic/language-reference/modifiers/widening.md)   
 [Restrizione](../../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Istruzione Structure](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Procedura: dichiarare una struttura](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Conversioni implicite ed esplicite](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Conversioni di ampliamento e restrizione](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
