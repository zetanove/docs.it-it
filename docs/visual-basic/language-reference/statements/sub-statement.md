---
title: "Istruzione Sub (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Sub"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Parola chiave Public, istruzioni Sub"
  - "procedure, creazione"
  - "dichiarazione di routine, Sub (istruzione)"
  - "argomenti [Visual Basic], Sub (routine)"
  - "Come parola chiave, istruzioni Sub"
  - "Parola chiave facoltativa, istruzioni Sub"
  - "dichiarazioni, procedure"
  - "Sub (parola chiave)"
  - "Parola chiave Handles, istruzioni Sub"
  - "Protected Friend (parola chiave)"
  - "ParamArray (parola chiave), istruzioni Sub"
  - "Parola chiave Implements, istruzioni Sub"
  - "Sub (istruzione)"
  - "subroutine"
  - "ByRef (parola chiave), istruzioni Sub"
  - "Sub (routine), Sub (istruzione)"
  - "routine ricorsive"
  - "Private (parola chiave), istruzioni Sub"
  - "Parola chiave Friend, istruzioni Sub"
  - "Exit (istruzione), istruzioni Sub"
  - "procedure, Sub"
  - "Parola chiave end, istruzioni Sub"
  - "ByVal (parola chiave), istruzioni Sub"
  - "Visual Basic (codice), Sub (routine)"
ms.assetid: e347d700-d06c-405b-b302-e9b1edb57dfc
caps.latest.revision: 52
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 52
---
# Istruzione Sub (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Dichiara il nome, parametri e il codice che definiscono un `Sub` procedura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ <attributelist> ] [ Partial ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async ]  
Sub name [ (Of typeparamlist) ] [ (parameterlist) ] [ Implements implementslist | Handles eventlist ]  
    [ statements ]  
    [ Exit Sub ]  
    [ statements ]  
End Sub  
```  
  
## <a name="parts"></a>Parti  
  
-   `attributelist`  
  
     Facoltativo. Vedere [elenco attributi](../../../visual-basic/language-reference/statements/attribute-list.md).  
  
-   `Partial`  
  
     Facoltativo. Indica la definizione di un metodo parziale. Vedere [metodi parziali](../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md).  
  
-   `accessmodifier`  
  
     Facoltativo. Può essere uno dei seguenti:  
  
    -   [Pubblica](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protetto](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Privato](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   `Protected Friend`  
  
     Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
-   `proceduremodifiers`  
  
     Facoltativo. Può essere uno dei seguenti:  
  
    -   [Overload](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
    -   [Esegue l'override](../../../visual-basic/language-reference/modifiers/overrides.md)  
  
    -   [Sottoponibili a override](../../../visual-basic/language-reference/modifiers/overridable.md)  
  
    -   [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)  
  
    -   [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)  
  
    -   `MustOverride Overrides`  
  
    -   `NotOverridable Overrides`  
  
-   `Shared`  
  
     Facoltativo. Vedere [condivisi](../../../visual-basic/language-reference/modifiers/shared.md).  
  
-   `Shadows`  
  
     Facoltativo. Vedere [ombreggiature](../../../visual-basic/language-reference/modifiers/shadows.md).  
  
-   `Async`  
  
     Facoltativo. Vedere [Async](../../../visual-basic/language-reference/modifiers/async.md).  
  
-   `name`  
  
     Obbligatorio. Nome della routine. Vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md). Per creare una routine di costruttore per una classe, impostare il nome di un `Sub` procedura per la `New` (parola chiave). Per ulteriori informazioni, vedere [la durata degli oggetti: come gli oggetti sono creare e distruggere](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md).  
  
-   `typeparamlist`  
  
     Facoltativo. Elenco di parametri di tipo per una procedura generica. Vedere [digitare elenco](../../../visual-basic/language-reference/statements/type-list.md).  
  
-   `parameterlist`  
  
     Facoltativo. Elenco di nomi di variabili locali che rappresentano i parametri di questa procedura. Vedere [elenco parametri](../../../visual-basic/language-reference/statements/parameter-list.md).  
  
-   `Implements`  
  
     Facoltativo. Indica che questa procedura viene implementato uno o più `Sub` procedure, ognuna definita in un'interfaccia implementata dalla classe o struttura che contiene questa procedura. Vedere [implementa istruzione](../../../visual-basic/language-reference/statements/implements-statement.md).  
  
-   `implementslist`  
  
     Necessario se si fornisce `Implements`. Elenco delle routine `Sub` implementate.  
  
     `implementedprocedure [ , implementedprocedure ... ]`  
  
     Ogni `implementedprocedure` presenta la sintassi e le parti seguenti:  
  
     `interface.definedname`  
  
    |||  
    |-|-|  
    |Parte|Descrizione|  
    |`interface`|Obbligatorio. Nome di un'interfaccia implementata da questa procedura contenente classe o struttura.|  
    |`definedname`|Obbligatorio. Nome mediante il quale la routine viene definita in `interface`.|  
  
-   `Handles`  
  
     Facoltativo. Indica che questa procedura può gestire uno o più eventi specifici. Vedere [gestisce](../../../visual-basic/language-reference/statements/handles-clause.md).  
  
-   `eventlist`  
  
     Necessario se si fornisce `Handles`. Elenco di eventi gestiti dalla routine.  
  
     `eventspecifier [ , eventspecifier ... ]`  
  
     Ogni `eventspecifier` presenta la sintassi e le parti seguenti:  
  
     `eventvariable.event`  
  
    |||  
    |-|-|  
    |Parte|Descrizione|  
    |`eventvariable`|Obbligatorio. Variabile oggetto dichiarata con il tipo di dati della classe o struttura che genera l'evento.|  
    |`event`|Obbligatorio. Nome dell'evento gestito dalla routine.|  
  
-   `statements`  
  
     Facoltativo. Blocco di istruzioni da eseguire all'interno di questa procedura.  
  
-   `End Sub`  
  
     Termina la definizione di questa procedura.  
  
## <a name="remarks"></a>Note  
 Tutto il codice eseguibile deve essere all'interno di una routine. Utilizzare un `Sub` procedure quando non si desidera restituire un valore al codice chiamante. Utilizzare un `Function` procedura quando si desidera restituire un valore.  
  
## <a name="defining-a-sub-procedure"></a>Definizione di una routine Sub  
 È possibile definire un `Sub` procedura solo a livello di modulo. Il contesto della dichiarazione per una routine sub deve, pertanto, essere una classe, una struttura, un modulo o un'interfaccia e non può essere un file di origine, uno spazio dei nomi, una routine o un blocco. Per ulteriori informazioni, vedere [contesti delle dichiarazioni e livelli di accesso predefinito](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 `Sub` Per impostazione predefinita le procedure per l'accesso pubblico. È possibile regolare i livelli di accesso mediante i modificatori di accesso.  
  
 Se la routine utilizza il `Implements` (parola chiave), classe o struttura deve avere un `Implements` istruzione che segue immediatamente il `Class` o `Structure` istruzione. Il `Implements` istruzione deve includere ogni interfaccia specificata in `implementslist`. Tuttavia, il nome con cui l'interfaccia definisce il `Sub` (in `definedname`) non deve necessariamente corrispondere al nome di questa procedura (in `name`).  
  
## <a name="returning-from-a-sub-procedure"></a>Restituzione da una routine Sub  
 Quando un `Sub` procedure restituisce al codice chiamante, l'esecuzione continua con l'istruzione successiva all'istruzione che lo hanno chiamato.  
  
 Nell'esempio seguente viene illustrato un ritorno da una `Sub` procedura.  
  
```vb#  
Sub mySub(ByVal q As String)  
    Return  
End Sub   
```  
  
 Il `Exit Sub` e `Return` istruzioni uscire immediatamente da un `Sub` procedura. Un numero qualsiasi di `Exit Sub` e `Return` istruzioni possono trovarsi in qualsiasi punto della procedura, ed è possibile combinare `Exit Sub` e `Return` istruzioni.  
  
## <a name="calling-a-sub-procedure"></a>Chiamare una routine Sub  
 Si chiama un `Sub` procedure utilizzando il nome della routine in un'istruzione e quindi seguendo questo nome con il relativo elenco di argomenti racchiuso tra parentesi. È possibile omettere le parentesi solo se non si fornisce alcun argomento. Tuttavia, il codice è più leggibile se si includono sempre le parentesi.  
  
 Oggetto `Sub` procedura e un `Function` procedura può avere parametri ed eseguire una serie di istruzioni. Tuttavia, un `Function` procedura restituisce un valore e un `Sub` non di procedura. Pertanto, è possibile utilizzare un `Sub` procedure in un'espressione.  
  
 È possibile utilizzare il `Call` parola chiave quando si chiama un `Sub` procedura, ma la parola chiave non è consigliato per la maggior parte dei casi. Per ulteriori informazioni, vedere [istruzione Call](../../../visual-basic/language-reference/statements/call-statement.md).  
  
 Visual Basic vengono a volte riorganizzate espressioni aritmetiche per aumentare l'efficienza interna. Per questo motivo, se all'elenco di argomenti sono incluse le espressioni che chiamano altre routine, non deve presupporre che le espressioni verranno chiamate in un ordine particolare.  
  
## <a name="async-sub-procedures"></a>Async Sub (routine)  
 Utilizzando la funzionalità Async, è possibile richiamare funzioni asincrone senza utilizzare callback esplicite o suddividere manualmente il codice in più funzioni o espressioni lambda.  
  
 Se si contrassegna una routine con il [Async](../../../visual-basic/language-reference/modifiers/async.md) modificatore, è possibile utilizzare il [Await](../../../visual-basic/language-reference/operators/await-operator.md) operatore nella procedura. Quando il controllo raggiunge un `Await` espressione la `Async` procedura, il controllo ritorna al chiamante e lo stato di avanzamento della procedura viene sospesa fino al completamento dell'attività di attesa. Una volta completata l'attività, nella procedura possibile riprendere l'esecuzione.  
  
> [!NOTE]
>  Un `Async` restituito al chiamante quando viene rilevato un il primo oggetto atteso che non è ancora completo o alla fine della routine di `Async` procedura viene raggiunto, qualunque si verifichi prima.  
  
 È inoltre possibile contrassegnare un [istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md) con il `Async` modificatore. Un `Async` funzione può avere un tipo restituito di <xref:System.Threading.Tasks.Task%601> o <xref:System.Threading.Tasks.Task>. Un esempio più avanti in questo argomento viene illustrato un `Async` che presenta un tipo restituito della funzione <xref:System.Threading.Tasks.Task%601>.  
  
 `Async` `Sub` procedure vengono utilizzate principalmente per i gestori eventi, in cui non può essere restituito un valore. Un `Async``Sub` procedura non può essere atteso e il chiamante di un `Async``Sub` procedura non può intercettare le eccezioni che il `Sub` procedura genera un'eccezione.  
  
 Un `Async` procedura non può dichiarare [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) parametri.  
  
 Per ulteriori informazioni su `Async` procedure, vedere [programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md), [flusso di controllo in programmi asincroni](../Topic/Control%20Flow%20in%20Async%20Programs%20\(C%23%20and%20Visual%20Basic\).md), e [Async restituire tipi](../Topic/Async%20Return%20Types%20\(C%23%20and%20Visual%20Basic\).md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `Sub` istruzione per definire il nome, parametri e il codice che formano il corpo di un `Sub` procedura.  
  
 [!code-vb[VbVbalrStatements#58](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/sub-statement_1.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, `DelayAsync` è un un `Async``Function` che presenta un tipo restituito di <xref:System.Threading.Tasks.Task%601>. `DelayAsync` ha un'istruzione `Return` che restituisce un numero intero. Pertanto, la dichiarazione della funzione di `DelayAsync` deve avere un tipo restituito di `Task(Of Integer)`. Poiché il tipo restituito è `Task(Of Integer)`, la valutazione di `Await` espressione `DoSomethingAsync` produce un numero intero, come illustrato nell'istruzione seguente: `Dim result As Integer = Await delayTask`.  
  
 Il `startButton_Click` procedure è un esempio di un `Async Sub` procedura. Poiché `DoSomethingAsync` è un `Async` (funzione), l'attività per la chiamata a `DoSomethingAsync` deve essere atteso, come illustrato nell'istruzione seguente: `Await DoSomethingAsync()`. Il `startButton_Click``Sub` procedura deve essere definita con la `Async` modificatore perché contiene un `Await` espressione.  
  
 [!code-vb[csAsyncMethod#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/VisualBasic/sub-statement_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Implements (istruzione)](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Elenco di parametri](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Istruzione Call](../../../visual-basic/language-reference/statements/call-statement.md)   
 [Di](../../../visual-basic/language-reference/statements/of-clause.md)   
 [Matrici di parametri](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Procedura: utilizzare una classe generica](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Le procedure di risoluzione](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [Metodi parziali](../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md)