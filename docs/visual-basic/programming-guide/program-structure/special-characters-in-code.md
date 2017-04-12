---
title: Caratteri speciali nel codice (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.)
- vb.(
- vb.colon
- vb.!
- vb..
- 'vb.:'
dev_langs:
- VB
helpviewer_keywords:
- special characters, in code
- parentheses, using in code
- colons (:)
- period character in code
- dot operator (.)
- dictionary access operator
- concatenation operators, special characters in code
- concatenation operators, vs. addition operator
- '! operator'
- separators, using in code
- operators [Visual Basic], dictionary access
- ': separator character'
- member access operator
- addition operator
- operators [Visual Basic], member access
- . operator
- exclamation points
- separators
- exclamation point operator (!)
- Visual Basic code, special characters
ms.assetid: 310dce0c-45b5-4e0d-83e9-32df258d2a3e
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
ms.openlocfilehash: 6d4b6e74ef3dfab3a7174da07cff7100fa4b2a2f
ms.lasthandoff: 03/13/2017

---
# <a name="special-characters-in-code-visual-basic"></a>Caratteri speciali nel codice (Visual Basic)
Talvolta è necessario utilizzare caratteri speciali nel codice, vale a dire caratteri non alfabetici o numerici. La punteggiatura e caratteri speciali di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] set di caratteri sono diversi utilizzi, dall'organizzazione del testo di programma alla definizione di attività eseguite dal compilatore o dal programma compilato. Questi caratteri non specificano l'esecuzione di un'operazione.  
  
## <a name="parentheses"></a>Tra parentesi  
 Utilizzare le parentesi quando si definisce una routine, ad esempio un `Sub` o `Function`. Tutti gli elenchi di argomenti di routine è necessario racchiudere tra parentesi. È inoltre utilizzare parentesi per raggruppare variabili o argomenti in gruppi logici, in particolare per ignorare l'ordine di precedenza tra operatori in un'espressione complessa predefinito. Questa condizione è illustrata nell'esempio seguente.  
  
 [!code-vb[VbVbcnConventions&#11;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_1.vb)]  
  
 Dopo l'esecuzione del codice precedente, il valore di `d` è 8,225 e il valore di `e` è 3. Il calcolo per `d` utilizza la precedenza predefinita di `/` su `+` ed equivale a `d = b + (c / a)`. Le parentesi nel calcolo del `e` ignorare l'ordine predefinito.  
  
## <a name="separators"></a>Separatori  
 Separatori si cosa suggerisce il nome stesso: consentono di separare le sezioni di codice. In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], il carattere separatore sia i due punti (`:`). Utilizzare i separatori quando si desidera includere più istruzioni in una singola riga anziché righe separate. Questo consente di risparmiare spazio e migliora la leggibilità del codice. Nell'esempio seguente mostra tre istruzioni separate da virgola.  
  
 [!code-vb[VbVbcnConventions&#12;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_2.vb)]  
  
 Per ulteriori informazioni, vedere [How to: Break e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md).  
  
 I due punti (`:`) carattere viene utilizzato anche per identificare un'etichetta dell'istruzione. Per ulteriori informazioni, vedere [How to: Label Statements](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md).  
  
## <a name="concatenation"></a>Concatenazione  
 Utilizzare il `&` operatore per *concatenazione*, o il collegamento di più stringhe. Non confondere con il `+` operatore, che vengono sommati i valori numerici. Se si utilizza il `+` per concatenare quando si opera su valori numerici, è possibile ottenere risultati non corretti. Nell'esempio che segue viene illustrato quanto descritto.  
  
 [!code-vb[13 VbVbcnConventions](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_3.vb)]  
  
 Dopo l'esecuzione del codice precedente, il valore di `resultA` è 21,01 e il valore di `resultB` è "10,0111".  
  
## <a name="member-access-operators"></a>Operatori di accesso ai membri  
 Per accedere a un membro di un tipo, utilizzare il punto (`.`) o punto esclamativo (`!`) (operatore) tra il nome del tipo e il nome del membro.  
  
### <a name="dot--operator"></a>Punto (.) Operatore  
 Utilizzare il `.` operatore su una classe, struttura, interfaccia o enumerazione come un operatore di accesso ai membri. Il membro può essere un campo, proprietà, evento o metodo. Questa condizione è illustrata nell'esempio seguente.  
  
 [!code-vb[VbVbcnConventions&#14;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_4.vb)]  
  
### <a name="exclamation-point--operator"></a>Punto esclamativo (!) Operatore  
 Utilizzare il `!` operatore solo in una classe o interfaccia come operatore di accesso al dizionario. La classe o interfaccia deve avere una proprietà predefinita che accetta un singolo `String` argomento. Identificatore che segue immediatamente il `!` diventa il valore dell'argomento passato alla proprietà predefinito come stringa. Nell'esempio che segue viene illustrato quanto descritto.  
  
 [!code-vb[VbVbcnConventions&#15;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/special-characters-in-code_5.vb)]  
  
 Le tre righe di output `MsgBox` tutte visualizzate con il valore `32856`. La prima riga utilizza l'accesso tradizionale alla proprietà `index`, il secondo si avvale del fatto che `index` la proprietà predefinita della classe `hasDefault`, e la terza utilizza l'accesso al dizionario alla classe.  
  
 Si noti che il secondo operando il `!` operatore deve essere un identificatore valido di Visual Basic non è racchiuso tra virgolette doppie (`" "`). In altre parole, è possibile utilizzare un valore letterale stringa o una variabile di stringa. La modifica seguente all'ultima riga del `MsgBox` chiamata genera un errore perché `"X"` è una stringa letterale racchiusa.  
  
 `"Dictionary access returns " & hD!"X")`  
  
> [!NOTE]
>  I riferimenti alle raccolte predefinite devono essere espliciti. In particolare, non è possibile utilizzare il `!` operatore su una variabile ad associazione tardiva.  
  
 Il `!` carattere viene utilizzato anche come il `Single` tipo di carattere.  
  
## <a name="see-also"></a>Vedere anche  
 [Struttura del programma e convenzioni del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Caratteri tipo](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
