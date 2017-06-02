---
title: Membri con corpo di espressione (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- expression-bodied members[C#]
- C# language, expresion-bodied members
author: rpetrusha
ms.author: ronpet
ms.translationtype: Human Translation
ms.sourcegitcommit: a5ed524a1b17f7be8903f998cbd732594faab831
ms.openlocfilehash: b77f656d36dc4f0a715755e13bfcd6c3515c697b
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="expression-bodied-members-c-programming-guide"></a>Membri con corpo di espressione (Guida per programmatori C#)
Le definizioni dei corpi di espressione consentono di eseguire l'implementazione di un membro in un modulo molto conciso e leggibile. È possibile usare una definizione di corpo di espressione ogni volta che la logica per un membro supportato, ad esempio un metodo o proprietà, è costituita da un'unica espressione. Una definizione di corpo di espressione presenta la seguente sintassi generale:

```csharp
member => expression;
```

dove *expression* è un'espressione valida. 

Il supporto per le definizioni dei corpi di espressione è stato introdotto per i metodi e le funzioni di accesso Property Get in C# 6 ed è stato ampliato in C# 7. Le definizioni dei corpi di espressione possono essere usate con i membri dei tipi elencati nella tabella seguente: 

|Membro  |Supportato a partire da... |
|---------|---------|
|[Metodo](#methods)  |C# 6 |
|[Costruttore](#constructors)   |C# 7 |
|[Finalizzatore](#finalizers)     |C# 7 |
|[Property Get](#property-get-statements)  |C# 6 |
|[Property Set](#property-set-statements)  |C# 7 |
|[Indicizzatore](#indexers)       |C# 7 |

## <a name="methods"></a>Metodi

Un metodo con corpo di espressione è costituito da una singola espressione che restituisce un valore il cui tipo corrisponde al tipo restituito del metodo oppure, per i metodi che restituiscono `void`, che esegue una determinata operazione. Ad esempio, i tipi che eseguono l'override del metodo <xref:System.Object.ToString%2A> di solito includono una singola espressione che restituisce la rappresentazione di stringa dell'oggetto corrente. 

L'esempio seguente definisce una classe `Person` che esegue l'override del metodo <xref:System.Object.ToString%2A> con una definizione di corpo di espressione. Definisce inoltre un metodo `Show` che visualizza un nome nella console. Si noti che la parola chiave `return` non viene usata nella definizione del corpo di espressione `ToString`.

[!code-cs[expression-bodied-methods](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-methods.cs)]  

Per altre informazioni, vedere [Metodi (Guida per programmatori C#)](../classes-and-structs/methods.md).
 
## <a name="constructors"></a>Costruttori

Una definizione di corpo di espressione per un costruttore in genere è costituita da una singola espressione di assegnazione o da una chiamata al metodo che gestisce gli argomenti del costruttore o inizializza lo stato dell'istanza. 

L'esempio seguente definisce una classe `Location` il cui costruttore ha un solo parametro di stringa denominato *name*. La definizione del corpo dell'espressione assegna l'argomento alla proprietà `Name`.

[!code-cs[expression-bodied-constructor](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-ctor.cs#1)]  

Per altre informazioni, vedere [Costruttori (Guida per programmatori C#)](../classes-and-structs/constructors.md).

## <a name="finalizers"></a>Finalizzatori

Una definizione di corpo di espressione per un finalizzatore in genere contiene istruzioni di pulitura, ad esempio le istruzioni che rilasciano risorse non gestite.

L'esempio seguente definisce un finalizzatore che usa una definizione di corpo di espressione per indicare che è stato chiamato il finalizzatore.

[!code-cs[expression-bodied-finalizer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-destructor.cs#1)]  

Per altre informazioni, vedere [Finalizzatori (Guida per programmatori C#)](../classes-and-structs/destructors.md).

## <a name="property-get-statements"></a>Istruzioni Property Get

Se si sceglie di implementare manualmente una funzione di accesso Property Get, è possibile usare una definizione di corpo di espressione per singole espressioni che restituiscono semplicemente il valore della proprietà. Si noti che l'istruzione `return` non viene usata.

L'esempio seguente definisce una proprietà `Location.Name` la cui funzione di accesso Property Get restituisce il valore del campo `locationName` privato sottostante alla proprietà. 

[!code-cs[expression-bodied-property-getter](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-ctor.cs#1)]  

Le proprietà di sola lettura che usano una definizione di corpo di espressione possono essere implementate senza un'istruzione `set` esplicita. La sintassi è:

```csharp
PropertyName => returnValue;
```

L'esempio seguente definisce una classe `Location` la cui proprietà `Name` di sola lettura viene implementata come definizione del corpo dell'espressione che restituisce il valore del campo `locationName` privato.

[!code-cs[expression-bodied-constructor](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-readonly.cs#1)]  

Per altre informazioni, vedere [Proprietà (Guida per programmatori C#)](../classes-and-structs/properties.md).

## <a name="property-set-statements"></a>Istruzioni Property Set

Se si sceglie di implementare manualmente una funzione di accesso Property Set, è possibile usare una definizione di corpo di espressione per un'espressione a riga singola che assegna un valore al campo sottostante alla proprietà.

L'esempio seguente definisce una proprietà `Location.Name` la cui istruzione Property Set assegna il proprio argomento di input al campo `locationName` privato sottostante alla proprietà.

[!code-cs[expression-bodied-property-setter](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-ctor.cs#1)]  

Per altre informazioni, vedere [Proprietà (Guida per programmatori C#)](../classes-and-structs/properties.md).

## <a name="indexers"></a>Indicizzatori

Analogamente alle proprietà, le funzioni di accesso get e set di un indicizzatore sono costituite da definizioni di corpi di espressione se la funzione di accesso get è costituita da una singola istruzione che restituisce un valore o la funzione di accesso set esegue un'assegnazione semplice.

Nell'esempio seguente viene definita una classe denominata `Sports` che include una matrice <xref:System.String> interna contenente i nomi di alcuni sport. Le funzioni di accesso sia get che set dell'indicizzatore vengono implementate come definizioni di corpi di espressione.

[!code-cs[expression-bodied-indexer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-indexers.cs#1)] 

Per altre informazioni, vedere [Indicizzatori (Guida per programmatori C#)](../indexers/index.md).


