---
title: Option Explicit Statement (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Explicit
- vb.OptionExplicit
dev_langs:
- VB
helpviewer_keywords:
- declaring variables, explicit
- forced variable declaration in Option Explicit statement
- Explicit keyword
- explicit variable declaration
- Option Explicit statement
ms.assetid: e82ac1ad-2cd3-49b2-b985-8bcf016f3fcc
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
ms.openlocfilehash: 020f12f1fbb9a06647215f1fac6324e3b74e8a77
ms.lasthandoff: 03/13/2017

---
# <a name="option-explicit-statement-visual-basic"></a>Istruzione Option Explicit (Visual Basic)
Forza la dichiarazione esplicita di tutte le variabili in un file o consente dichiarazioni implicite delle variabili.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Option Explicit { On | Off }  
```  
  
## <a name="parts"></a>Parti  
 `On`  
 Facoltativo. Consente di `Option Explicit` il controllo. Se `On` o `Off` non è specificato, il valore predefinito è `On`.  
  
 `Off`  
 Facoltativo. Disabilita `Option Explicit` il controllo.  
  
## <a name="remarks"></a>Note  
 Quando `Option Explicit On` o `Option Explicit` viene visualizzato in un file, è necessario dichiarare tutte le variabili in modo esplicito tramite il `Dim` o `ReDim` istruzioni. Se si tenta di utilizzare un nome di variabile non dichiarato, si verifica un errore in fase di compilazione. Il `Option Explicit Off` istruzione consente la dichiarazione implicita delle variabili.  
  
 Se usato, è necessario includere l'istruzione `Option Explicit` in un file prima di tutte le altre istruzioni del codice sorgente.  
  
> [!NOTE]
>  L'impostazione `Option Explicit` a `Off` non è in genere consigliabile. Impossibile digitato un nome di variabile in uno o più percorsi, che potrebbe provocare risultati imprevisti quando viene eseguito il programma.  
  
## <a name="when-an-option-explicit-statement-is-not-present"></a>Quando non è presente un'istruzione Option Explicit  
 Se il codice sorgente non contiene un `Option Explicit` istruzione, il **Option Explicit** impostazione per il [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic) viene utilizzato. Se viene utilizzato il compilatore della riga di comando, il [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md) viene utilizzata l'opzione del compilatore.  
  
#### <a name="to-set-option-explicit-in-the-ide"></a>Per impostare Option Explicit nell'IDE  
  
1.  In **Esplora**, selezionare un progetto. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Impostare il valore di **Option Explicit** casella.  
  
 Quando si crea un nuovo progetto, il **Option Explicit** impostazione per il **compilare** scheda è impostata sul **Option Explicit** impostazione nel **impostazioni predefinite di Visual Basic** la finestra di dialogo. Per accedere al **VB per impostazione predefinita** della finestra di dialogo di **strumenti** menu, fare clic su **opzioni**. Nel **opzioni** finestra di dialogo espandere **progetti e soluzioni**, quindi fare clic su **impostazioni predefinite di Visual Basic**. L'impostazione predefinita iniziale in **impostazioni predefinite di Visual Basic** è `On`.  
  
#### <a name="to-set-option-explicit-on-the-command-line"></a>Per impostare Option Explicit nella riga di comando  
  
-   Includere il [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md) opzione del compilatore di **vbc** comando.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `Option Explicit` istruzione per imporre la dichiarazione esplicita di tutte le variabili. Tentativo di utilizzare una variabile non dichiarata provoca un errore in fase di compilazione.  
  
 [!code-vb[VbVbalrStatements&#47;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-explicit-statement_1.vb)]  
  
 [!code-vb[VbVbalrStatements n.&48;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-explicit-statement_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [ReDim (istruzione)](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [Istruzione Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
