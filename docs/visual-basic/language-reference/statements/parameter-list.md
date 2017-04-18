---
title: Elenco di parametri (Visual Basic) | Documenti di Microsoft
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
- parameters, Visual Basic
- parameters, lists
- parameter lists
- Visual Basic code, parameter lists
- arguments [Visual Basic], Visual Basic
- procedures, parameter lists
ms.assetid: 5d737319-0c34-4df9-a23d-188fc840becd
caps.latest.revision: 19
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
ms.openlocfilehash: abadaa8e035bfa4c92acc30ab633d6a7e958676c
ms.lasthandoff: 03/13/2017

---
# <a name="parameter-list-visual-basic"></a>Elenco dei parametri (Visual Basic)
Specifica i parametri di che una procedura prevede quando viene chiamato. Più parametri sono separati da virgole. Di seguito è la sintassi per un parametro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ <attributelist> ] [ Optional ] [{ ByVal | ByRef }] [ ParamArray ]   
parametername[( )] [ As parametertype ] [ = defaultvalue ]  
```  
  
## <a name="parts"></a>Parti  
 `attributelist`  
 Facoltativo. Elenco di attributi che si applicano a questo parametro. È necessario racchiudere il [elenco attributi](../../../visual-basic/language-reference/statements/attribute-list.md) parentesi angolari ("`<`"e"`>`").  
  
 `Optional`  
 Facoltativo. Specifica che questo parametro non è necessario quando viene chiamata la routine.  
  
 `ByVal`  
 Facoltativo. Specifica che la procedura non possa sostituire o riassegnare l'elemento variabile sottostante all'argomento corrispondente nel codice chiamante.  
  
 `ByRef`  
 Facoltativo. Specifica che la routine può modificare l'elemento variabile sottostante nel codice chiamante allo stesso modo che il codice.  
  
 `ParamArray`  
 Facoltativo. Specifica che l'ultimo parametro nell'elenco dei parametri è una matrice facoltativa di elementi del tipo di dati specificato. In questo modo il codice chiamante di passare un numero arbitrario di argomenti per la procedura.  
  
 `parametername`  
 Obbligatorio. Nome della variabile locale che rappresenta il parametro.  
  
 `parametertype`  
 Obbligatorio se `Option Strict` è `On`. Tipo di dati della variabile locale che rappresenta il parametro.  
  
 `defaultvalue`  
 Necessario per `Optional` i parametri. Qualsiasi espressione costante o una costante che restituisce il tipo di dati del parametro. Se il tipo è `Object`, o una classe, interfaccia, una matrice o una struttura, il valore predefinito può essere solo `Nothing`.  
  
## <a name="remarks"></a>Note  
 I parametri sono racchiusi tra parentesi e separati da virgole. Un parametro può essere dichiarato con qualsiasi tipo di dati. Se non si specifica `parametertype`, l'impostazione predefinita è `Object`.  
  
 Quando si chiama la procedura, il codice chiamante passa un *argomento* per ogni parametro obbligatorio. Per ulteriori informazioni, vedere [le differenze tra parametri e argomenti](../../../visual-basic/programming-guide/language-features/procedures/differences-between-parameters-and-arguments.md).  
  
 L'argomento che il codice chiamante passa a ogni parametro è un puntatore a un elemento sottostante nel codice chiamante. Se questo elemento è *variabile* (una costante, valore letterale, enumerazione o espressione), è Impossibile per il codice per modificarlo. In questo caso un *variabile* elemento (una variabile dichiarata, campo, proprietà, matrice o elemento di struttura), il codice chiamante può modificarlo. Per ulteriori informazioni, vedere [le differenze tra modificabile e non modificabili argomenti](../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md).  
  
 Se viene passato un elemento variabile `ByRef`, la routine può modificare anche. Per ulteriori informazioni, vedere [le differenze tra il passaggio di un argomento per valore e per riferimento](../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md).  
  
## <a name="rules"></a>Regole  
  
-   **Parentesi.** Se si specifica un elenco di parametri, è necessario racchiuderlo tra parentesi. Se non sono presenti parametri, è comunque possibile utilizzare parentesi che racchiudono un elenco vuoto. Per migliorare la leggibilità del codice indicando che l'elemento è una procedura.  
  
-   **Parametri facoltativi.** Se si utilizza il `Optional` modificatore su un parametro, tutti i parametri successivi nell'elenco deve inoltre essere facoltativi ed essere dichiarati utilizzando il `Optional` modificatore.  
  
     Ogni dichiarazione di parametro facoltativo è necessario fornire il `defaultvalue` clausola.  
  
     Per ulteriori informazioni, vedere [parametri facoltativi](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md).  
  
-   **Matrici di parametri.** È necessario specificare `ByVal` per un `ParamArray` parametro.  
  
     È possibile utilizzare sia `Optional` e `ParamArray` nello stesso elenco di parametri.  
  
     Per ulteriori informazioni, vedere [matrici di parametro](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md).  
  
-   **Meccanismo di passaggio.** Il meccanismo predefinito per ogni argomento è `ByVal`, ovvero la procedura non può modificare l'elemento variabile sottostante. Tuttavia, se l'elemento è un tipo di riferimento, la routine può modificare il contenuto o i membri dell'oggetto sottostante, anche se è possibile sostituire o riassegnare l'oggetto stesso.  
  
-   **Nomi dei parametri.** Se il tipo di dati del parametro è una matrice, seguire `parametername` parentesi immediatamente. Per ulteriori informazioni sui nomi dei parametri, vedere [nomi di elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente un `Function` routine che definisce due parametri.  
  
 [!code-vb[VbVbalrStatements n.&2;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/parameter-list_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.InteropServices.DllImportAttribute></xref:System.Runtime.InteropServices.DllImportAttribute>   
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub (istruzione)](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Declare (istruzione)](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Cenni preliminari sugli attributi](../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
