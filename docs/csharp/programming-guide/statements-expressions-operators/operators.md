---
title: "Operatori (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, operatori"
  - "operatori [C#]"
  - "operatori [C#], informazioni sugli operatori"
ms.assetid: 214e7b83-1a41-4f7c-9867-64e9c0bab39f
caps.latest.revision: 42
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 42
---
# Operatori (Guida per programmatori C#)
Nel linguaggio C\# un *operatore* è un elemento del programma che si applica a uno o più *operandi* in un'espressione o in un'istruzione. Gli operatori che accettano un unico operando, ad esempio l'operatore di incremento \(`++`\) o `new`, sono denominati operatori *unari*. Quelli che accettano due operandi, ad esempio gli operatori aritmetici \(`+`,`-`,`*`,`/`\), sono denominati operatori *binari*. L'operatore condizionale \(`?:`\) accetta tre operandi ed è l'unico operatore ternario disponibile in C\#.  
  
 L'istruzione C\# riportata di seguito contiene un unico operatore unario e un unico operando. L'operatore di incremento `++` modifica il valore dell'operando `y`.  
  
 [!code-cs[csProgGuideStatements#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/operators_1.cs)]  
  
 L'istruzione C\# riportata di seguito contiene due operatori binari, ciascuno con due operandi. L'operatore di assegnazione `=` ha come operandi la variabile integer `y` e l'espressione `2 + 3`. L'espressione `2 + 3` è costituita dall'operatore di addizione e due operandi, `2` e `3`.  
  
 [!code-cs[csProgGuideStatements#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/operators_2.cs)]  
  
## Operatori, valutazione e precedenza operatori  
 Un operando può essere un'espressione valida composta da codice di qualsiasi lunghezza e può includere un numero qualsiasi di sottoespressioni. In un'espressione che contiene più operatori, l'ordine in cui vengono applicati gli operatori è determinata dalla *precedenza tra operatori*, l'*associatività* e le parentesi.  
  
 Ogni operatore ha una precedenza definita. In un'espressione che contiene più operatori che dispongono di diversi livelli di precedenza, la precedenza degli operatori determina l'ordine in cui gli operatori verranno valutati. L'istruzione che segue, ad esempio, assegna il valore 3 a `n1`.  
  
 `n1 = 11 - 2 * 4;`  
  
 La moltiplicazione viene eseguita per prima perché ha la precedenza sulla sottrazione.  
  
 Nella tabella riportata di seguito gli operatori sono suddivisi in categorie in base al tipo di operazione che eseguono. Le categorie sono elencate in ordine di precedenza.  
  
 **Operatori primari**  
  
|Espressione|Descrizione|  
|-----------------|-----------------|  
|x[.](../../../csharp/language-reference/operators/member-access-operator.md)y<br /><br /> x?.y|Accesso ai membri<br /><br /> Accesso ai membri condizionali|  
|f[\(x\)](../../../csharp/language-reference/operators/invocation-operator.md)|Chiamata a metodi e delegati|  
|a[&#91;x&#93;](../../../csharp/language-reference/operators/index-operator.md)<br /><br /> a?\[x\]|Accesso a matrici e indicizzatori<br /><br /> Accesso a matrici e indicizzatori condizionali|  
|x[\+\+](../../../csharp/language-reference/operators/increment-operator.md)|Post\-incremento|  
|x[\-\-](../../../csharp/language-reference/operators/decrement-operator.md)|Post\-decremento|  
|[new](../../../csharp/language-reference/keywords/new-operator.md) T\(...\)|Creazione di oggetti e delegati|  
|`new` T\(...\){...}|Creazione di oggetti con inizializzatore. Vedere [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).|  
|`new` {...}|Inizializzatore di oggetti anonimi. Vedere [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).|  
|`new` T\[...\]|Creazione di matrici. Vedere [Matrici](../../../csharp/programming-guide/arrays/index.md).|  
|[typeof](../../../csharp/language-reference/keywords/typeof.md)\(T\)|Ottenere l'oggetto System.Type per T|  
|[checked](../../../csharp/language-reference/keywords/checked.md)\(x\)|Valutare l'espressione in un contesto controllato \(checked\)|  
|[unchecked](../../../csharp/language-reference/keywords/unchecked.md)\(x\)|Valutare l'espressione in un contesto non controllato \(unchecked\)|  
|[default](../../../csharp/language-reference/keywords/default.md) \(T\)|Ottenere il valore predefinito del tipo T|  
|[delegate](../../../csharp/language-reference/keywords/delegate.md) {}|Funzione anonima \(metodo anonimo\)|  
  
 **Operatori unari**  
  
|Espressione|Descrizione|  
|-----------------|-----------------|  
|[\+](../../../csharp/language-reference/operators/addition-operator.md)x|Identità|  
|[\-](../../../csharp/language-reference/operators/subtraction-operator.md)x|Negazione|  
|[\!](../../../csharp/language-reference/operators/logical-negation-operator.md)x|Negazione logica|  
|[~](../../../csharp/language-reference/operators/bitwise-complement-operator.md)x|Negazione bit per bit|  
|[\+\+](../../../csharp/language-reference/operators/increment-operator.md)x|Pre\-incremento|  
|[\-\-](../../../csharp/language-reference/operators/decrement-operator.md)x|Pre\-decremento|  
|[\(T\)](../../../csharp/language-reference/operators/invocation-operator.md)x|Convertire in modo esplicito x nel tipo T|  
  
 **Operatori moltiplicativi**  
  
|Espressione|Descrizione|  
|-----------------|-----------------|  
|[\*](../../../csharp/language-reference/operators/multiplication-operator.md)|Moltiplicazione|  
|[\/](../../../csharp/language-reference/operators/division-operator.md)|Divisione|  
|[%](../../../csharp/language-reference/operators/modulus-operator.md)|Resto|  
  
 **Operatori additivi**  
  
|Espressione|Descrizione|  
|-----------------|-----------------|  
|x [\+](../../../csharp/language-reference/operators/addition-operator.md) y|Addizione, concatenazione di stringhe, combinazione di delegati|  
|x [\-](../../../csharp/language-reference/operators/subtraction-operator.md) y|Sottrazione, rimozione di delegati|  
  
 **Operatori shift**  
  
|Espressione|Descrizione|  
|-----------------|-----------------|  
|x [\<\<](../../../csharp/language-reference/operators/left-shift-operator.md) y|Spostamento a sinistra|  
|x [\>\>](../../../csharp/language-reference/operators/right-shift-operator.md) y|Spostamento a destra|  
  
 **Operatori relazionali e operatori di tipo**  
  
|Espressione|Descrizione|  
|-----------------|-----------------|  
|x [\<](../../../csharp/language-reference/operators/less-than-operator.md) y|Minore di|  
|x [\>](../../../csharp/language-reference/operators/greater-than-operator.md) y|Maggiore di|  
|x [\<\=](../../../csharp/language-reference/operators/less-than-equal-operator.md) y|Minore o uguale a|  
|x [\>\=](../../../csharp/language-reference/operators/greater-than-equal-operator.md) y|Maggiore o uguale a|  
|x [is](../../../csharp/language-reference/keywords/is.md) T|Restituisce true se x è un oggetto T; in caso contrario, false|  
|x [as](../../../csharp/language-reference/keywords/as.md) T|Restituisce x tipizzato come T oppure Null se x non è un oggetto T|  
  
 **Operatori di uguaglianza**  
  
|Espressione|Descrizione|  
|-----------------|-----------------|  
|x [\=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md) y|Uguale|  
|x [\!\=](../../../csharp/language-reference/operators/not-equal-operator.md) y|Non uguaglianza|  
  
 **Operatori logici, condizionali e Null**  
  
|Categoria|Espressione|Descrizione|  
|---------------|-----------------|-----------------|  
|AND logico|x [&](../../../csharp/language-reference/operators/and-operator.md) y|AND Integer bit per bit, AND logico booleano|  
|XOR logico|x [^](../../../csharp/language-reference/operators/xor-operator.md) y|XOR Integer bit per bit, XOR logico booleano|  
|OR logico|x [&#124;](../../../csharp/language-reference/operators/or-operator.md) y|OR Integer bit per bit, OR logico booleano|  
|AND condizionale|x [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) y|Restituisce y solo se x è true|  
|OR condizionale|x [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md) y|Restituisce y solo se x è false|  
|Null\-coalescing|x [??](../../../csharp/language-reference/operators/null-conditional-operator.md) y|Restituisce y se x è Null; in caso contrario x|  
|Condizionale|x [?](../../../csharp/language-reference/operators/conditional-operator.md) y : z|Restituisce y se x è true, z se x è false|  
  
 **Operatori di assegnazione e operatori anonimi**  
  
|Espressione|Descrizione|  
|-----------------|-----------------|  
|[\=](../../../csharp/language-reference/operators/assignment-operator.md)|Assegnazione|  
|x op\= y|Assegnazione composta. Supporta gli operatori seguenti: [\+\=](../../../csharp/language-reference/operators/addition-assignment-operator.md), [\-\=](../../../csharp/language-reference/operators/subtraction-assignment-operator-1.md), [\*\=](../../../csharp/language-reference/operators/multiplication-assignment-operator.md), [\/\=](../../../csharp/language-reference/operators/subtraction-assignment-operator.md), [%\=](../../../csharp/language-reference/operators/modulus-assignment-operator.md), [&\=](../../../csharp/language-reference/operators/and-assignment-operator.md), [&#124;\=](../../../csharp/language-reference/operators/or-assignment-operator.md), [\!\=](../../../csharp/language-reference/operators/not-equal-operator.md), [\<\<\=](../../../csharp/language-reference/operators/left-shift-assignment-operator.md), [\>\>\=](../../../csharp/language-reference/operators/right-shift-assignment-operator.md)|  
|\(T x\) [\=\>](../../../csharp/language-reference/operators/lambda-operator.md) y|Funzione anonima \(espressione lambda\)|  
  
## Associazione  
 Quando in un'espressione sono presenti due o più operatori con la stessa precedenza, verranno valutati in base all'associazione. Gli operatori che prevedono l'associazione all'operando sinistro vengono valutati nell'ordine da sinistra a destra. L'espressione `x * y / z` viene ad esempio valutata come `(x * y) / z`. Gli operatori che prevedono l'associazione all'operando destro vengono valutati nell'ordine da destra a sinistra. Ad esempio, l'operatore di assegnazione prevede l'associazione all'operando destro. Se non fosse così, il codice seguente restituirà un errore.  
  
```c#  
int a, b, c; c = 1; // The following two lines are equivalent. a = b = c; a = (b = c); // The following line, which forces left associativity, causes an error. //(a = b) = c;  
```  
  
 Facendo un altro esempio, l'operatore ternario \([?:](../../../csharp/language-reference/operators/conditional-operator.md)\) prevede l'associazione all'operando destro. La maggior parte degli operatori binari prevede l'associazione all'operando sinistro.  
  
 Se gli operatori in un'espressione sono impostati su associativo o associativo da destra, gli operandi di ogni espressione vengono valutati per primi, da sinistra a destra. Negli esempi seguenti viene illustrato l'ordine di valutazione degli operatori e degli operandi.  
  
|Istruzione|Ordine di valutazione|  
|----------------|---------------------------|  
|`a = b`|a, b, \=|  
|`a = b + c`|a, b, c, \+, \=|  
|`a = b + c * d`|a, b, c, d, \*, \+, \=|  
|`a = b * c + d`|a, b, c, \*, d, \+, \=|  
|`a = b - c + d`|a, b, c, \-, d, \+, \=|  
|`a += b -= c`|a, b, c, \-\=, \+\=|  
  
## Aggiunta di parentesi  
 È possibile modificare l'ordine imposto dalla precedenza degli operatori e dall'associatività usando le parentesi. Ad esempio, il risultato dell'espressione `2 + 3 * 2` restituisce normalmente 8, in quanto gli operatori di moltiplicazione hanno la precedenza su quelli di addizione. Tuttavia, se si scrive l'espressione in questo modo `(2 + 3) * 2`, l'addizione è presa in considerazione prima della moltiplicazione e il risultato sarà 10. Negli esempi seguenti viene illustrato l'ordine di valutazione delle espressioni tra parentesi. Come negli esempi precedenti, gli operandi vengono valutati prima di applicare l'operatore.  
  
|Istruzione|Ordine di valutazione|  
|----------------|---------------------------|  
|`a = (b + c) * d`|a, b, c, \+, d, \*, \=|  
|`a = b - (c + d)`|a, b, c, d, \+, \-, \=|  
|`a = (b + c) * (d - e)`|a, b, c, \+, d, e, \-, \*, \=|  
  
## Overload degli operatori  
 È possibile modificare il comportamento degli operatori per classi e struct personalizzati. Questo processo è denominato *overload degli operatori*. Per altre informazioni, vedere [Operatori che supportano l'overload](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md).  
  
## Sezioni correlate  
 Per altre informazioni, vedere [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md) e [Operatori](../../../csharp/language-reference/operators/index.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Istruzioni, espressioni e operatori](../../../csharp/programming-guide/statements-expressions-operators/index.md)