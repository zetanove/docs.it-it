---
title: "Try...Catch...Finally Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Try...Catch...Finally"
  - "vb.when"
  - "vb.Finally"
  - "vb.Catch"
  - "vb.Try"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Try...Catch...Finally statements"
  - "Try statement"
  - "try-catch exception handling, Try...Catch...Finally statements"
  - "error handling, while running code"
  - "Try statement, Try...Catch...Finally"
  - "Finally keyword [Visual Basic], Try...Catch...Finally"
  - "Catch statement"
  - "When keyword"
  - "Visual Basic code, handling errors while running"
  - "structured exception handling, Try...Catch...Finally statements"
ms.assetid: d6488026-ccb3-42b8-a810-0d97b9d6472b
caps.latest.revision: 69
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 69
---
# Try...Catch...Finally Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di gestire alcuni o tutti i possibili errori che possono verificarsi in un determinato blocco di codice in esecuzione.  
  
## Sintassi  
  
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
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`tryStatements`|Opzionale.  Una o più istruzioni in cui può verificarsi un errore.  Può trattarsi di un'istruzione composta.|  
|`Catch`|Opzionale.  Sono ammessi più blocchi `Catch`.  Se durante l'elaborazione del blocco `Try` si verifica un'eccezione, ogni istruzione `Catch` viene esaminata in ordine testuale per stabilire se gestisce l'eccezione. L'eccezione generata è rappresentata da `exception`.|  
|`exception`|Opzionale.  Qualsiasi nome di variabile.  Il valore iniziale di `exception` corrisponde al valore dell'errore generato.  Viene utilizzata con `Catch` per specificare l'errore intercettato.  Se omessa, l'istruzione `Catch` genera un'eccezione.|  
|`type`|Opzionale.  Consente di specificare il tipo di classe filtrato.  Se il valore di `exception` è del tipo specificato da `type` o di un tipo derivato da questo, l'identificatore viene associato all'oggetto eccezione.|  
|`When`|Opzionale.  Un'istruzione `Catch` con una clausola `When` intercetta eccezioni solo quando `expression` restituisce `True`.  Una clausola `When` viene applicata soltanto dopo il controllo del tipo di eccezione; `expression` può fare riferimento all'identificatore che indica l'eccezione.|  
|`expression`|Opzionale.  Deve essere convertibile in modo implicito in un valore di tipo `Boolean`.  Qualsiasi espressione in cui è descritto un filtro generico.  Utilizzato in genere per filtrare in base al numero di errore.  Viene utilizzato con la parola chiave `When` per specificare le circostanze in cui è stato intercettato l'errore.|  
|`catchStatements`|Opzionale.  Una o più istruzioni per la gestione degli errori verificatisi nel blocco `Try` associato.  Può trattarsi di un'istruzione composta.|  
|`Exit Try`|Opzionale.  Parola chiave con cui viene interrotta la struttura `Try...Catch...Finally`.  L'esecuzione riprende con il codice immediatamente successivo all'istruzione `End Try`.  Verrà eseguita l'istruzione `Finally`.  Non ammessa nei blocchi `Finally`.|  
|`Finally`|Opzionale.  Blocco `Finally` che viene eseguito tutte le volte che l'esecuzione abbandona l'istruzione `Try...Catch` in un punto qualsiasi.|  
|`finallyStatements`|Opzionale.  Una o più istruzioni eseguite dopo l'elaborazione di tutti gli altri errori.|  
|`End Try`|Consente di terminare la struttura `Try...Catch...Finally`.|  
  
## Note  
 Se si prevede il verificarsi di una determinata eccezione nel corso di una particolare sezione di codice, inserire il codice in un blocco `Try` e utilizzare un blocco `Catch` per mantenere il controllo e gestire l'eccezione nel caso in cui si verifichi.  
  
 Un'istruzione `Try…Catch` è costituita da un blocco `Try` seguito da una o più clausole `Catch`, mediante le quali vengono specificati i gestori per diverse eccezioni.  Quando viene generata un'eccezione in un blocco `Try`, tramite [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] viene cercata l'istruzione `Catch` mediante la quale viene gestita l'eccezione.  Se non viene individuata un'istruzione `Catch` corrispondente, il metodo mediante il quale è stata eseguita la chiamata al metodo corrente e così via lungo lo stack di chiamate viene esaminato da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  Se non viene trovato alcun blocco `Catch`, in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] viene visualizzato un messaggio di eccezione non gestita e l'esecuzione del programma viene arrestata.  
  
 È possibile utilizzare più istruzioni `Catch` in un'istruzione `Try…Catch`.  In tal caso, l'ordine delle clausole `Catch` è importante poiché vengono esaminate nell'ordine specificato.  Vengono intercettate prima le eccezioni più specifiche, quindi quelle meno specifiche.  
  
 Le seguenti condizioni dell'istruzione `Catch` sono quelle meno specifiche e consentono di rilevare tutte le eccezioni che derivano dalla classe <xref:System.Exception>.  Di norma, si consiglia di utilizzare una di queste variazioni come ultimo blocco `Catch` nella struttura `Try...Catch...Finally`, una volta generate tutte le eccezioni specifiche previste.  Il flusso di controllo non può raggiungere mai un blocco `Catch` che segue una di queste variazioni.  
  
-   Il valore di `type` è `Exception`, ad esempio: `Catch ex As Exception`  
  
-   Nell'istruzione non sono presenti variabili `exception`, ad esempio: `Catch`  
  
 Quando un'istruzione `Try…Catch…Finally` è annidata in un altro blocco `Try`, in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] viene esaminata dapprima ciascuna istruzione `Catch` nella parte più interna del blocco `Try`.  Se non viene trovata alcuna istruzione `Catch` corrispondente, si continua la ricerca nelle istruzioni `Catch` del blocco `Try…Catch…Finally` esterno.  
  
 Le variabili locali di un blocco `Try` non sono disponibili in un blocco `Catch` in quanto rappresentano blocchi separati.  Se si desidera utilizzare una variabile in più blocchi, dichiarare la variabile al di fuori della struttura `Try...Catch...Finally`.  
  
> [!TIP]
>  L'istruzione `Try…Catch…Finally` è disponibile come frammento di codice IntelliSense.  In Gestione frammenti di codice espandere **Modelli di codice \- If, For Each, Try Catch, Property e così via**, quindi **Gestione errori \(Eccezioni\)**.  Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
## Blocco finally  
 Se si dispone di una o più istruzioni da eseguire prima di uscire dalla struttura `Try`, utilizzare un blocco `Finally`.  Il controllo viene passato al blocco `Finally` appena prima dell'uscita dalla struttura `Try…Catch`.  Il passaggio avviene anche se si verifica un'eccezione in qualsiasi posizione all'interno della struttura `Try`.  
  
 Un blocco `Finally` è utile per l'esecuzione di qualsiasi codice sia necessario eseguire persino in presenza di un'eccezione.  Il controllo viene passato al blocco `Finally`, indipendentemente dalla modalità di uscita dal blocco `Try...Catch`.  
  
 Il codice incluso in un blocco `Finally` viene eseguito anche se si incontra un'istruzione `Return` in un blocco `Try` o `Catch`.  Il controllo non viene passato da un blocco `Try` o `Catch` al blocco `Finally` corrispondente nei seguenti casi:  
  
-   Un'[End Statement](../../../visual-basic/language-reference/statements/end-statement.md) viene rilevata nel blocco `Try` o `Catch`.  
  
-   Un'eccezione <xref:System.StackOverflowException> viene generata nel blocco `Try` o `Catch`.  
  
 Non è valida in modo esplicito trasferire l'esecuzione in un blocco `Finally`.  L'esecuzione di trasferimento da un blocco `Finally` non è valida, ma con un'eccezione.  
  
 Se un'istruzione `Try` non contiene almeno un blocco `Catch`, deve contenere un blocco `Finally`.  
  
> [!TIP]
>  Se non è necessario rilevare eccezioni specifiche, il comportamento dell'istruzione `Using` è identico a quello di un blocco `Try…Finally` e viene garantita l'eliminazione delle risorse, a prescindere dalla modalità di uscita dal blocco.  Questo meccanismo è valido anche per le eccezioni non gestite.  Per ulteriori informazioni, vedere [Using Statement](../../../visual-basic/language-reference/statements/using-statement.md).  
  
## Argomento Exception  
 L'argomento `exception` del blocco `Catch` è un'istanza della classe <xref:System.Exception> oppure una classe che deriva dalla classe `Exception`.  L'istanza della classe `Exception` corrisponde all'errore verificatosi nel blocco `Try`.  
  
 Le proprietà dell'oggetto `Exception` consentono di identificare la causa e il percorso di un'eccezione.  Ad esempio, nella proprietà <xref:System.Exception.StackTrace%2A> sono elencati i metodi chiamati che hanno causato l'eccezione, in modo da consentire di individuare il punto del codice in cui si è verificato l'errore.  Tramite la proprietà <xref:System.Exception.Message%2A> viene restituito un messaggio in cui viene descritta l'eccezione.  Tramite la proprietà <xref:System.Exception.HelpLink%2A> viene restituito un collegamento a un file della Guida associato.  Tramite la proprietà <xref:System.Exception.InnerException%2A> viene restituito l'oggetto `Exception` mediante il quale è stata causata l'eccezione corrente oppure viene restituito `Nothing` se non è presente alcun oggetto `Exception` originale.  
  
## Considerazioni in caso di utilizzo di un blocco Try...Catch  
 Utilizzare un'istruzione `Try…Catch` solo segnalare il verificarsi di eventi anomali o imprevisti.  Di seguito sono elencati alcuni dei motivi:  
  
-   Il rilevamento di eccezioni in fase di esecuzione crea sovraccarico aggiuntivo e probabilmente risulta più lento rispetto a un controllo preventivo per evitare le eccezioni.  
  
-   Se un blocco `Catch` non viene gestito correttamente, l'eccezione potrebbe non essere segnalata correttamente agli utenti.  
  
-   La gestione delle eccezioni rende più complesso un programma.  
  
 Non sempre è necessaria un'istruzione `Try…Catch` per controllare una condizione che è probabile si verifichi.  Nell'esempio seguente viene verificata l'esistenza di un file prima di tentarne l'apertura.  In tal modo, la necessità di rilevare un'eccezione generata dal metodo <xref:System.IO.File.OpenText%2A> si riduce.  
  
 [!code-vb[VbVbalrStatements#94](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_1.vb)]  
  
 Assicurarsi che il codice nei blocchi `Catch` consenta di segnalare correttamente le eccezioni agli utenti, tramite l'accesso thread\-safe o messaggi appropriati.  In caso contrario, le eccezioni potrebbero rimanere sconosciute.  
  
## Metodi di Async  
 Se si contrassegna un metodo con il modificatore [Async](../../../visual-basic/language-reference/modifiers/async.md), è possibile utilizzare l'operatore [Attendere](../../../visual-basic/language-reference/operators/await-operator.md) nel metodo.  Un'istruzione con l'operatore `Await` sospende l'esecuzione del metodo finché l'attività attesa non completi.  l'attività rappresenta il lavoro in corso.  Quando l'attività associata all'operatore `Await` completa, l'esecuzione riprende lo stesso metodo.  Per ulteriori informazioni, vedere [Flusso di controllo in programmi asincroni](../Topic/Control%20Flow%20in%20Async%20Programs%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Un'attività restituita da un metodo di Async può terminare lo stato Faulted, indicando che ha terminato a causa di un'eccezione non gestita.  Un'attività può inoltre possibile terminare in uno stato annullato, pertanto `OperationCanceledException` generato dall'espressione di attesa.  Per rilevare qualsiasi tipo di eccezione, inserire l'espressione `Await` associata all'attività in un blocco `Try` e per rilevare l'eccezione nel blocco `Catch`.  Un esempio è dato più avanti in questo argomento.  
  
 Un'attività può essere in uno stato di errore perché più eccezioni sono responsabili dell'errore.  Ad esempio, un'attività potrebbe essere il risultato di una chiamata a <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>.  Quando si attendono tale attività, l'eccezione viene rilevata una sola delle eccezioni e non è possibile prevedere quale eccezione viene intercettata.  Un esempio è dato più avanti in questo argomento.  
  
 Un'espressione `Await` non può trovarsi a un blocco `Catch` o del blocco `Finally`.  
  
## Iteratori  
 Una funzione iteratori o una funzione di accesso `Get` esegue un'iterazione personalizzata in una raccolta.  Un iteratore utilizza un'istruzione [Prestazioni](../../../visual-basic/language-reference/statements/yield-statement.md) per restituire ogni elemento della raccolta uno alla volta.  Chiama una funzione iteratori utilizzando [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
 Un'istruzione `Yield` può essere in un blocco `Try`.  Un blocco `Try` contenente un'istruzione `Yield` può contenere blocchi `Catch` e può presentare un blocco `Finally`.  Vedere “blocco try la sezione in Visual Basic„ [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md) per un esempio.  
  
 Un'istruzione `Yield` non può trovarsi a un blocco `Catch` o un blocco `Finally`.  
  
 Se il corpo `For Each` \(l'esterno della funzione iteratori\) genera un'eccezione, un blocco `Catch` nella funzione iteratori non viene eseguito, ma un blocco `Finally` nella funzione di iteratore viene eseguito.  Un blocco `Catch` in una funzione iteratori rilevate solo le eccezioni che si verificano nella funzione di iteratore.  
  
## Situazioni parzialmente attendibili  
 Nelle situazioni di attendibilità parziale, ad esempio un'applicazione ospitata in una condivisione di rete, la struttura `Try...Catch...Finally` non intercetta le eccezioni di sicurezza che si verificano prima che venga richiamato il metodo contenente la chiamata.  Nell'esempio riportato di seguito, se l'istruzione viene inserita su una condivisione server ed eseguita da tale posizione, verrà generato l'errore "System.Security.SecurityException: Richiesta non riuscita". Per ulteriori informazioni sulle eccezioni di sicurezza, vedere la classe <xref:System.Security.SecurityException>.  
  
 [!code-vb[VbVbalrStatements#85](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_2.vb)]  
  
 In una situazione di attendibilità parziale di questo tipo, è necessario inserire l'istruzione `Process.Start` in un'istruzione `Sub` separata.  La chiamata iniziale a `Sub` avrà esito negativo.  In questo modo, l'istruzione `Try...Catch` potrà intercettarlo prima che venga avviato l'oggetto `Sub` contenente `Process.Start` e prodotta l'eccezione di sicurezza.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata la struttura dell'istruzione `Try...Catch...Finally`.  
  
 [!code-vb[VbVbalrStatements#86](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_3.vb)]  
  
## Esempio  
 Nell'esempio seguente, tramite il metodo `CreateException` viene generata un'eccezione `NullReferenceException`.  Il codice tramite il quale viene generata l'eccezione non è in un blocco `Try`.  Pertanto, il metodo `CreateException` non consente la gestione dell'eccezione.  L'eccezione viene gestita tramite il metodo `RunSample` poiché la chiamata al metodo `CreateException` è in un blocco `Try`.  
  
 Nell'esempio vengono incluse le istruzioni `Catch` per diversi tipi di eccezioni, ordinate dalla più specifica alla più generale.  
  
 [!code-vb[VbVbalrStatements#91](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_4.vb)]  
  
## Esempio  
 Nell'esempio seguente viene mostrato come utilizzare un'istruzione `Catch When` per filtrare un'espressione condizionale.  Se l'espressione condizionale restituisce `True`, viene eseguito il codice nel blocco `Catch`.  
  
 [!code-vb[VbVbalrStatements#92](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_5.vb)]  
  
## Esempio  
 Nell'esempio seguente è presente un'istruzione `Try…Catch` contenuta in un blocco `Try`.  Tramite il blocco `Catch` interno viene generata un'eccezione la cui proprietà `InnerException` è impostata sull'eccezione originale.  Tramite il blocco `Catch` esterno vengono segnalate l'eccezione propria del blocco e quella interna.  
  
 [!code-vb[VbVbalrStatements#93](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/try-catch-finally-statement_6.vb)]  
  
## Esempio  
 Il seguente esempio viene illustrata la gestione delle eccezioni per i metodi async.  Per intercettare un'eccezione che si applica a un'attività async, l'espressione `Await` è in un blocco `Try` del chiamante e l'eccezione viene rilevata nel blocco `Catch`.  
  
 Rimuovere il commento dalla riga `Throw New Exception` nell'esempio per illustrare la gestione delle eccezioni.  L'eccezione viene rilevata nel blocco `Catch`, la proprietà `IsFaulted` dell'attività è impostata su `True`e la proprietà `Exception.InnerException` dell'attività viene impostata sull'eccezione.  
  
 Rimuovere il commento dalla riga `Throw New OperationCancelledException` per illustrare ciò che si verifica quando si annulla un processo asincrono.  L'eccezione viene rilevata nel blocco `Catch` e la proprietà `IsCanceled` dell'attività è impostata su `True`.  Tuttavia, in alcuni casi non si applicano a questo esempio, `IsFaulted` è impostato su `True` e `IsCanceled` è impostato su `False`.  
  
 [!code-vb[csAsyncExceptions#1](../../../csharp/language-reference/keywords/codesnippet/VisualBasic/try-catch-finally-statement_7.vb)]  
  
## Esempio  
 Il seguente esempio viene illustrata la gestione delle eccezioni in cui più attività possono comportare più eccezioni.  Il blocco `Try` è l'espressione `Await` per l'attività che <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> restituito.  L'attività è completa quando le tre attività a cui si applica <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> sono state completate.  
  
 Ciascuna delle cause di attività un'eccezione.  Il blocco `Catch` scorre le eccezioni, che si trovano nella proprietà `Exception.InnerExceptions` dell'attività che `Task.WhenAll` restituito.  
  
 [!code-vb[csAsyncExceptions#3](../../../csharp/language-reference/keywords/codesnippet/VisualBasic/try-catch-finally-statement_8.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Information.Err%2A>   
 <xref:System.Exception>   
 [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [On Error Statement](../../../visual-basic/language-reference/statements/on-error-statement.md)   
 [Procedure consigliate per l'utilizzo dei frammenti di codice](/visual-studio/ide/best-practices-for-using-code-snippets)   
 [Gestione delle eccezioni](../Topic/Exception%20Handling%20\(Task%20Parallel%20Library\).md)   
 [Throw Statement](../../../visual-basic/language-reference/statements/throw-statement.md)