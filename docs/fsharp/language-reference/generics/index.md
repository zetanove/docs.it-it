---
title: Generics (F#)
description: Generics (F#)
keywords: visual f#, f#, programmazione funzionale
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: a9f2e2ee-bcb1-4ce3-8531-850aa183040f
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: 98f65de4f3434aea9ee0b78848b85ba398543974
ms.lasthandoff: 04/05/2017

---

# <a name="generics"></a>Generics

I valori, i metodi, le proprietà delle funzioni F# e i tipi di aggregazione quali classi, record e unioni discriminate possono essere *generici*. I costrutti generici contengono almeno un parametro di tipo, specificato in genere dall'utente del costrutto generico. Le funzioni e i tipi generici consentono di scrivere codice che può essere usato con un'ampia gamma di tipi senza ripetere il codice per ogni tipo. In F# è possibile rendere generico un codice in maniera semplice, perché spesso il codice viene dedotto in modo implicito come generico dall'inferenza del tipo di compilatore e dai meccanismi di generalizzazione automatica.


## <a name="syntax"></a>Sintassi

```fsharp
// Explicitly generic function.
let function-name<type-parameters> parameter-list =
function-body

// Explicitly generic method.
[ static ] member object-identifer.method-name<type-parameters> parameter-list [ return-type ] =
method-body

// Explicitly generic class, record, interface, structure,
// or discriminated union.
type type-name<type-parameters> type-definition
```

## <a name="remarks"></a>Note
La dichiarazione di una funzione o di un tipo esplicitamente generico è molto simile a quella di una funzione o di un tipo non generico, ad eccezione per la specifica (e uso) dei parametri di tipo, che si trovano in parentesi acute dopo il nome della funzione o del tipo.

Le dichiarazioni sono spesso implicitamente generiche. Se non si specifica completamente il tipo di ogni parametro usato per creare una funzione o un tipo, il compilatore prova a dedurre il tipo di ogni parametro, del valore e della variabile dal codice scritto. Per altre informazioni, vedere [Type Inference](../type-inference.md) (Inferenza del tipo). Se il codice per il tipo o per la funzione non vincola i tipi di parametri, la funzione o il tipo è implicitamente generico. Questo processo è denominato *generalizzazione automatica*. Ci sono alcuni limiti per la generalizzazione automatica. Ad esempio, se il compilatore F# non è in grado di dedurre i tipi per un costrutto generico, segnala un errore che fa riferimento a una limitazione definita *limitazione valore*. In tal caso, potrebbe essere necessario aggiungere alcune annotazioni di tipo. Per altre informazioni sulla generalizzazione automatica e la limitazione valori e su come modificare il codice per risolvere il problema, vedere [Generalizzazione automatica](automatic-generalization.md).

Nella sintassi precedente, *type-parameters* (parametri_tipo) è un elenco delimitato da virgole di parametri che rappresentano tipi sconosciuti, ognuno dei quali inizia con una virgoletta singola, facoltativamente con una clausola di vincolo che limita ulteriormente i tipi che possono essere usati per il parametro di tipo. Per informazioni sui vincoli e sulla sintassi per le clausole di vincolo di vari tipi, vedere [Vincoli](constraints.md).

*type-definition* (definizione_tipo) nella sintassi è identica alla definizione del tipo per un tipo non generico. Include i parametri del costruttore per un tipo di classe, una clausola `as` facoltativa, il simbolo di uguaglianza, i campi di record, la clausola `inherit`, le opzioni per un'unione discriminata, le associazioni `let` e `do`, le definizioni dei membri e altri elementi consentiti in una definizione di tipo non generico.

Gli altri elementi di sintassi sono gli stessi di quelli per le funzioni e i tipi non generici. Ad esempio, *object-identifier* (identificatore_oggetto) è un identificatore che rappresenta l'oggetto che contiene se stesso.

Le proprietà, i campi e i costruttori non possono essere più generici del tipo che li contiene. I valori in un modulo non possono essere generici.


## <a name="implicitly-generic-constructs"></a>Costrutti implicitamente generici
Quando il compilatore F# deduce i tipi nel codice, considera automaticamente come generica qualsiasi funzione che può essere generica. Se si specifica un tipo in modo esplicito, ad esempio un tipo di parametro, si evita la generalizzazione automatica.

Nell'esempio di codice seguente, `makeList` è generico, anche se il codice e i relativi parametri non sono dichiarati esplicitamente come generici.

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet1700.fs)]

La firma della funzione viene dedotta come `'a -> 'a -> 'a list`. Si noti che `a` e `b` in questo esempio vengono considerati come elementi dello stesso tipo. Ciò si verifica perché sono inclusi nello stesso elenco e tutti gli elementi di un elenco devono essere dello stesso tipo.

È anche possibile rendere una funzione generica usando la sintassi con virgoletta singola in un'annotazione di tipo per indicare che un tipo di parametro è un parametro di tipo generico. Nel codice seguente, `function1` è generico perché i parametri vengono dichiarati in questo modo, come parametri di tipo.

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet1701.fs)]
    
## <a name="explicitly-generic-constructs"></a>Costrutti esplicitamente generici
È anche possibile rendere una funzione generica dichiarando in modo esplicito i parametri di tipo in parentesi acute (`<type-parameter>`). Questa condizione è illustrata nel codice che segue.

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet1703.fs)]
    
## <a name="using-generic-constructs"></a>Uso di costrutti generici
Quando si usano funzioni o metodi generici, potrebbe non essere necessario specificare gli argomenti di tipo. Il compilatore usa l'inferenza del tipo per dedurre gli argomenti di tipo appropriato. Se c'è ancora ambiguità, è possibile specificare gli argomenti di tipo in parentesi acute, separando più argomenti di tipo con una virgola.

Il codice seguente illustra l'uso delle funzioni definite nelle sezioni precedenti.

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet1702.fs)]
    
>[!NOTE]
Ci sono due modi per fare riferimento a un tipo generico in base al nome. Ad esempio, `list<int>` e `int list` sono due modi per fare riferimento a un tipo generico `list` che ha un solo argomento di tipo `int`. La seconda forma viene comunemente usata solo con i tipi F# predefiniti, ad esempio `list` e `option`. Se ci sono più argomenti di tipo, in genere si usa la sintassi `Dictionary<int, string>` ma è anche possibile usare la sintassi `(int, string) Dictionary`.

## <a name="wildcards-as-type-arguments"></a>Caratteri jolly come argomenti di tipo
Per specificare che un argomento di tipo deve essere dedotto dal compilatore, è possibile usare il carattere di sottolineatura o un carattere jolly (`_`), anziché un argomento di tipo denominato. Questo comportamento viene illustrato nel codice seguente.

[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet1704.fs)]
    
## <a name="constraints-in-generic-types-and-functions"></a>Vincoli in funzioni e tipi generici
In una definizione di funzione o tipo generico, è possibile usare solo questi costrutti disponibili nel parametro di tipo generico. Ciò è necessario per abilitare la verifica delle chiamate di funzioni e metodi in fase di compilazione. Se si dichiarano in modo esplicito i parametri di tipo, è possibile applicare un vincolo esplicito a un parametro di tipo generico per notificare al compilatore che sono disponibili alcuni metodi e funzioni. Se tuttavia si consente al compilatore F# di dedurre i tipi di parametri generici, il compilatore determinerà i vincoli appropriati. Per altre informazioni, vedere [Vincoli](constraints.md).


## <a name="statically-resolved-type-parameters"></a>Parametri di tipo risolti staticamente
Ci sono due tipi di parametri di tipo che possono essere usati in programmi F#. Il primo tipo include parametri di tipo generico del tipo descritto nelle sezioni precedenti. Il primo tipo di parametro di tipo è equivalente ai parametri di tipo generico che vengono usati in linguaggi quali Visual Basic e C#. Un altro tipo di parametro di tipo è specifico di F# e viene definito come *parametro di tipo risolto staticamente*. Per informazioni su questi costrutti, vedere [Statically Resolved Type Parameters](statically-resolved-type-parameters.md) (Parametri di tipo risolti staticamente).


## <a name="examples"></a>Esempi
[!code-fsharp[Principale](../../../../samples/snippets/fsharp/lang-ref-1/snippet1705.fs)]
    
## <a name="see-also"></a>Vedere anche
[Riferimenti per il linguaggio](../index.md)

[Tipi](../fsharp-types.md)

[Parametri di tipo risolti staticamente](statically-resolved-type-parameters.md)

[Generics in .NET Framework](https://msdn.microsoft.com/library/ms172192.aspx)

[Generalizzazione automatica](automatic-generalization.md)

[Vincoli](constraints.md)
