---
title: "On Error Statement (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.OnError"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, control flow"
  - "Resume Next statement"
  - "errors [Visual Basic], trapping"
  - "error handling, On Error statement"
  - "Next statement, On Error"
  - "control flow, branching"
  - "Error keyword"
  - "execution, conditional"
  - "Resume statement, and On Error statement"
  - "Error statement, and On Error statement"
  - "GoTo statement, and On Error statement"
  - "branching, on error"
  - "conditional statements, On Error"
  - "On Error statement, syntax"
  - "On keyword"
  - "run-time errors, handling"
  - "On Error statement"
ms.assetid: ff947930-fb84-40cf-bd66-1ea219561d5c
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# On Error Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di abilitare una routine di gestione degli errori e di specificarne la posizione all'interno di una routine più ampia. Consente inoltre di disabilitare una routine di gestione degli errori.  
  
 In assenza di un'istruzione `On Error`, qualsiasi errore di runtime può risultare irreversibile: viene visualizzato un messaggio di errore e l'esecuzione viene interrotta.  
  
 Se possibile, si è gestione delle eccezioni strutturata di utilizzo nel codice, anziché utilizzare la gestione delle eccezioni non strutturata e `On Error` istruzione.  Per ulteriori informazioni, vedere [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
> [!NOTE]
>  La parola chiave `Error` viene utilizzata anche nell'[Error Statement](../../../visual-basic/language-reference/statements/error-statement.md), supportata per garantire la compatibilità con le versioni precedenti.  
  
## Sintassi  
  
```  
On Error { GoTo [ line | 0 | -1 ] | Resume Next }  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`GoTo` `line`|Consente di attivare la routine di gestione degli errori che inizia sulla riga specificata nell'argomento obbligatorio `line`.  L'argomento `line` può corrispondere a qualsiasi numero o etichetta di riga.  Se si verifica un errore di runtime, il controllo crea un ramo nella riga specificata, attivando il gestore errori.  La riga specificata deve trovarsi nella stessa routine dell'istruzione `On Error`. In caso contrario si verificherà un errore di compilazione.|  
|`GoTo` 0|Consente di disabilitare il gestore errori attivato nella routine corrente e di reimpostarlo su `Nothing`.|  
|`GoTo` \-1|Consente di disabilitare l'eccezione attivata nella routine corrente e di reimpostarla su `Nothing`.|  
|`Resume Next`|Consente di specificare che, in caso di errore di runtime, il controllo passi all'istruzione immediatamente successiva a quella in cui si è verificato l'errore e l'esecuzione continui da tale punto.  Quando si accede agli oggetti, utilizzare questo form anziché `On Error GoTo`.|  
  
## Note  
  
> [!NOTE]
>  Si consiglia di utilizzare la gestione delle eccezioni strutturata nel codice laddove possibile, anziché utilizzare la gestione delle eccezioni non strutturata e `On Error` istruzione.  Per ulteriori informazioni, vedere [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
 Un gestore errori "abilitato" è quello che viene attivato da un'istruzione `On Error`.  Un gestore errori "attivo", invece, rappresenta un gestore abilitato in procinto di gestire un errore.  
  
 Se si verifica un errore mentre un gestore errori è attivo \(tra l'occorrenza dell'errore e un'istruzione `Resume`, `Exit Sub`, `Exit Function` o `Exit Property`\), il gestore errori della routine corrente non sarà in grado di gestirlo.  Il controllo verrà restituito, quindi, alla routine chiamante.  
  
 Se la routine chiamante dispone di un gestore errori abilitato, esso verrà attivato per provvedere alla gestione dell'errore.  Tuttavia, se è attivo anche il gestore errori della routine, il controllo verrà passato di nuovo alle precedenti routine chiamanti fino al rilevamento di un gestore errori abilitato ma inattivo.  Se il gestore errori non viene trovato, nel punto in cui si è effettivamente verificato l'errore risulta irreversibile.  
  
 Ogni volta che il controllo viene passato nuovamente a una routine chiamante, questa diventerà la routine corrente.  Infine, quando l'errore viene gestito da un gestore errori di qualsiasi routine, l'esecuzione viene ripresa nella routine corrente, dal punto indicato dall'istruzione `Resume`.  
  
> [!NOTE]
>  Una routine di gestione degli errori non corrisponde a una routine `Sub` o `Function`.  Si tratta di una sezione di codice contrassegnata da un'etichetta o da un numero di riga.  
  
## Proprietà Number  
 Per determinare la causa di un errore, le routine di gestione degli errori si basano sul valore della proprietà `Number` dell'oggetto `Err`.  Con la routine, i valori rilevanti delle proprietà dell'oggetto `Err` verranno verificati e salvati prima che venga generato un altro errore o che venga richiamata una routine che possa causare un errore.  I valori delle proprietà dell'oggetto `Err` riflettono solo l'ultimo errore verificatosi.  Il messaggio di errore associato a `Err.Number` è disponibile in `Err.Description`.  
  
## Istruzione Throw  
 Se un errore viene generato con il metodo `Err.Raise`, la proprietà `Exception` viene impostata su un'istanza appena creata della classe <xref:System.Exception>.  Per consentire la generazione di eccezioni di tipi derivati, nel linguaggio è supportata un'istruzione `Throw`.  Tale istruzione richiede un solo parametro, ovvero l'istanza di eccezione da generare.  Nell'esempio seguente viene illustrato come utilizzare queste funzionalità con il supporto esistente per la gestione delle eccezioni:  
  
 [!code-vb[VbVbalrErrorHandling#17](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/on-error-statement_1.vb)]  
  
 Si noti che nell'istruzione `On Error GoTo` vengono intercettati tutti gli errori, indipendentemente dalla classe dell'eccezione.  
  
## On Error Resume Next  
 Se si utilizza `On Error Resume Next`, l'esecuzione prosegue con l'istruzione immediatamente successiva a quella che ha causato l'errore di runtime oppure immediatamente successiva all'ultima chiamata effettuata nella routine contenente l'istruzione `On Error Resume Next`.  Questa istruzione consente di continuare l'esecuzione in caso di errore di runtime.  È possibile inserire la routine di gestione nel punto in cui è possibile che si verifichi l'errore anziché trasferire il controllo in un'altra posizione all'interno della routine.  Un'istruzione `On Error Resume Next` diventa inattiva quando viene richiamata un'altra routine, pertanto, se si desidera una gestione degli errori inline, occorre eseguire un'istruzione `On Error Resume Next` in ciascuna routine chiamata.  
  
> [!NOTE]
>  Per la gestione degli errori generati in fase di accesso ad altri oggetti, è preferibile il costrutto `On Error Resume Next` rispetto a `On Error GoTo`.  Effettuando il controllo di `Err` dopo ciascuna interazione con un oggetto si elimina ogni possibile ambiguità relativa all'oggetto a cui il codice ha avuto accesso.  È possibile conoscere con certezza l'oggetto con cui è stato inserito il codice di errore in `Err.Number`, nonché l'oggetto con cui in origine è stato generato l'errore \(l'oggetto specificato in `Err.Source`\).  
  
## On Error GoTo 0  
 `On Error GoTo 0` consente di disabilitare la gestione delle errori nella routine corrente.  La riga 0 non viene specificata come inizio del codice di gestione degli errori, anche se la routine contiene una riga numerata come 0.  Senza un'istruzione `On Error GoTo 0`, un gestore di errori viene disabilitato automaticamente al termine di una routine.  
  
## On Error GoTo \-1  
 `On Error GoTo -1` consente di disabilitare l'eccezione nella routine corrente.  La riga \-1 non viene specificata come inizio del codice di gestione degli errori, anche se la routine contiene una riga numerata come \-1.  Senza un'istruzione `On Error GoTo -1`, un'eccezione viene disabilitata automaticamente al termine di una routine.  
  
 Per impedire l'esecuzione del codice di gestione degli errori quando non si è verificato alcun errore, inserire un'istruzione `Exit Sub`, `Exit Function` o `Exit Property` immediatamente prima della routine di gestione degli errori, come illustrato nel seguente frammento di codice:  
  
 [!code-vb[VbVbalrErrorHandling#18](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/on-error-statement_2.vb)]  
  
 In questo esempio il codice di gestione degli errori è racchiuso tra le istruzioni `Exit Sub` ed `End Sub`, che lo separano dal flusso della routine.  Il codice di gestione degli errori può essere inserito in un punto qualsiasi della routine.  
  
## Errori non intercettati  
 Gli errori non intercettati negli oggetti vengono restituiti all'applicazione attiva quando l'oggetto viene eseguito come file eseguibile.  All'interno dell'ambiente di sviluppo gli errori non intercettati vengono restituiti all'applicazione di controllo solo se sono state impostate le opzioni adatte.  Per una descrizione delle opzioni da impostare durante il debug e delle relative modalità di impostazione e per determinare se l'host è in grado di creare classi, consultare la documentazione fornita con l'applicazione host.  
  
 Se si crea un oggetto a cui è consentito l’accesso ad altri oggetti, è opportuno tentare di gestire tutti gli eventuali errori non gestiti passati da tali oggetti.  Se ciò non è possibile, associare i codici di errore di `Err.Number` a uno degli errori, quindi passarli nuovamente all'elemento che ha chiamato l'oggetto.  Specificare l'errore aggiungendone il codice alla costante `VbObjectError`.  Se, ad esempio, il codice dell'errore è 1052, assegnarlo come riportato di seguito:  
  
 [!code-vb[VbVbalrErrorHandling#19](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/on-error-statement_3.vb)]  
  
> [!CAUTION]
>  In caso di errori di sistema che si verificano durante le chiamate alle librerie a collegamento dinamico \(DDL, Dynamic\-Link Library\) di Windows, non vengono generate eccezioni. Gli errori, inoltre, non potranno essere rilevati mediante l'intercettazione degli errori di Visual Basic.  Quando si richiamano funzioni di DLL, è opportuno verificare l'esito di ciascun valore restituito \(secondo le specifiche API\) e, in caso di esito negativo, controllare il valore della proprietà `LastDLLError` dell'oggetto `Err`.  
  
## Esempio  
 In questo esempio viene innanzitutto utilizzata l'istruzione `On Error GoTo` per specificare la posizione di una routine di gestione degli errori all'interno di una routine.  Nell'esempio, un tentativo di dividere per zero genera l'errore numero 6.  L'errore viene gestito nella routine di gestione degli errori e il controllo viene quindi restituito all'istruzione che ha causato l'errore.  L'istruzione `On Error GoTo 0` consente di disattivare l'intercettazione degli errori.  Viene quindi utilizzata l'istruzione `On Error Resume Next` per rinviare l'intercettazione degli errori affinché il contesto per l'errore generato dall'istruzione successiva possa essere riconosciuto in modo certo.  `Err.Clear` viene utilizzato per cancellare le proprietà dell'oggetto `Err` una volta gestito l'errore.  
  
 [!code-vb[VbVbalrErrorHandling#20](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/on-error-statement_4.vb)]  
  
## Requisiti  
 **Spazio dei nomi:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **Assembly:** Visual Basic Runtime Library \(in Microsoft.VisualBasic.dll\)  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Information.Err%2A>   
 <xref:Microsoft.VisualBasic.ErrObject.Number%2A>   
 <xref:Microsoft.VisualBasic.ErrObject.Description%2A>   
 <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>   
 [End Statement](../../../visual-basic/language-reference/statements/end-statement.md)   
 [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Resume Statement](../../../visual-basic/language-reference/statements/resume-statement.md)   
 [Error Messages](../../../visual-basic/language-reference/error-messages/index.md)   
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)