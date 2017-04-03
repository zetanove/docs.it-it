---
title: Criteri di ricerca | Guida a C#
description: Informazioni sulle espressioni di criteri di ricerca in C#
keywords: .NET, .NET Core, C#
ms.date: 01/24/2017
ms.author: wiwagn
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 1e575c32-2e2b-4425-9dca-7d118f3ed15b
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c5b1ef4b6de108e2ea3967630e9e37e52a97245c
ms.lasthandoff: 03/13/2017

---

# <a name="pattern-matching"></a>Criteri di ricerca #

I criteri verificano che un valore abbia una determinata *forma* e possono *estrarre* informazioni dal valore quando ha la forma corrispondente. I criteri di ricerca offrono una sintassi più concisa per gli algoritmi già in uso. Usando la sintassi esistente vengono già creati algoritmi di criteri di ricerca. Vengono scritte istruzioni `if` o `switch` che testano i valori. Quindi, quando le istruzioni corrispondono, si estraggono e si usano le informazioni del valore. I nuovi elementi di sintassi sono estensioni di istruzioni già note: `is` e `switch`. Queste nuove estensioni associano il test di un valore all'estrazione delle informazioni.

In questo argomento viene descritta la nuova sintassi per illustrare come creare codice leggibile e conciso. I criteri di ricerca consentono di usare termini in cui dati e codice sono separati, a differenza delle progettazioni orientate a oggetti in cui i dati e i metodi che li modificano sono strettamente associati.

Per descrivere questi nuovi termini, verranno usate strutture che rappresentano forme geometriche usando istruzioni di criteri di ricerca. È probabile che si abbia già acquisito dimestichezza con la compilazione delle gerarchie di classi e la creazione di [metodi virtuali e metodi sottoposti a override](methods.md#inherited) per personalizzare il comportamento degli oggetti in base al tipo di runtime dell'oggetto.

Queste tecniche non sono possibili con dati che non sono strutturati in una gerarchia di classi. Quando dati e metodi sono separati, è necessario usare altri strumenti. I costrutti dei nuovi *criteri di ricerca* offrono una sintassi più chiara per esaminare i dati e modificare il flusso di controllo in base a qualsiasi condizione dei dati. Si scrivono già istruzioni `if` e `switch` che testano il valore di una variabile. Si scrivono istruzioni `is` che testano il tipo di una variabile. I *criteri di ricerca* aggiungono nuove funzionalità alle istruzioni.

In questo argomento verrà creato un metodo che calcola l'area di diverse forme geometriche. L'operazione verrà tuttavia eseguita senza ricorrere a tecniche orientate a oggetti compilare una gerarchia di classi per le diverse forme.
Verranno usati invece i *criteri di ricerca*. Per sottolineare ulteriormente che non verrà usata l'ereditarietà, ogni forma verrà specificata come `struct` anziché come classe. Si noti che poiché tipi `struct` diversi non possono specificare un tipo di base comune definito dall'utente, l'ereditarietà non è una progettazione possibile.
Procedendo nell'esempio, confrontare il codice a un eventuale codice strutturato come gerarchia di oggetti. Quando i dati in cui è necessario eseguire le query e che devono essere modificati non sono costituiti da una gerarchia di classi, i criteri di ricerca offrono progettazioni molto eleganti.

Anziché iniziare con una definizione della forma astratta e l'aggiunta di diverse classi di forme specifiche, iniziare con definizioni di soli dati semplici per ogni forma geometrica:

[!code-csharp[ShapeDefinitions](../../samples/csharp/PatternMatching/Shapes.cs#01_ShapeDefinitions "Definizioni delle forme")]

Da queste strutture scrivere un metodo che calcola l'area di una forma.

## <a name="the-is-type-pattern-expression"></a>Espressione del criterio di tipo `is`

Prima di C# 7, era necessario testare ogni tipo di una serie di istruzioni `if` e `is`:

[!code-csharp[ClassicIsExpression](../../samples/csharp/PatternMatching/GeometricUtilities.cs#02_ClassicIsExpression "Criteri di tipo classico che usano is")]

Il codice precedente è un'espressione classica del *criterio di tipo*: si esegue il test di una variabile per determinarne il tipo ed eseguire un'azione diversa in base al tipo.

Questo codice diventa più semplice con l'uso di estensioni dell'espressione `is` per l'assegnazione di una variabile se il test ha esito positivo:

[!code-csharp[IsPatternExpression](../../samples/csharp/PatternMatching/GeometricUtilities.cs#03_IsPatternExpression "Espressione del criterio is")]

In questa versione aggiornata l'espressione `is` esegue il test della variabile e la assegna a una nuova variabile del tipo appropriato. Si noti anche che questa versione include il tipo `Rectangle` che è uno `struct`. La nuova espressione `is` può essere usata con tipi di valore e tipi di riferimento.

Le regole del linguaggio per i criteri di ricerca consentono di evitare un uso errato dei risultati di un'espressione di confronto. Nell'esempio precedente le variabili `s`,  `c` e `r` sono nell'ambito e assegnate definitivamente solo quando le relative espressioni di criteri di ricerca hanno risultati `true`. Se si tenta di usare una variabile in un altro percorso, il codice genera errori del compilatore.

Vengono ora esaminate entrambe le regole nel dettaglio iniziando con l'ambito. La variabile `c` è nell'ambito solo nel ramo `else` della prima istruzione `if`. La variabile `s` è nell'ambito nel metodo `ComputeArea`. Ciò accade perché ogni ramo di un'istruzione `if` definisce un ambito separato per le variabili. Tuttavia, l'istruzione `if` stessa non esegue questa operazione. Ciò significa che le variabili dichiarate nell'istruzione `if` sono nello stesso ambito dell'istruzione `if` (in questo caso, il metodo). Questo comportamento non è specifico dei criteri di ricerca, ma è il comportamento definito per gli ambiti delle variabili e le istruzioni `if` e `else`.

Le variabili `c` e `s` vengono assegnate quando le rispettive istruzioni `if` sono vere a causa del meccanismo di assegnazione definitiva quando sono vere.

> [!TIP]
> Gli esempi di questo argomento usano il costrutto consigliato dove un'espressione `is` di criteri di ricerca assegna in modo definitivo la variabile di corrispondenza nel ramo `true` dell'istruzione `if`.
> È possibile invertire la logica affermando che `if (!(shape is Square s))` e la variabile `s` vengono assegnate definitivamente solo nel ramo `false`. Sebbene sia valido in C#, questo approccio non è consigliabile poiché risulta più complesso seguire la logica.

Queste regole comportano l'impossibilità di accedere accidentalmente al risultato di un'espressione di criteri di ricerca quando i criteri non vengono soddisfatti.

## <a name="using-pattern-matching-switch-statements"></a>Uso di istruzioni `switch` di criteri di ricerca

È possibile sia necessario in seguito supportare altri tipi di forme. Man mano che aumenta il numero di condizioni da testare, l'uso di espressioni di criteri di ricerca `is` può risultare troppo complesso. Oltre a richiedere istruzioni `if` in ogni tipo da controllare, le espressioni `is` sono limitate all'esecuzione di test se l'input corrisponde a un singolo tipo. In questo caso, le espressioni di criteri di ricerca `switch` risultano una scelta migliore. 

L'istruzione `switch` tradizionale era un'espressione di criteri che supportava i criteri costanti.
Era possibile confrontare una variabile con qualsiasi costante in un'istruzione `case`:

[!code-csharp[ClassicSwitch](../../samples/csharp/PatternMatching/GeometricUtilities.cs#04_ClassicSwitch "Istruzione switch classica")]

Gli unici criteri supportati dall'istruzione `switch` erano i criteri costanti. Era presente un'ulteriore limitazione ai tipi numerici e al tipo `string`.
Queste limitazioni sono state rimosse ed è ora possibile scrivere un'istruzione `switch` usando i criteri di tipo:

[!code-csharp[Switch Type Pattern](../../samples/csharp/PatternMatching/GeometricUtilities.cs#05_SwitchTypePattern "Calcolo con l'espressione 'switch'")]

L'istruzione `switch` di criteri di ricerca usa una sintassi già nota agli sviluppatori che hanno usato l'istruzione `switch` di tipo C. Viene valutata ogni istruzione `case` e viene eseguito il codice sottostante la condizione che corrisponde alla variabile di input. L'esecuzione del codice non può "passare" da un'espressione case alla successiva. La sintassi dell'istruzione `case` richiede che ogni `case` termini con `break`, `return` o `goto`.

> [!NOTE]
> Le istruzioni `goto` per il passaggio a un'altra etichetta sono valide solo per il criterio costante, l'istruzione switch classica.

L'istruzione `switch` è governata da nuove regole importanti. Le limitazioni al tipo della variabile nell'espressione `switch` sono state rimosse.
È possibile usare tutti i tipi, ad esempio `object`. Le espressioni case non sono più limitate ai valori costanti. La rimozione di questa limitazione significa che la ridisposizione delle sezioni `switch` può modificare il comportamento di un programma.

Quando sono limitate ai valori costanti, solo un'etichetta `case` può corrispondere al valore dell'espressione `switch`. Se a questo si aggiungeva la regola per la quale ogni sezione `switch` non doveva passare alla sezione successiva ne conseguiva che le sezioni `switch` potevano essere ridisposte in qualsiasi ordine senza effetti sul comportamento.
Ora, con espressioni `switch` più generalizzate, l'ordine di ogni sezione è rilevante. Le espressioni `switch` vengono valutate in ordine testuale. L'esecuzione si trasferisce alla prima etichetta `switch` che corrisponde all'espressione `switch`.  
Si noti che il caso `default` verrà eseguito solo se non corrispondano altre etichette case. Il caso `default` viene valutato per ultimo, indipendentemente dall'ordine testuale. Se non è presente alcun caso `default` e nessuna delle altre istruzioni `case` corrisponde, l'esecuzione continua con l'istruzione che segue l'istruzione `switch`. Non viene eseguito il codice di alcuna etichetta `case`.

## <a name="when-clauses-in-case-expressions"></a>Clausole `when` nelle espressioni `case`

È possibile creare casi speciali per le forme con area 0 usando una clausola `when` nell'etichetta `case`. Un quadrato con una lunghezza del lato pari a 0 o un cerchio con raggio pari a 0 ha un'area 0. Questa condizione viene specificata usando una clausola `when` nell'etichetta `case`:  

[!code-csharp[ComputeDegenerateShapes](../../samples/csharp/PatternMatching/GeometricUtilities.cs#07_ComputeDegenerateShapes "Calcolo di forme con area 0")]

Questa modifica illustra alcune considerazioni importanti sulla nuova sintassi. Innanzitutto, è possibile applicare più etichette `case` a una sezione `switch`. Il blocco di istruzioni viene eseguito quando una delle etichette è `true`. In questa istanza se l'espressione `switch` è un cerchio o un quadrato con area 0, il metodo restituisce la costante 0.

Questo esempio illustra due variabili diverse in due etichette `case` per il primo blocco `switch`. Si noti che le istruzioni in questo blocco `switch` non usano la variabile `c` per il cerchio o `s` per il quadrato.
Nessuna delle variabili è assegnata in modo definitivo in questo blocco `switch`.
Se uno di questi casi corrisponde, significa che una delle variabili è stata assegnata.
Tuttavia, non è possibile sapere *quale* variabile è stata assegnata in fase di compilazione poiché entrambi i casi possono corrispondere in fase di esecuzione. Per questo motivo, nella maggior parte dei casi in cui vengono usate più etichette `case` per lo stesso blocco, non verrà introdotta una nuova variabile nell'istruzione `case` o verrà usata solo la variabile nella clausola `when`.

Dopo aver aggiunto le forme con area 0, si aggiungono due tipi di forme aggiuntivi, un rettangolo e un triangolo:

[!code-csharp[AddRectangleAndTriangle](../../samples/csharp/PatternMatching/GeometricUtilities.cs#09_AddRectangleAndTriangle "Aggiunta di rettangolo e triangolo")]

 Questo set di modifiche aggiunge etichette `case` per il caso degenere ed etichette e blocchi per ogni nuova forma. 

È possibile infine aggiungere un caso `null` per assicurarsi che l'argomento non sia `null`:

[!code-csharp[NullCase](../../samples/csharp/PatternMatching/GeometricUtilities.cs#10_NullCase "Aggiunta del caso null")]

Il caso particolare del criterio `null` è interessante poiché la costante `null` non ha un tipo ma può essere convertita in qualsiasi tipo di riferimento o nullable. 

## <a name="conclusions"></a>Conclusioni

I *costrutti dei criteri di ricerca* consentono di gestire in modo semplice il flusso di controllo tra variabili e tipi diversi non correlati a una gerarchia di ereditarietà. È anche possibile controllare la logica per usare qualsiasi condizione testata sulla variabile. Sono anche disponibili criteri e termini che è possibile usare per compilare applicazioni più distribuite, dove i dati e i metodi che modificano i dati sono separati. Sarà possibile notare che gli struct delle forme usati nell'esempio non contengono metodi, ma solo proprietà di sola lettura.
I criteri di ricerca possono essere usati con qualsiasi tipo di dati. Vengono scritte espressioni che esaminano l'oggetto ed eseguono decisioni per il flusso di controllo in base alle condizioni.

Confrontare il codice dell'esempio con la progettazione che deriverebbe dalla creazione di una gerarchia di classi per una `Shape` astratta e le forme derivate specifiche ognuna con la propria implementazione di un metodo virtuale per il calcolo dell'area. Spesso sarà possibile osservare che le espressioni di criteri di ricerca possono essere uno strumento utile quando si usano dati e si vogliono separare le esigenze di archiviazione di dati da quelle di comportamento.


