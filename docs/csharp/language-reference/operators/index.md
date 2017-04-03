---
title: Operatori C# | Microsoft Docs
ms.date: 2017-03-09
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.operators
dev_langs:
- CSharp
helpviewer_keywords:
- boolean operators [C#]
- expressions [C#], operators
- logical operators [C#]
- operators [C#]
- Visual C#, operators
- indirection operators [C#]
- assignment operators [C#]
- shift operators [C#]
- relational operators [C#]
- bitwise operators [C#]
- address operators [C#]
- keywords [C#], operators
- arithmetic operators [C#]
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
caps.latest.revision: 40
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: fd70919f68c7c48894e7c944aeb1a74c73513e8e
ms.lasthandoff: 03/13/2017

---
# <a name="c-operators"></a>Operatori [C#]
C# fornisce diversi operatori, ovvero simboli che specificano quali operazioni (matematiche, indicizzazione, chiamate di funzione e così via) eseguire in un'espressione.  È possibile eseguire l'[overload](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md) di diversi operatori per cambiarne il significato quando vengono applicati a un tipo definito dall'utente.  
  
 Le operazioni sui tipi integrali (come `==`, `!=`, `<`, `>`, `&`, `|`) sono generalmente consentite sui tipi di enumerazione (`enum`).  
  
 Le sezioni elencano gli operatori C# da quelli con la precedenza più alta a quelli con la più bassa.  Gli operatori di ogni sezione condividono lo stesso livello di precedenza.  
  
## <a name="primary-operators"></a>Operatori primari  
 Sono gli operatori con la precedenza più alta.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x.y](../../../csharp/language-reference/operators/member-access-operator.md): accesso ai membri.  
  
 [x?.y](../../../csharp/language-reference/operators/null-conditional-operators.md): accesso ai membri condizionali null.  Restituisce `null` se l'operando sul lato sinistro è `null`.  
 
 [x?[y]](../../../csharp/language-reference/operators/null-conditional-operators.md): accesso all'indice condizionale null. Restituisce `null` se l'operando sul lato sinistro è `null`.
 
 [f(x)](../../../csharp/language-reference/operators/invocation-operator.md): chiamata di funzione.  
  
 [a&#91;x&#93;](../../../csharp/language-reference/operators/index-operator.md): indicizzazione oggetto aggregato.  
  
 [a?&#91;x&#93;](../../../csharp/language-reference/operators/null-conditional-operators.md): indicizzazione condizionale null.  Restituisce `null` se l'operando sul lato sinistro è `null`.  
  
 [x++](../../../csharp/language-reference/operators/increment-operator.md): incremento suffisso.  Restituisce il valore di x e quindi aggiorna la posizione di archiviazione con il valore di x che risulta maggiore (in genere aggiunge il numero intero 1).  
  
 [x--](../../../csharp/language-reference/operators/decrement-operator.md): decremento suffisso.  Restituisce il valore di x e quindi aggiorna la posizione di archiviazione con il valore di x che risulta minore (in genere sottrae il numero intero 1).  
  
 [new](../../../csharp/language-reference/keywords/new-operator.md): creazione di un'istanza del tipo.  
  
 [typeof](../../../csharp/language-reference/keywords/typeof.md): restituisce l'oggetto System.Type che rappresenta l'operando.  
  
 [checked](../../../csharp/language-reference/keywords/checked.md): abilita il controllo di overflow per le operazioni con numeri interi.  
  
 [unchecked](../../../csharp/language-reference/keywords/unchecked.md): disabilita il controllo di overflow per le operazioni con numeri interi.  Questo è il comportamento predefinito per il compilatore.  
  
 [default(T)](../../../csharp/programming-guide/generics/default-keyword-in-generic-code.md): restituisce il valore inizializzato predefinito di tipo T, `null` per i tipi di riferimento, zero per i tipi numerici e inserimento di zero/`null` nei membri per i tipi struct.  
  
 [delegate](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md): dichiara e restituisce un'istanza di delegato.  
  
 [sizeof](../../../csharp/language-reference/keywords/sizeof.md): restituisce le dimensioni in byte dell'operando type.  
  
 [->](../../../csharp/language-reference/operators/dereference-operator.md): dereferenziazione puntatore combinata con l'accesso ai membri.  
  
## <a name="unary-operators"></a>Operatori unari  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [+x](../../../csharp/language-reference/operators/addition-operator.md): restituisce il valore di x.  
  
 [-x](../../../csharp/language-reference/operators/subtraction-operator.md): negazione numerica.  
  
 [!x](../../../csharp/language-reference/operators/logical-negation-operator.md): negazione logica.  
  
 [~x](../../../csharp/language-reference/operators/bitwise-complement-operator.md): complemento bit per bit.  
  
 [~x](../../../csharp/language-reference/operators/increment-operator.md): incremento prefisso.  Restituisce il valore di x dopo avere aggiornato la posizione di archiviazione con il valore di x che risulta maggiore (in genere aggiunge il numero intero 1).  
  
 [--x](../../../csharp/language-reference/operators/decrement-operator.md): decremento prefisso.  Restituisce il valore di x dopo avere aggiornato la posizione di archiviazione con il valore di x che risulta minore (in genere aggiunge il numero intero 1).  
  
 [(T)x](../../../csharp/language-reference/operators/invocation-operator.md): cast di tipo.  
  
 [await](../../../csharp/language-reference/keywords/await.md): attende un oggetto `Task`.  
  
 [&x](../../../csharp/language-reference/operators/and-operator.md): indirizzo.  
  
 [*x](../../../csharp/language-reference/operators/multiplication-operator.md): dereferenziazione.  
  
## <a name="multiplicative-operators"></a>Operatori moltiplicativi  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x * y](../../../csharp/language-reference/operators/multiplication-operator.md): moltiplicazione.  
  
 [x / y](../../../csharp/language-reference/operators/division-operator.md): divisione.  Se gli operandi sono numeri interi, il risultato è un numero intero troncato verso zero (ad esempio, `-7 / 2 is -3`).  
  
 [x % y](../../../csharp/language-reference/operators/modulus-operator.md): modulo.  Se gli operandi sono numeri interi, restituisce il resto della divisione di x per y.  Se `q = x / y` e `r = x % y`, allora `x = q * y + r`   
  
## <a name="additive-operators"></a>Operatori additivi  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x + y](../../../csharp/language-reference/operators/addition-operator.md): addizione.  
  
 [x – y](../../../csharp/language-reference/operators/subtraction-operator.md): sottrazione.  
  
## <a name="shift-operators"></a>Operatori shift  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x <\<  y](../../../csharp/language-reference/operators/left-shift-operator.md): spostamento dei bit a sinistra e inserimento di zero a destra.  
  
 [x >> y](../../../csharp/language-reference/operators/right-shift-operator.md): spostamento dei bit a destra.  Se l'operando di sinistra è `int` o `long`, i bit di sinistra vengono riempiti con il bit più significativo.  Se l'operando di sinistra è `uint` o `ulong`, i bit di sinistra vengono riempiti con zero.  
  
## <a name="relational-and-type-testing-operators"></a>Operatori relazionali e operatori di test del tipo  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x \< y](../../../csharp/language-reference/operators/less-than-operator.md): minore di (true se x è minore di y).  
  
 [x > y](../../../csharp/language-reference/operators/greater-than-operator.md): maggiore di (true se x è maggiore di y).  
  
 [x \<= y](../../../csharp/language-reference/operators/less-than-equal-operator.md): minore o uguale a.  
  
 [x >= y](../../../csharp/language-reference/operators/greater-than-equal-operator.md): maggiore o uguale a.  
  
 [is](../../../csharp/language-reference/keywords/is.md): compatibilità del tipo.  Restituisce true se è possibile eseguire il cast dell'operando di sinistra valutato al tipo specificato nell'operando di destra (un tipo statico).  
  
 [as](../../../csharp/language-reference/keywords/as.md): conversione di tipi.  Restituisce il cast dell'operando di sinistra al tipo specificato dall'operando di destra (un tipo statico), ma `as` restituisce `null` dove `(T)x` genererebbe un'eccezione.  
  
## <a name="equality-operators"></a>Operatori di uguaglianza  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x == y](../../../csharp/language-reference/operators/equality-comparison-operator.md): uguaglianza.  Per impostazione predefinita, per i tipi di riferimento diversi da `string`, restituisce l'uguaglianza dei riferimenti (test dell'identità).  Tuttavia, i tipi possono eseguire l'overload di `==`, quindi, se si prevede di testare l'identità, è meglio usare il metodo `ReferenceEquals` su `object`.  
  
 [x != y](../../../csharp/language-reference/operators/not-equal-operator.md): diverso da.  Vedere il commento per `==`.  Se un tipo esegue l'overload di `==`, deve eseguire l'overload di `!=`.  
  
## <a name="logical-and-operator"></a>Operatore AND logico  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x & y](../../../csharp/language-reference/operators/and-operator.md): AND logico o bit per bit.  L'uso con i tipi Integer e con i tipi `enum` è in genere consentito.  
  
## <a name="logical-xor-operator"></a>Operatore XOR logico  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x ^ y](../../../csharp/language-reference/operators/xor-operator.md): XOR logico o bit per bit.  Di solito è possibile usarlo con i tipi Integer e con i tipi `enum`.  
  
## <a name="logical-or-operator"></a>Operatore OR logico  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x &#124; y](../../../csharp/language-reference/operators/or-operator.md): OR logico o bit per bit.  L'uso con i tipi Integer e con i tipi `enum` è in genere consentito.  
  
## <a name="conditional-and-operator"></a>Operatore AND condizionale  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x && y](../../../csharp/language-reference/operators/conditional-and-operator.md): AND logico.  Se il primo operando è false, C# non valuta il secondo operando.  
  
## <a name="conditional-or-operator"></a>Operatore OR condizionale  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x &#124;&#124; y](../../../csharp/language-reference/operators/conditional-or-operator.md): OR logico.  Se il primo operando è true, C# non valuta il secondo operando.  
  
## <a name="null-coalescing-operator"></a>Operatore null-coalescing  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x ?? y](../../../csharp/language-reference/operators/null-conditional-operator.md): restituisce `x` se è non `null`. In caso contrario, restituisce `y`.  
  
## <a name="conditional-operator"></a>Operatore condizionale  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [t ? x : y](../../../csharp/language-reference/operators/conditional-operator.md): se `t` di test è true, valuta e restituisce `x`. In caso contrario, valuta e restituisce `y`.  
  
## <a name="assignment-and-lambda-operators"></a>Operatori di assegnazione e lambda  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x = y](../../../csharp/language-reference/operators/assignment-operator.md): assegnazione.  
  
 [x = y](../../../csharp/language-reference/operators/addition-assignment-operator.md): incremento.  Aggiunge il valore di `y` al valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  Se `x` designa un oggetto `event`, `y` deve essere una funzione appropriata che C# aggiunge come gestore eventi.  
  
 [x -= y](../../../csharp/language-reference/operators/subtraction-assignment-operator.md): decremento.  Sottrae il valore di `y` dal valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  Se `x` designa un oggetto `event`, `y` deve essere una funzione appropriata che C# rimuove come gestore eventi.  
  
 [x -= y](../../../csharp/language-reference/operators/multiplication-assignment-operator.md): assegnazione di moltiplicazione.  Moltiplica il valore di `y` per il valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x -= y](../../../csharp/language-reference/operators/division-assignment-operator.md): assegnazione di divisione.  Divide il valore di `x` per il valore di `y`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x %= y](../../../csharp/language-reference/operators/modulus-assignment-operator.md): assegnazione modulo.  Divide il valore di `x` per il valore di `y`, archivia il resto in `x` e restituisce il nuovo valore.  
  
 [x &= y](../../../csharp/language-reference/operators/and-assignment-operator.md): assegnazione dell'operatore AND.  Applica AND al valore di `y` con il valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x &#124;= y](../../../csharp/language-reference/operators/or-assignment-operator.md): assegnazione dell'operatore OR.  Applica OR al valore di `y` con il valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x ^= y](../../../csharp/language-reference/operators/xor-assignment-operator.md): assegnazione dell'operatore XOR.  Applica XOR al valore di `y` con il valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x <<= y](../../../csharp/language-reference/operators/left-shift-assignment-operator.md): assegnazione di spostamento a sinistra.  Sposta il valore di `x` verso sinistra di `y` posti, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x >>= y](../../../csharp/language-reference/operators/right-shift-assignment-operator.md): assegnazione di spostamento a destra.  Sposta il valore di `x` verso destra di `y` posti, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [=>](../../../csharp/language-reference/operators/lambda-operator.md): dichiarazione lambda.  
  
## <a name="arithmetic-overflow"></a>Overflow aritmetico  
 Gli operatori aritmetici ([+](../../../csharp/language-reference/operators/addition-operator.md), [-](../../../csharp/language-reference/operators/subtraction-operator.md), [*](../../../csharp/language-reference/operators/multiplication-operator.md), [/](../../../csharp/language-reference/operators/division-operator.md)) possono produrre risultati non compresi nell'intervallo dei valori possibili per il tipo numerico coinvolto. È consigliabile fare riferimento alla sezione di un particolare operatore per i dettagli, ma in generale:  
  
- L'overflow aritmetico di interi genera un'eccezione <xref:System.OverflowException> o rimuove i bit più significativi del risultato. La divisione di interi per zero genera sempre un'eccezione @System.DivideByZeroException.  

   Quando si verifica un overflow di interi, ciò che accade dipende dal contesto dell'esecuzione, che può essere [verificato o non verificato](../../../csharp/language-reference/keywords/checked-and-unchecked.md). In un contesto verificato, viene generata un'eccezione <xref:System.OverflowException>. In un contesto non verificato, i bit più significativi del risultato vengono rimossi e l'esecuzione continua. C# consente dunque di scegliere se gestire o ignorare l'overflow. Per impostazione predefinita, le operazioni aritmetiche vengono eseguite in un contesto *non verificato*. 

   Oltre alle operazioni aritmetiche, anche i cast da tipo integrale a tipo integrale possono causare l'overflow, ad esempio il cast di [long](../../../csharp/language-reference/keywords/long.md) a [int](../../../csharp/language-reference/keywords/int.md), e sono soggetti a esecuzione verificata o non verificata. Tuttavia, gli operatori bit per bit e gli operatori shift non causano mai l'overflow.  
   
-   L'overflow aritmetico a virgola mobile o la divisione per zero non genera mai un'eccezione, perché i tipi a virgola mobile si basano su IEEE 754 e quindi dispongono del provisioning per la rappresentazione dell'infinito e di NaN (Not a Number).  
  
-   L'overflow aritmetico [decimale](../../../csharp/language-reference/keywords/decimal.md) genera sempre un'eccezione <xref:System.OverflowException>. La divisione decimale per zero genera sempre un'eccezione <xref:System.DivideByZeroException>.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [C#](../../../csharp/csharp.md)   
 [Operatori che supportano l'overload](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)

