---
title: Istruzione Option Infer | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.OptionInfer
- vb.Infer
dev_langs:
- VB
helpviewer_keywords:
- variables [Visual Basic], declaring
- Option Infer statement
- Infer keyword
- declaring variables, inferred
- inferred variable declaration
ms.assetid: 4ad3e6e9-8f5b-4209-a248-de22ef6e4652
caps.latest.revision: 72
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
ms.openlocfilehash: e6074ad44b94c80f275af562edef2dcd1173c0c3
ms.lasthandoff: 03/13/2017

---
# <a name="option-infer-statement"></a>Option Infer (istruzione)
Abilita l'uso dell'inferenza del tipo di variabile locale nelle variabili dichiaranti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Option Infer { On | Off }  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`On`|Parametro facoltativo. Abilita l'inferenza del tipo di variabile locale.|  
|`Off`|Parametro facoltativo. Disabilita l'inferenza del tipo di variabile locale.|  
  
## <a name="remarks"></a>Note  
 Per impostare `Option Infer` in un file, digitare `Option Infer On` oppure `Option Infer Off` all'inizio del file, prima di qualsiasi altro codice sorgente. Se il valore impostato per `Option Infer` in un file è in conflitto con il valore impostato nell'IDE o sulla riga di comando, il valore nel file ha precedenza.  
  
 Quando si imposta `Option Infer` su `On`, è possibile dichiarare variabili locali senza dichiarare in modo esplicito un tipo di dati. Tramite l'inferenza, il compilatore deriva il tipo di dati di una variabile dal tipo della relativa espressione di inizializzazione.  
  
 Nella figura seguente, l'istruzione `Option Infer` è abilitata. La variabile nella dichiarazione `Dim someVar = 2` viene dichiarata come Integer in base all'inferenza del tipo.  
  
 ![Visualizzazione IntelliSense della dichiarazione.](../../../visual-basic/language-reference/statements/media/optioninferasinteger.png "optionInferAsInteger")  
IntelliSense quando Option Infer è attivato  
  
 Nella figura seguente, l'istruzione `Option Infer` è disabilitata. La variabile nella dichiarazione `Dim someVar = 2` viene dichiarata come `Object` in base all'inferenza del tipo. In questo esempio, il **Option Strict** è impostata su **Off** sul [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic).  
  
 ![Visualizzazione IntelliSense della dichiarazione.](../../../visual-basic/language-reference/statements/media/optioninferasobject.png "optionInferAsObject")  
IntelliSense quando Option Infer è disabilitato  
  
> [!NOTE]
>  Quando una variabile viene dichiarata come `Object`, il tipo di runtime può essere modificato mentre il programma è in esecuzione. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]esegue operazioni chiamate *boxing* e *unboxing* per la conversione tra un `Object` e un tipo di valore, che rende l'esecuzione più lenta. Per informazioni sulle conversioni boxing e unboxing, vedere il [specifiche del linguaggio Visual Basic](../../../visual-basic/reference/language-specification.md).  
  
 L'inferenza del tipo si applica a livello di routine e non si applica all'esterno di una routine in una classe, una struttura, un modulo o un'interfaccia.  
  
 Per ulteriori informazioni, vedere [l'inferenza del tipo locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
## <a name="when-an-option-infer-statement-is-not-present"></a>Quando non è presente un'istruzione Option Infer  
 Se il codice sorgente non contiene un `Option Infer` istruzione, il **Option Infer** impostazione per il [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic) viene utilizzato. Se viene utilizzato il compilatore della riga di comando, il [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md) viene utilizzata l'opzione del compilatore.  
  
#### <a name="to-set-option-infer-in-the-ide"></a>Per impostare Option Infer nell'IDE  
  
1.  In **Esplora**, selezionare un progetto. Nel **progetto** menu, fare clic su **proprietà**. Per ulteriori informazioni, vedere [NIB: gestione di proprietà del progetto con Progettazione progetti](http://msdn.microsoft.com/en-us/983f3c18-832f-4666-afec-74b716ff3e0e).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Impostare il valore di **Option infer** casella.  
  
 Quando si crea un nuovo progetto, il **Option Infer** impostazione per il **compilare** scheda è impostata sul **Option Infer** impostazione nel **impostazioni predefinite di Visual Basic** la finestra di dialogo. Per accedere al **VB per impostazione predefinita** della finestra di dialogo di **strumenti** menu, fare clic su **opzioni**. Nel **opzioni** finestra di dialogo espandere **progetti e soluzioni**, quindi fare clic su **impostazioni predefinite di Visual Basic**. L'impostazione predefinita iniziale in **impostazioni predefinite di Visual Basic** è `On`.  
  
#### <a name="to-set-option-infer-on-the-command-line"></a>Per impostare Option Infer nella riga di comando  
  
-   Includere il [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md) opzione del compilatore di **vbc** comando.  
  
## <a name="default-data-types-and-values"></a>Tipi di dati e valori predefiniti  
 Nella tabella seguente vengono descritti i risultati di varie combinazioni della specifica del tipo di dati e dell'inizializzatore in un'istruzione `Dim`.  
  
|Tipo di dati specificato?|Inizializzatore specificato?|Esempio|Risultato|  
|---|---|---|---|  
|No|No|`Dim qty`|Se `Option Strict` è disabilitato (impostazione predefinita), la variabile è impostata su `Nothing`.<br /><br /> Se `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|No|Sì|`Dim qty = 5`|Se `Option Infer` è abilitato (impostazione predefinita), alla variabile viene assegnato il tipo di dati dell'inizializzatore. Vedere [inferenza del tipo locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).<br /><br /> Se le istruzioni `Option Infer` e `Option Strict` sono disabilitate, il tipo di dati accettato dalla variabile è `Object`.<br /><br /> Se `Option Infer` è disabilitato e `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|Sì|No|`Dim qty As Integer`|La variabile viene inizializzata sul valore predefinito per il tipo di dati. Per ulteriori informazioni, vedere [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md).|  
|Sì|Sì|`Dim qty  As Integer = 5`|Se il tipo di dati dell'inizializzatore non è convertibile nel tipo di dati specificato, si verifica un errore in fase di compilazione.|  
  
## <a name="example"></a>Esempio  
 Gli esempi seguenti illustrano come l'istruzione `Option Infer` permette di usare inferenza del tipo di variabile locale.  
  
 [!code-vb[6 VbVbalrTypeInference](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/option-infer-statement_1.vb)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente dimostra che il tipo di runtime può differire quando una variabile viene identificata come `Object`.  
  
 [!code-vb[VbVbalrTypeInference&#11;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/option-infer-statement_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Inferenza del tipo locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Istruzione Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Finestra di dialogo Opzioni predefinite, progetti, Visual Basic](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)   
 [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Boxing e unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)
