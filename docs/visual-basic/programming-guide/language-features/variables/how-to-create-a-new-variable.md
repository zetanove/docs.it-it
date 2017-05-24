---
title: 'Procedura: creare una nuova variabile (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Dim statement
- variables [Visual Basic], creating
ms.assetid: 35300be3-77b0-4bef-a156-034d3cdedde0
caps.latest.revision: 29
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2856fe19ddc48a14385aaae7b1c331fcb96c0554
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-new-variable-visual-basic"></a>Procedura: creare una nuova variabile (Visual Basic)
Creare una variabile con un [Dim (istruzione)](../../../../visual-basic/language-reference/statements/dim-statement.md).  
  
### <a name="to-create-a-new-variable"></a>Per creare una nuova variabile  
  
1.  Dichiarare la variabile in un `Dim` istruzione.  
  
    ```  
    Dim newCustomer  
    ```  
  
2.  Includere specifiche per le caratteristiche della variabile, ad esempio [privata](../../../../visual-basic/language-reference/modifiers/private.md), [statico](../../../../visual-basic/language-reference/modifiers/static.md), [ombreggiature](../../../../visual-basic/language-reference/modifiers/shadows.md), o [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md). Per ulteriori informazioni, vedere [caratteristiche di elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md).  
  
    ```  
    Public Static newCustomer  
    ```  
  
     Non è necessario il `Dim` (parola chiave) se si utilizzano altre parole chiave nella dichiarazione.  
  
3.  Seguire le specifiche con il nome della variabile, che devono seguire [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] regole e convenzioni. Per ulteriori informazioni, vedere [nomi di elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
    ```  
    Public Static newCustomer  
    ```  
  
4.  Dopo il nome con il [come](../../../../visual-basic/language-reference/statements/as-clause.md) clausola per specificare il tipo di dati della variabile.  
  
    ```  
    Public Static newCustomer As Customer  
    ```  
  
     Se non si specifica il tipo di dati, viene utilizzato il valore predefinito: `Object`.  
  
5.  Seguire il `As` clausola con un segno di uguale (`=`) e seguire il segno di uguale valore iniziale della variabile.  
  
     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Assegna il valore specificato per la variabile ogni volta che viene eseguito il `Dim` istruzione. Se non si specifica un valore iniziale, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] assegna il valore iniziale predefinito per il tipo di dati della variabile quando la prima volta inserisce il codice che contiene il `Dim` istruzione.  
  
     Se la variabile è un tipo di riferimento, è possibile creare un'istanza della classe, includendo il [nuovo operatore](../../../../visual-basic/language-reference/operators/new-operator.md) (parola chiave) nei `As` clausola. Se non si utilizza `New`, il valore iniziale della variabile è [nulla](../../../../visual-basic/language-reference/nothing.md).  
  
    ```  
    Public Static newCustomer As New Customer  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Variabili](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Dichiarazione di variabile](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Nomi elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Caratteristiche di elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [Tipi di valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Istruzioni](../../../../visual-basic/language-reference/statements/index.md)   
 [Inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Istruzione Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md)

