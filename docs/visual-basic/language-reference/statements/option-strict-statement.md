---
title: Option Strict (istruzione) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Strict
- vb.OptionStrict
dev_langs:
- VB
helpviewer_keywords:
- Strict keyword
- Option Strict statement
- conversions, implicit
- late binding
- implicit conversions
ms.assetid: 5883e0c1-a920-4274-8e46-b0ff047eaee5
caps.latest.revision: 49
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
ms.openlocfilehash: 3bf0d4939f24c38392d7ca4764c41d12366067b5
ms.lasthandoff: 03/13/2017

---
# <a name="option-strict-statement"></a>Option Strict Statement
Limita le conversioni di tipo dati implicita in solo conversioni di ampliamento, non consente l'associazione tardiva e la tipizzazione implicita che comporta un `Object` tipo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Option Strict { On | Off }  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`On`|Facoltativo. Consente di `Option Strict` il controllo.|  
|`Off`|Facoltativo. Disabilita `Option Strict` il controllo.|  
  
## <a name="remarks"></a>Note  
 Quando `Option Strict On` o `Option Strict` viene visualizzato in un file, le condizioni seguenti generano un errore in fase di compilazione:  
  
-   Le conversioni implicite  
  
-   Associazione tardiva  
  
-   La tipizzazione implicita che comporta un `Object` tipo  
  
> [!NOTE]
>  Nelle configurazioni di avviso che è possibile impostare per il [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic), sono disponibili tre impostazioni che corrispondono alle tre condizioni che causano un errore in fase di compilazione. Per informazioni su come utilizzare queste impostazioni, vedere [per impostare le configurazioni di avviso nell'IDE](../../../visual-basic/language-reference/statements/option-strict-statement.md#conditions) più avanti in questo argomento.  
  
 Il `Option Strict Off` istruzione disattiva l'errore e avviso di controllo per tutte e tre le condizioni, anche se le impostazioni IDE associate specificano per attivare questi errori o avvisi. Il `Option Strict On` istruzione attiva errore e avviso di controllo per tutte e tre le condizioni, anche se le impostazioni IDE associate specificano per disattivare questi errori o avvisi.  
  
 Se utilizzato, il `Option Strict` istruzione deve essere visualizzato prima di qualsiasi altra istruzione di codice in un file.  
  
 Quando si imposta `Option Strict` a `On`, Visual Basic controlla che i tipi di dati vengono specificati per tutti gli elementi di programmazione. Tipi di dati possono essere specificati in modo esplicito o specificati tramite l'inferenza del tipo locale. Specifica di tipi di dati per tutti gli elementi di programmazione è consigliata, per i motivi seguenti:  
  
-   Consente il supporto IntelliSense per le variabili e parametri. In questo modo è possibile visualizzare le relative proprietà e gli altri membri durante la digitazione di codice.  
  
-   Consente al compilatore di eseguire il controllo dei tipi. Controllo dei tipi consente di trovare istruzioni possono avere esito negativo in fase di esecuzione a causa di errori di conversione. Inoltre, identifica le chiamate ai metodi su oggetti che non supportano tali metodi.  
  
-   Accelera l'esecuzione di codice. Una ragione è che se non si specifica un tipo di dati per un elemento di programmazione, il compilatore Visual Basic assegna il `Object` tipo. Codice compilato potrebbe essere necessario convertire avanti e indietro tra `Object` e altri tipi di dati, riducendo le prestazioni.  
  
## <a name="implicit-narrowing-conversion-errors"></a>Errori di conversione di Narrowing implicite  
 Errori di conversione di narrowing implicite si verificano quando esiste una conversione implicita dei dati tipo di conversione.  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]convertire molti tipi di dati in altri tipi di dati. Quando il valore di un tipo di dati viene convertito in un tipo di dati che dispone di una capacità inferiore o meno preciso, può verificarsi una perdita di dati. Se tale conversione non riesce, verrà generato un errore in fase di esecuzione. `Option Strict`garantisce la notifica in fase di compilazione di queste conversioni di restrizione in modo che possano essere evitate. Per ulteriori informazioni, vedere [conversioni implicite ed esplicite](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md) e [conversioni di ampliamento e restrizione](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
 Le conversioni che possono causare errori includono conversioni implicite che si verificano nelle espressioni. Per altre informazioni, vedere i seguenti argomenti:  
  
-   [Operatore +](../../../visual-basic/language-reference/operators/addition-operator.md)  
  
-   [Operatore +=](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)  
  
-   [\ Operatore (Visual Basic)](../../../visual-basic/language-reference/operators/integer-division-operator.md)  
  
-   [Operatore / = (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)  
  
-   [Tipo di dati Char](../../../visual-basic/language-reference/data-types/char-data-type.md)  
  
 Quando si concatenano stringhe tramite il [/ operatore](../../../visual-basic/language-reference/operators/concatenation-operator.md), tutte le conversioni per le stringhe sono considerate di ampliamento. Affinché queste conversioni non generano un errore di conversione narrowing implicite, anche se `Option Strict` è su.  
  
 Quando si chiama un metodo che dispone di un argomento con un tipo di dati diverso dal parametro corrispondente, una conversione di narrowing causa un errore in fase di compilazione se `Option Strict` è su. È possibile evitare l'errore in fase di compilazione tramite una conversione di ampliamento o una conversione esplicita.  
  
 Errori di conversione di narrowing implicite vengono soppressi in fase di compilazione per le conversioni da elementi di un `For Each…Next` insieme alla variabile di controllo del ciclo. Questo errore si verifica anche se `Option Strict` è su. Per ulteriori informazioni, vedere la sezione "Conversioni di restrizione" [For Each... Istruzione successiva](../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
## <a name="late-binding-errors"></a>Errori di associazione tardiva  
 Un oggetto viene associato tardivamente quando viene assegnato a una proprietà o metodo di una variabile dichiarata di tipo `Object`. Per ulteriori informazioni, vedere [anticipato e l'associazione tardiva](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md).  
  
## <a name="implicit-object-type-errors"></a>Errori di tipo di oggetto implicito  
 Se non può essere un tipo appropriato si verificano errori di tipo di oggetto implicito inferito per una variabile dichiarata, pertanto, un tipo di `Object` viene dedotto. Ciò si verifica principalmente quando si utilizza un `Dim` istruzione per dichiarare una variabile senza utilizzare un `As` clausola e `Option Infer` è disattivata. Per ulteriori informazioni, vedere [Option Infer Statement](../../../visual-basic/language-reference/statements/option-infer-statement.md) e [specifiche del linguaggio Visual Basic](../../../visual-basic/reference/language-specification.md).  
  
 Per i parametri di metodo, il `As` clausola è facoltativa se `Option Strict` è disattivata. Tuttavia, se un qualsiasi parametro utilizza un `As` clausola tutti deve essere utilizzata. Se `Option Strict` è abilitato, il `As` clausola è obbligatoria per ogni definizione di parametro.  
  
 Se si dichiara una variabile senza utilizzare un `As` clausola e impostarlo su `Nothing`, la variabile di tipo `Object`. In questo caso verrà generato alcun errore in fase di compilazione quando `Option Strict` è e `Option Infer` si trova in. Un esempio è `Dim something = Nothing`.  
  
### <a name="default-data-types-and-values"></a>Tipi di dati e valori predefiniti  
 Nella tabella seguente vengono descritti i risultati di varie combinazioni della specifica del tipo di dati e dell'inizializzatore in un [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md).  
  
|Tipo di dati specificato?|Inizializzatore specificato?|Esempio|Risultato|  
|---|---|---|---|  
|No|No|`Dim qty`|Se `Option Strict` è disabilitato (impostazione predefinita), la variabile è impostata su `Nothing`.<br /><br /> Se `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|No|Sì|`Dim qty = 5`|Se `Option Infer` è abilitato (impostazione predefinita), alla variabile viene assegnato il tipo di dati dell'inizializzatore. Vedere [inferenza del tipo locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).<br /><br /> Se le istruzioni `Option Infer` e `Option Strict` sono disabilitate, il tipo di dati accettato dalla variabile è `Object`.<br /><br /> Se `Option Infer` è disabilitato e `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|Sì|No|`Dim qty As Integer`|La variabile viene inizializzata sul valore predefinito per il tipo di dati. Per ulteriori informazioni, vedere [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md).|  
|Sì|Sì|`Dim qty  As Integer = 5`|Se il tipo di dati dell'inizializzatore non è convertibile nel tipo di dati specificato, si verifica un errore in fase di compilazione.|  
  
## <a name="when-an-option-strict-statement-is-not-present"></a>Quando non è presente un'istruzione Option Strict  
 Se il codice sorgente non contiene un `Option Strict` istruzione, il **Option strict** impostazione per il [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic) viene utilizzato. Il **pagina Compila** dispone di impostazioni che consentono un maggiore controllo sulle condizioni che generano un errore.  
  
 Se si utilizza il compilatore della riga di comando, è possibile utilizzare il [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md) l'opzione del compilatore per specificare un'impostazione per `Option Strict`.  
  
### <a name="to-set-option-strict-in-the-ide"></a>Per impostare Option Strict nell'IDE  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
1.  In **Esplora**, selezionare un progetto. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Nel **compilare** scheda, impostare il valore **Option Strict** casella.  
  
###  <a name="conditions"></a>Per impostare le configurazioni di avviso nell'IDE  
 Quando si utilizza il [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic) invece di un `Option Strict` istruzione, è possibile controllare altre condizioni che generano errori. Il **configurazioni avvisi** sezione il **pagina Compila** ha impostazioni che corrispondono alle tre condizioni che causano un errore in fase di compilazione quando `Option Strict` è. Di seguito sono queste impostazioni:  
  
-   **Conversione implicita**  
  
-   **Associazione tardiva; chiamata potrebbe non riuscire in fase di esecuzione**  
  
-   **Tipo implicito. presunto oggetto**  
  
 Quando si imposta **Option Strict** a **su**, tutte e tre queste impostazioni di configurazione di avviso sono impostate su **errore**. Quando si imposta **Option Strict** a **Off**, tutte le tre opzioni siano impostate su **Nessuna**.  
  
 È possibile modificare singolarmente ogni avviso impostazione di configurazione per **Nessuna**, **avviso**, o **errore**. Se tutte le tre impostazioni di configurazione di avviso sono impostate su **errore**, `On` è presente il `Option strict` casella. Se tutte e tre sono impostate su **Nessuna**, `Off` viene visualizzato in questa casella. Per qualsiasi altra combinazione di queste impostazioni, **(personalizzata)** viene visualizzata.  
  
### <a name="to-set-the-option-strict-default-setting-for-new-projects"></a>Per impostare l'impostazione predefinita Option Strict per nuovi progetti  
 Quando si crea un progetto, il **Option Strict** impostazione per il **compilare** scheda è impostata sul **Option Strict** impostazione nel **opzioni** la finestra di dialogo.  
  
 Per impostare `Option Strict` in questa finestra di dialogo nel **strumenti** menu, fare clic su **opzioni**. Nel **opzioni** finestra di dialogo espandere **progetti e soluzioni**, quindi fare clic su **impostazioni predefinite di Visual Basic**. L'impostazione predefinita iniziale in **impostazioni predefinite di Visual Basic** è `Off`.  
  
### <a name="to-set-option-strict-on-the-command-line"></a>Per impostare Option Strict nella riga di comando  
 Includere il [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md) opzione del compilatore di **vbc** comando.  
  
## <a name="example"></a>Esempio  
 Gli esempi seguenti illustrano gli errori in fase di compilazione causati da conversioni implicite di tipi sono conversioni di restrizione. Questa categoria di errori corrisponde al **la conversione implicita** condizione di **pagina Compila**.  
  
 [!code-vb[VbVbalrStatements&#161;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_1.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato un errore in fase di compilazione causato dall'associazione tardiva. Questa categoria di errori corrisponde al **ritardo associazione; chiamata potrebbe avere esito negativo in fase di esecuzione** condizione di **pagina Compila**.  
  
 [!code-vb[VbVbalrStatements&#162;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_2.vb)]  
  
## <a name="example"></a>Esempio  
 Gli esempi seguenti illustrano gli errori causati da variabili dichiarate con un tipo implicito di `Object`. Questa categoria di errori corrisponde al **tipo implicito: presunto oggetto** condizione di **pagina Compila**.  
  
 [!code-vb[VbVbalrStatements&#163;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_3.vb)]  
  
 [!code-vb[&#164; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_4.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Ampliamento e restrizione conversioni](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Conversioni implicite ed esplicite](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Compilazione (pagina), Creazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)   
 [Istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Funzioni di conversione del tipo](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Procedura: accedere ai membri di un oggetto](../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)   
 [Espressioni incorporate in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [Conversione di tipo relaxed del delegato](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [Associazione tardiva nelle soluzioni Office](https://msdn.microsoft.com/library/3xxe951d)   
 [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
