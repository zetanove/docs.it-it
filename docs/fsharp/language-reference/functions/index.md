---
title: Funzioni (F#)
description: Funzioni (F#)
keywords: visual f#, f#, programmazione funzionale
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 6dea2c3e-2f9d-4c9d-97a2-d8f9a72b6f4c
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: 7a5fff4746157b430c6f1a492c23e9ea3d7b82c3
ms.lasthandoff: 04/05/2017

---

# <a name="functions"></a>Funzioni

Le funzioni sono l'unità fondamentale di esecuzione di un programma in qualsiasi linguaggio di programmazione. Come negli altri linguaggi, una funzione F# ha un nome, può avere parametri e accettare argomenti e ha un corpo. F# supporta anche i costrutti di programmazione funzionale, ad esempio l'uso di funzioni come valori, l'uso di funzioni senza nome nelle espressioni, composizione di funzioni per creare nuove funzioni, funzioni sottoposte a currying e la definizione implicita di funzioni attraverso l'applicazione parziale di argomenti di funzioni.

Le funzioni vengono definite tramite la parole chiave `let` oppure, se la funzione è ricorsiva, tramite la combinazione di parole chiave `let rec`.


## <a name="syntax"></a>Sintassi

```fsharp
// Non-recursive function definition.
let [inline] function-name parameter-list [ : return-type ] = function-body
// Recursive function definition.
let rec function-name parameter-list = recursive-function-body
```

## <a name="remarks"></a>Note
*Function-name* (nome_funzione) è un identificatore che rappresenta la funzione. *Parameter-list* (elenco_parametri) consiste di parametri successivi separati da spazi. È possibile specificare un tipo esplicito per ogni parametro, come illustrato nella sezione Parametri. Se non si specifica un tipo di argomento specifico, il compilatore prova a dedurre il tipo dal corpo della funzione. *Function-body* (corpo_funzione) è costituito da un'espressione. L'espressione che costituisce il corpo della funzione è in genere un'espressione composta che consiste di un numero di espressioni che terminano con un'espressione finale, che è il valore restituito. *Return-type* (tipo_restituito) è rappresentato dai due punti seguiti da un tipo ed è facoltativo. Se non si specifica il tipo del valore restituito in modo esplicito, il compilatore determina il tipo restituito dall'espressione finale.

Una definizione di funzione semplice è simile alla seguente:

```fsharp
let f x = x + 1
```

Nell'esempio precedente, il nome della funzione è `f`, l'argomento è `x` ed è di tipo `int`, il corpo della funzione è `x + 1` e il valore restituito è di tipo `int`.

Le funzioni possono essere contrassegnate `inline`. Per informazioni su `inline`, vedere [Funzioni inline](../functions/inline-functions.md).


## <a name="scope"></a>Ambito
A qualsiasi livello di ambito diverso dall'ambito del modulo, non è un errore riusare un nome di funzione o un valore. Se si riusa un nome, il nome dichiarato successivamente sostituisce il nome dichiarato in precedenza. Tuttavia, nell'ambito di livello superiore in un modulo, i nomi devono essere univoci. Ad esempio, il codice seguente genera un errore quando viene visualizzato nell'ambito del modulo, ma non quando viene visualizzato all'interno di una funzione:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet101.fs)]

Ma il codice seguente è accettabile a qualsiasi livello di ambito:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet102.fs)]
    
#### <a name="parameters"></a>Parametri
I nomi dei parametri vengono elencati dopo il nome della funzione. È possibile specificare un tipo per un parametro, come illustrato nell'esempio seguente:

```fsharp
let f (x : int) = x + 1
```

Se si specifica un tipo, questo segue il nome del parametro ed è separato dal nome da due punti. Se si omette il tipo per il parametro, questo viene dedotto dal compilatore. Ad esempio, nella definizione della funzione seguente, l'argomento `x` viene dedotto come tipo `int` perché 1 è di tipo `int`.

```fsharp
let f x = x + 1
```

Tuttavia, il compilatore proverà a creare la funzione nel modo più generico possibile. Ad esempio, si noti il codice seguente:

```fsharp
let f x = (x, x)
```

La funzione crea una tupla da un argomento di qualsiasi tipo. Poiché il tipo non è specificato, la funzione può essere usata con qualsiasi tipo di argomento. Per altre informazioni, vedere [Generalizzazione automatica](../generics/automatic-generalization.md).


## <a name="function-bodies"></a>Corpi di funzioni
Un corpo di funzione può contenere definizioni di funzioni e variabili locali. Tali funzioni e variabili rientrano nell'ambito del corpo della funzione corrente ma non al suo esterno. Dopo aver abilitato l'opzione di sintassi leggera, è necessario usare un rientro per indicare che una definizione è in un corpo della funzione, come illustrato nell'esempio seguente:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet103.fs)]

Per altre informazioni, vedere [Code Formatting Guidelines](../code-formatting-guidelines.md) (Linee guida per la formattazione del codice) e [Verbose Syntax](../verbose-syntax.md) (Sintassi dettagliata).


## <a name="return-values"></a>Valori restituiti
Il compilatore usa l'espressione finale in un corpo di funzione per determinare il valore restituito e il tipo. Il compilatore può dedurre il tipo dell'espressione finale dalle espressioni precedenti. Nella funzione `cylinderVolume`, come illustrato nella sezione precedente, il tipo di `pi` è determinato dal tipo di valore letterale `3.14159` come `float`. Per determinare il tipo dell'espressione `h * pi * r * r` come `float`, il compilatore usa il tipo di `pi`. Pertanto, il tipo restituito completo della funzione è `float`.

Per specificare in modo esplicito il valore restituito, scrivere il codice nel modo seguente:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet105.fs)]

Analogamente al codice scritto in precedenza, il compilatore applica **float** all'intera funzione; se si vuole applicarlo anche ai tipi di parametro, usare il codice seguente:

```fsharp
let cylinderVolume (radius : float) (length : float) : float
```

## <a name="calling-a-function"></a>Chiamata di una funzione
Le funzioni vengono chiamate specificando il nome della funzione seguito da uno spazio e quindi dagli argomenti separati da spazi. Ad esempio, per chiamare la funzione **cylinderVolume** e assegnare il risultato al valore **vol**, scrivere il codice seguente:

```fsharp
let vol = cylinderVolume 2.0 3.0
```

## <a name="partial-application-of-arguments"></a>Applicazione parziale degli argomenti
Se si specifica un numero di argomenti inferiore al numero specificato, si crea una nuova funzione che prevedere gli argomenti rimanenti. Questo metodo di gestione degli argomenti è detto *currying* ed è una caratteristica dei linguaggi di programmazione funzionale come F#. Ad esempio, si supponga di usare due dimensioni per un tubo: una ha un raggio di **2** e l'altra ha un raggio di **3**. È possibile creare funzioni che determinano il volume del tubo nel modo seguente:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet106.fs)]

Verrà quindi specificato l'argomento aggiuntivo necessario per varie lunghezze del tubo delle due dimensioni diverse:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet107.fs)]
    
## <a name="recursive-functions"></a>Funzioni ricorsive
Le *funzioni ricorsive* sono funzioni che chiamano se stesse. Richiedono di specificare la parola chiave **rec** seguita dalla parola chiave **let**. È possibile richiamare la funzione ricorsiva dall'interno del corpo della funzione esattamente come si richiama qualsiasi chiamata di funzione. La funzione ricorsiva seguente calcola il numero di Fibonacci *n*. La sequenza dei numeri di Fibonacci è nota dall'antichità ed è una sequenza in cui ogni numero successivo è la somma di due numeri precedenti nella sequenza.

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet108.fs)]

Alcune funzioni ricorsive potrebbero includere un overflow dello stack di programma o risultare inefficienti se non vengono scritte con cura e con tecniche speciali, come l'uso di accumulatori e continuazioni.


## <a name="function-values"></a>Valori della funzione
In F#, tutte le funzioni sono considerate valori, e infatti sono note come *valori di funzione*. Poiché le funzioni sono valori, possono essere usate come argomenti per altre funzioni o in altri contesti in cui vengono usati valori. Di seguito è incluso un esempio di una funzione che accetta un valore di funzione come argomento:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet109.fs)]

Il tipo di valore di una funzione viene specificato usando il token `->`. Sul lato sinistro di questo token si trova il tipo dell'argomento e sul lato destro si trova il valore restituito. Nell'esempio precedente, `apply1` è una funzione che accetta una funzione `transform` come argomento, in cui `transform` è una funzione che accetta un numero intero e restituisce un altro numero intero. L'esempio di codice seguente illustra come usare `apply1`:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet110.fs)]

Il valore di `result` sarà 101 dopo l'esecuzione del codice precedente.

Più argomenti sono separati da token `->` successivi, come illustrato nell'esempio seguente:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet111.fs)]

Il risultato è 200.


## <a name="lambda-expressions"></a>Espressioni lambda
Un'*espressione lambda* è una funzione senza nome. Negli esempi precedenti, invece di definire le funzioni denominate **increment** e **mul**, è possibile usare espressioni lambda nel modo seguente:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet112.fs)]

Le espressioni lambda vengono definite usando la parola chiave `fun`. Un'espressione lambda è simile a una definizione di funzione, con la differenza che al posto del token `=`, viene usato il token `->` per separare l'elenco di argomenti dal corpo della funzione. Analogamente a una definizione di funzione regolare, i tipi di argomenti possono essere dedotti o specificati in modo esplicito e il tipo restituito dell'espressione lambda viene dedotto dal tipo dell'ultima espressione nel corpo. Per altre informazioni, vedere [Espressioni lambda: parola chiave `fun`](../functions/lambda-expressions-the-fun-keyword.md).


## <a name="function-composition-and-pipelining"></a>Composizione di funzioni e pipelining
Le funzioni in F# possono essere composte da altre funzioni. La composizione di due funzioni, **funzione1** e **funzione2**, è un'altra funzione che rappresenta l'applicazione di **funzione1** seguita dall'applicazione di **funzione2**:

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet113.fs)]

Il risultato è 202.

Il pipelining consente alle chiamate di funzioni di essere concatenate come operazioni successive. Il pipelining funziona nel modo seguente:

```fsharp
let result = 100 |> function1 |> function2
```

Il risultato è di nuovo 202.

Gli operatori di composizione accettano due funzioni e restituiscono una funzione; al contrario, gli operatori pipeline accettano una funzione e un argomento e restituiscono un valore. L'esempio di codice seguente illustra la differenza tra gli operatori di pipeline e di composizione visualizzando le differenze nelle firme di funzione e nell'uso.

```fsharp
// Function composition and pipeline operators compared.

let addOne x = x + 1
let timesTwo x = 2 * x

// Composition operator
// ( >> ) : ('T1 -> 'T2) -> ('T2 -> 'T3) -> 'T1 -> 'T3
let Compose2 = addOne >> timesTwo

// Backward composition operator
// ( << ) : ('T2 -> 'T3) -> ('T1 -> 'T2) -> 'T1 -> 'T3
let Compose1 = addOne << timesTwo

// Result is 5
let result1 = Compose1 2

// Result is 6
let result2 = Compose2 2

// Pipelining
// Pipeline operator
// ( <| ) : ('T -> 'U) -> 'T -> 'U
let Pipeline1 x = addOne <| timesTwo x

// Backward pipeline operator
// ( |> ) : 'T1 -> ('T1 -> 'U) -> 'U
let Pipeline2 x = addOne x |> timesTwo

// Result is 5
let result3 = Pipeline1 2

// Result is 6
let result4 = Pipeline2 2
```

## <a name="overloading-functions"></a>Overload delle funzioni
È possibile eseguire l'overload di metodi di un tipo, ma non di funzioni. Per altre informazioni, vedere [Metodi](../members/methods.md).


## <a name="see-also"></a>Vedere anche
[Valori](../values/index.md)

[Riferimenti per il linguaggio F#](../index.md)

