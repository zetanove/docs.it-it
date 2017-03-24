---
title: Try... Catch... Istruzione finally (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Try...Catch...Finally
- vb.when
- vb.Finally
- vb.Catch
- vb.Try
dev_langs:
- VB
helpviewer_keywords:
- Try...Catch...Finally statements
- Try statement
- try-catch exception handling, Try...Catch...Finally statements
- error handling, while running code
- Try statement, Try...Catch...Finally
- Finally keyword [Visual Basic], Try...Catch...Finally
- Catch statement
- When keyword
- Visual Basic code, handling errors while running
- structured exception handling, Try...Catch...Finally statements
ms.assetid: d6488026-ccb3-42b8-a810-0d97b9d6472b
caps.latest.revision: 69
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
ms.openlocfilehash: 379359e3a338746ccd440dbe1ad58c483e562dbe
ms.lasthandoff: 03/13/2017

---
# <a name="trycatchfinally-statement-visual-basic"></a>Istruzione Try...Catch...Finally (Visual Basic)
Fornisce un modo per gestire alcuni o tutti i possibili errori che potrebbero verificarsi in un determinato blocco di codice, codice in esecuzione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Try  
    [ tryStatements ]  
    [ Exit Try ]  
[ Catch [ exception [ As type ] ] [ When expression ]  
    [ catchStatements ]  
    [ Exit Try ] ]  
[ Catch ... ]  
[ Finally  
    [ finallyStatements ] ]  
End Try  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`tryStatements`|Facoltativo. Una o più istruzioni in cui può verificarsi un errore. Può essere un'istruzione composta.|  
|`Catch`|Facoltativo. Più `Catch` blocchi consentiti. Se si verifica un'eccezione durante l'elaborazione di `Try` blocco, ogni `Catch` istruzione verrà esaminata in ordine testuale per stabilire se gestisce l'eccezione, con `exception` che rappresenta l'eccezione che è stata generata.|  
|`exception`|Facoltativo. Qualsiasi nome di variabile. Il valore iniziale di `exception` corrisponde al valore dell'errore generato. Utilizzato con `Catch` per specificare l'errore rilevato. Se omesso, il `Catch` istruzione genera un'eccezione.|  
|`type`|Facoltativo. Specifica il tipo di filtro di classe. Se il valore di `exception` è del tipo specificato da `type` o di un tipo derivato, l'identificatore viene associato all'oggetto eccezione.|  
|`When`|Facoltativo. Oggetto `Catch` istruzione con un `When` clausola intercetta le eccezioni solo quando `expression` restituisce `True`. Oggetto `When` clausola viene applicata solo dopo avere selezionato il tipo di eccezione, e `expression` possono fare riferimento a un identificatore che rappresenta l'eccezione.|  
|`expression`|Facoltativo. Deve essere convertibile in modo implicito in `Boolean`. Qualsiasi espressione che descrive un filtro generico. In genere utilizzato per filtrare in base al numero di errore. Utilizzato con `When` (parola chiave) per specificare le circostanze in cui viene rilevato l'errore.|  
|`catchStatements`|Facoltativo. Istruzioni per gestire gli errori che si verificano nel blocco `Try` blocco. Può essere un'istruzione composta.|  
|`Exit Try`|Facoltativo. Parola chiave che viene interrotta la `Try...Catch...Finally` struttura. Con il codice immediatamente dopo l'esecuzione riprende il `End Try` istruzione. Il `Finally` verrà eseguita l'istruzione. Non è consentito in `Finally` blocchi.|  
|`Finally`|Facoltativo. Oggetto `Finally` blocco viene eseguito quando l'esecuzione lascia qualsiasi parte di `Try...Catch` istruzione.|  
|`finallyStatements`|Facoltativo. Una o più istruzioni che vengono eseguite dopo ogni altra elaborazione di errore.|  
|`End Try`|Termina la `Try...Catch...Finally` struttura.|  
  
## <a name="remarks"></a>Note  
 Se si prevede che una particolare eccezione potrebbe verificarsi durante una particolare sezione di codice, inserire il codice in un `Try` blocco e utilizzare un `Catch` blocco per mantenere il controllo e gestire l'eccezione, se si verifica.  
  
 Oggetto `Try…Catch` istruzione costituita da un `Try` blocco seguito da uno o più `Catch` clausole che specificano i gestori per diverse eccezioni. Quando viene generata un'eccezione un `Try` blocco, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Cerca il `Catch` istruzione che gestisce l'eccezione. Se un corrispondente `Catch` istruzione non viene trovata, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] esamina il metodo che ha chiamato il metodo corrente, e così via lungo lo stack di chiamate. Se non `Catch` blocco viene trovato, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Visualizza un messaggio di eccezione non gestita all'utente e interrompe l'esecuzione del programma.  
  
 È possibile utilizzare più `Catch` istruzione in un `Try…Catch` istruzione. In tal caso, l'ordine dei `Catch` clausole è importante in quanto vengono esaminate nell'ordine. Intercettare le eccezioni più specifiche prima di quelle meno specifiche.  
  
 Nell'esempio `Catch` condizioni dell'istruzione sono quelle meno specifiche e intercetterà tutte le eccezioni che derivano dalla <xref:System.Exception>classe.</xref:System.Exception> È in genere necessario utilizzare una di queste variazioni come l'ultima `Catch` blocco il `Try...Catch...Finally` struttura, dopo l'intercettazione si prevede che tutte le eccezioni specifiche. Flusso di controllo non può mai raggiungere un `Catch` blocco che segue una di queste variazioni.  
  
-   Il `type` è `Exception`, ad esempio:`Catch ex As Exception`  
  
-   L'istruzione non ha alcun `exception` variabile, ad esempio:`Catch`  
  
 Quando un `Try…Catch…Finally` nidificata in un'altra istruzione `Try` blocco, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] innanzitutto esaminare ogni `Catch` istruzione nella parte più interna `Try` blocco. Se nessuna corrispondenza `Catch` istruzione è stata trovata, la ricerca procede con la `Catch` istruzioni di esterna `Try…Catch…Finally` blocco.  
  
 Le variabili locali di un `Try` blocco non sono disponibili in un `Catch` bloccarsi, in quanto rappresentano blocchi separati. Se si desidera utilizzare una variabile in più di un blocco, dichiarare la variabile all'esterno di `Try...Catch...Finally` struttura.  
  
> [!TIP]
>  La `Try…Catch…Finally` informativa è disponibile come frammento di codice IntelliSense. In Gestione frammenti di codice, espandere **modelli di codice - se, per ognuno, Try Catch, proprietà, e così via**e quindi **Error Handling (eccezioni)**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
## <a name="finally-block"></a>Blocco finally  
 Se si dispone di uno o più istruzioni da eseguire prima di chiudere il `Try` struttura, utilizzare un `Finally` blocco. Il controllo passa al `Finally` blocco appena prima di passare fuori il `Try…Catch` struttura. Questo vale anche se si verifica un'eccezione in un punto qualsiasi all'interno di `Try` struttura.  
  
 Oggetto `Finally` blocco è utile per eseguire qualsiasi codice che deve eseguire anche se si verifica un'eccezione. Il controllo viene passato per il `Finally` blocco indipendentemente da come la `Try...Catch` uscita dal blocco.  
  
 Il codice in un `Finally` blocco viene eseguito anche se il codice rileva un `Return` istruzione in un `Try` o `Catch` blocco. Il controllo viene passato da un `Try` o `Catch` blocco per il corrispondente `Finally` blocco nei casi seguenti:  
  
-   Un [istruzione End](../../../visual-basic/language-reference/statements/end-statement.md) viene rilevata nel `Try` o `Catch` blocco.  
  
-   Oggetto <xref:System.StackOverflowException>viene generata nel `Try` o `Catch` blocco.</xref:System.StackOverflowException>  
  
 Non è valido per trasferire in modo esplicito l'esecuzione in un `Finally` blocco. Trasferimento di esecuzione all'esterno di un `Finally` blocco non è valido, ad eccezione di un'eccezione.  
  
 Se un `Try` istruzione non contiene almeno un `Catch` blocco, deve contenere un `Finally` blocco.  
  
> [!TIP]
>  Se non è necessario rilevare eccezioni specifiche, il `Using` istruzione si comporta come un `Try…Finally` blocco e garantisce l'eliminazione delle risorse, indipendentemente dalla modalità di uscita dal blocco. Ciò è vero anche con un'eccezione non gestita. Per ulteriori informazioni, vedere [istruzione Using](../../../visual-basic/language-reference/statements/using-statement.md).  
  
## <a name="exception-argument"></a>Argomento Exception  
 Il `Catch` blocco `exception` argomento è un'istanza della <xref:System.Exception>classe o una classe che deriva dalla `Exception` classe</xref:System.Exception> Il `Exception` istanza della classe corrisponde all'errore che si è verificato durante il `Try` blocco.  
  
 Le proprietà del `Exception` oggetto servono a identificare la causa e la posizione di un'eccezione. Ad esempio, la <xref:System.Exception.StackTrace%2A>proprietà sono elencati i metodi di chiamata che ha causato l'eccezione, consentendo di individuare dove si è verificato l'errore nel codice.</xref:System.Exception.StackTrace%2A> <xref:System.Exception.Message%2A>Restituisce un messaggio che descrive l'eccezione.</xref:System.Exception.Message%2A> <xref:System.Exception.HelpLink%2A>Restituisce un collegamento a un file della Guida associato.</xref:System.Exception.HelpLink%2A> <xref:System.Exception.InnerException%2A>Restituisce il `Exception` oggetto che ha causato l'eccezione corrente oppure restituisce `Nothing` se è presente alcun originale `Exception`.</xref:System.Exception.InnerException%2A>  
  
## <a name="considerations-when-using-a-trycatch-statement"></a>Considerazioni sull'utilizzo di un blocco Try... Catch (istruzione)  
 Utilizzare un `Try…Catch` istruzione solo per segnalare la presenza di eventi anomali o imprevisti. Le cause includono quanto segue:  
  
-   Intercettare le eccezioni in fase di esecuzione comporta un sovraccarico aggiuntivo e potrebbero essere più lento rispetto alla verifica preliminare per evitare le eccezioni.  
  
-   Se un `Catch` blocco non viene gestito correttamente, l'eccezione potrebbe non essere segnalata correttamente agli utenti.  
  
-   Gestione delle eccezioni rende più complesso un programma.  
  
 Non è sempre necessario un `Try…Catch` istruzione per verificare la presenza di una condizione che è probabile che si verifichi. Nell'esempio seguente verifica l'esistenza di un file prima di tentare di aprirlo. Questo riduce la necessità di rilevare un'eccezione generata dal <xref:System.IO.File.OpenText%2A>(metodo).</xref:System.IO.File.OpenText%2A>  
  
 [!code-vb[VbVbalrStatements&#94;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_1.vb)]  
  
 Assicurarsi che il codice `Catch` blocchi possono segnalare correttamente le eccezioni per gli utenti, tramite accesso thread-safe o messaggi appropriati. In caso contrario, le eccezioni potrebbero rimanere sconosciute.  
  
## <a name="async-methods"></a>Metodi asincroni  
 Se si contrassegna un metodo con il [Async](../../../visual-basic/language-reference/modifiers/async.md) modificatore, è possibile utilizzare il [Await](../../../visual-basic/language-reference/operators/await-operator.md) operatore nel metodo. Un'istruzione con il `Await` operatore sospende l'esecuzione del metodo fino al completamento dell'attività attesa. L'attività rappresenta il lavoro attualmente in fase di esecuzione. Quando l'attività che è associato il `Await` operatore termina, riprende l'esecuzione nello stesso metodo. Per ulteriori informazioni, vedere [flusso di controllo in programmi asincroni](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md).  
  
 Un'attività restituita da un metodo asincrono può terminare con uno stato di errore, che indica che è stata completata a causa di un'eccezione non gestita. Un'attività può inoltre terminare in uno stato annullato, che comporta un `OperationCanceledException` generata fuori l'espressione await. Per entrambi i tipi di eccezione, inserire il `Await` espressione associata all'attività in un `Try` bloccare e rilevare l'eccezione nel `Catch` blocco. Viene fornito un esempio più avanti in questo argomento.  
  
 Un'attività può essere in uno stato di errore in quanto più eccezioni sono stati responsabili per il relativo stato di errore. Ad esempio, l'attività potrebbe essere il risultato di una chiamata a <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>.</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> Quando si attende tale attività, l'eccezione rilevata è solo una delle eccezioni e non è possibile prevedere quale eccezione verrà intercettata. Viene fornito un esempio più avanti in questo argomento.  
  
 Un `Await` espressione non può essere all'interno di un `Catch` blocco o `Finally` blocco.  
  
## <a name="iterators"></a>Iteratori  
 Una funzione iteratore o `Get` della funzione di accesso esegue un'iterazione personalizzata su una raccolta. Un iteratore utilizza un [Yield](../../../visual-basic/language-reference/statements/yield-statement.md) istruzione per la restituzione di ogni elemento della raccolta uno alla volta. Per chiamare una funzione iteratore un [For Each... Istruzione successiva](../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
 Oggetto `Yield` istruzione può essere contenuta in un `Try` blocco. Oggetto `Try` blocco che contiene un `Yield` istruzione possono essere presenti `Catch` si blocca e può avere un `Finally` blocco. Vedere la sezione "provare a blocchi in Visual Basic" di [iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7) per un esempio.  
  
 Oggetto `Yield` istruzione non può essere all'interno di un `Catch` blocco o un `Finally` blocco.  
  
 Se il `For Each` corpo (all'esterno della funzione iteratore) genera un'eccezione, un `Catch` blocco nella funzione iteratore non viene eseguita, ma un `Finally` try nella funzione iteratore. Oggetto `Catch` blocco all'interno di una funzione iteratore intercetta solo le eccezioni che si verificano all'interno della funzione iteratore.  
  
## <a name="partial-trust-situations"></a>Situazioni di attendibilità parziale  
 In situazioni di attendibilità parziale, ad esempio un'applicazione ospitata in una condivisione di rete, `Try...Catch...Finally` non intercetta le eccezioni di sicurezza che si verificano prima che venga richiamato il metodo che contiene la chiamata. L'esempio seguente, quando si inserisce in una condivisione server ed eseguita da lì, produce l'errore "System.Security.SecurityException: richiesta non riuscita." Per ulteriori informazioni sulle eccezioni di sicurezza, vedere la <xref:System.Security.SecurityException>classe.</xref:System.Security.SecurityException>  
  
 [!code-vb[&#85; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_2.vb)]  
  
 In una situazione di attendibilità parziale di questo tipo, è necessario inserire il `Process.Start` istruzione in un oggetto separato `Sub`. La chiamata iniziale per il `Sub` avrà esito negativo. In questo modo `Try...Catch` per intercettare, prima di `Sub` contenente `Process.Start` viene avviato e ha causato l'eccezione di sicurezza.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata la struttura del `Try...Catch...Finally` istruzione.  
  
 [!code-vb[VbVbalrStatements&#86;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_3.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, il `CreateException` genererà un `NullReferenceException`. Il codice che genera l'eccezione non si trova in un `Try` blocco. Pertanto, il `CreateException` metodo gestisce l'eccezione. Il `RunSample` metodo gestisce l'eccezione perché la chiamata al `CreateException` metodo si trova in un `Try` blocco.  
  
 L'esempio include `Catch` istruzioni per diversi tipi di eccezioni, ordinate dalla più specifica alla più generale.  
  
 [!code-vb[VbVbalrStatements&#91;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_4.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare un `Catch When` istruzione per filtrare un'espressione condizionale. Se l'espressione condizionale restituisce `True`, il codice di `Catch` bloccare l'esecuzione.  
  
 [!code-vb[VbVbalrStatements&#92;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_5.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente è presente un `Try…Catch` istruzione contenuta in un `Try` blocco. L'eccezione interna `Catch` blocco genera un'eccezione che ha il `InnerException` impostata sull'eccezione originale. Esterna `Catch` blocco segnala la propria eccezione e l'eccezione interna.  
  
 [!code-vb[&#93; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_6.vb)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra la gestione delle eccezioni per i metodi asincroni. Per rilevare un'eccezione che si applica a un'attività asincrona, il `Await` l'espressione ha un `Try` blocco del chiamante e l'eccezione viene rilevata nel `Catch` blocco.  
  
 Rimuovere il commento dalla riga `Throw New Exception` nell'esempio per illustrare la gestione delle eccezioni. L'eccezione viene rilevata nel `Catch` blocco, l'attività `IsFaulted` è impostata su `True`e l'attività `Exception.InnerException` proprietà è impostata sull'eccezione.  
  
 Rimuovere il commento di `Throw New OperationCancelledException` riga per illustrare ciò che accade quando si annulla un processo asincrono. L'eccezione viene rilevata nel `Catch` blocco e l'attività `IsCanceled` è impostata su `True`. Tuttavia, in alcune condizioni sono validi per questo esempio, `IsFaulted` è impostato su `True` e `IsCanceled` è impostato su `False`.  
  
 [!code-vb[csAsyncExceptions n.&1;](../../../csharp/language-reference/keywords/codesnippet/VisualBasic/try-catch-finally-statement_7.vb)]  
  
## <a name="example"></a>Esempio  
 Il seguente esempio illustra la gestione delle eccezioni dove più attività possono restituire più eccezioni. Il `Try` blocco ha il `Await` espressione per l'attività che <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>restituito.</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> L'attività viene completata quando le tre attività a cui <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>viene applicato sono state completate.</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>  
  
 Ognuna delle tre attività genera un'eccezione. Il `Catch` blocco scorre le eccezioni, che si trovano nella `Exception.InnerExceptions` proprietà dell'attività che `Task.WhenAll` restituito.  
  
 [!code-vb[csAsyncExceptions n.&3;](../../../csharp/language-reference/keywords/codesnippet/VisualBasic/try-catch-finally-statement_8.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Information.Err%2A></xref:Microsoft.VisualBasic.Information.Err%2A>   
 <xref:System.Exception></xref:System.Exception>   
 [Exit (istruzione)](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Istruzione On Error](../../../visual-basic/language-reference/statements/on-error-statement.md)   
 [Procedure consigliate per l'utilizzo di frammenti di codice](https://docs.microsoft.com/visualstudio/ide/best-practices-for-using-code-snippets)   
 [Gestione delle eccezioni](https://msdn.microsoft.com/library/dd997415)   
 [Istruzione Throw](../../../visual-basic/language-reference/statements/throw-statement.md)
