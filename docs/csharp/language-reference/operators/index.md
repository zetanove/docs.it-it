---
title: "Operatori | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "cs.operators"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "operatori indirizzo [C#]"
  - "operatori aritmetici [C#]"
  - "operatori di assegnazione [C#]"
  - "operatori bit per bit [C#]"
  - "operatori booleani [C#]"
  - "espressioni [C#], operatori"
  - "operatori di riferimento indiretto [C#]"
  - "parole chiave [C#], operatori"
  - "operatori logici [C#]"
  - "operatori [C#]"
  - "operatori relazionali [C#]"
  - "operatori shift [C#]"
  - "Visual C#, operatori"
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
caps.latest.revision: 40
caps.handback.revision: 38
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatori
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

C\# fornisce diversi operatori, ovvero simboli che specificano quali operazioni \(matematiche, indicizzazione, chiamate di funzione e così via\) eseguire in un'espressione.  È possibile eseguire l'[overload](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md) di diversi operatori per cambiarne il significato quando vengono applicati a un tipo definito dall'utente.  
  
 Le operazioni sui tipi integrali \(ad esempio `==`, `!=`, `<`, `>`, `&`,                   `|` \) di solito sono consentite sui tipi di enumerazione \(`enum`\).  
  
 Le sezioni elencano gli operatori C\# da quelli con la precedenza più alta a quelli con la più bassa.  Gli operatori di ogni sezione condividono lo stesso livello di precedenza.  
  
## Operatori primari  
 Sono gli operatori con la precedenza più alta.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x.y](../../../csharp/language-reference/operators/member-access-operator.md): accesso ai membri.  
  
 [x?.y](../../../csharp/language-reference/operators/null-conditional-operators.md): accesso ai membri condizionali null.  Restituisce null se l'operando sul lato sinistro è null.  
  
 [f\(x\)](../../../csharp/language-reference/operators/invocation-operator.md): chiamata di funzione.  
  
 [a&#91;x&#93;](../../../csharp/language-reference/operators/index-operator.md): indicizzazione oggetto aggregato.  
  
 [a?&#91;x&#93;](../../../csharp/language-reference/operators/null-conditional-operators.md): indicizzazione condizionale null.  Restituisce null se l'operando sul lato sinistro è null.  
  
 [x\+\+](../../../csharp/language-reference/operators/increment-operator.md): incremento suffisso.  Restituisce il valore di x e quindi aggiorna la posizione di archiviazione con il valore di x che risulta maggiore \(in genere aggiunge il numero intero 1\).  
  
 [x\-\-](../../../csharp/language-reference/operators/decrement-operator.md): decremento suffisso.  Restituisce il valore di x e quindi aggiorna la posizione di archiviazione con il valore di x che risulta minore \(in genere sottrae il numero intero 1\).  
  
 [New](../../../csharp/language-reference/keywords/new-operator.md): creazione di un'istanza del tipo.  
  
 [Typeof](../../../csharp/language-reference/keywords/typeof.md): restituisce l'oggetto System.Type che rappresenta l'operando.  
  
 [Checked](../../../csharp/language-reference/keywords/checked.md): abilita il controllo di overflow per le operazioni con numeri interi.  
  
 [Unchecked](../../../csharp/language-reference/keywords/unchecked.md): disabilita il controllo di overflow per le operazioni con numeri interi.  Questo è il comportamento predefinito per il compilatore.  
  
 [default\(T\)](../../../csharp/programming-guide/generics/default-keyword-in-generic-code.md): restituisce il valore inizializzato predefinito di tipo T, null per i tipi di riferimento, zero per i tipi numerici e zero\/null specificati nei membri per i tipi struct.  
  
 [Delegate](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md): dichiara e restituisce un'istanza di delegato.  
  
 [Sizeof](../../../csharp/language-reference/keywords/sizeof.md): restituisce le dimensioni in byte dell'operando type.  
  
 [\-\>](../../../csharp/language-reference/operators/dereference-operator.md): dereferenziazione puntatore combinata con l'accesso ai membri.  
  
## Operatori unari  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [\+x](../../../csharp/language-reference/operators/addition-operator.md): restituisce il valore di x.  
  
 [\-x](../../../csharp/language-reference/operators/subtraction-operator.md): negazione numerica.  
  
 [\!x](../../../csharp/language-reference/operators/logical-negation-operator.md): negazione logica.  
  
 [~x](../../../csharp/language-reference/operators/bitwise-complement-operator.md): complemento bit per bit.  
  
 [\+\+x](../../../csharp/language-reference/operators/increment-operator.md): incremento prefisso.  Restituisce il valore di x dopo avere aggiornato la posizione di archiviazione con il valore di x che risulta maggiore \(in genere aggiunge il numero intero 1\).  
  
 [\-\-x](../../../csharp/language-reference/operators/decrement-operator.md): decremento prefisso.  Restituisce il valore di x dopo avere aggiornato la posizione di archiviazione con il valore di x che risulta minore \(in genere aggiunge il numero intero 1\).  
  
 [\(T\)x](../../../csharp/language-reference/operators/invocation-operator.md): cast di tipo.  
  
 [Await](../../../csharp/language-reference/keywords/await.md): attende un oggetto `Task`.  
  
 [&x](../../../csharp/language-reference/operators/and-operator.md): indirizzo.  
  
 [\*x](../../../csharp/language-reference/operators/multiplication-operator.md): dereferenziazione.  
  
## Operatori moltiplicativi  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x \* y](../../../csharp/language-reference/operators/multiplication-operator.md): moltiplicazione.  
  
 [x \/ y](../../../csharp/language-reference/operators/division-operator.md): divisione.  Se gli operandi sono numeri interi, il risultato è un numero intero troncato verso zero \(ad esempio, `-7 / 2 is -3`\).  
  
 [x % y](../../../csharp/language-reference/operators/modulus-operator.md): modulo.  Se gli operandi sono numeri interi, restituisce il resto della divisione di x per y.  Se `q = x / y` e `r = x % y`, allora `x = q * y + r`  
  
## Operatori additivi  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x \+ y](../../../csharp/language-reference/operators/addition-operator.md): addizione.  
  
 [x \- y](../../../csharp/language-reference/operators/subtraction-operator.md): sottrazione.  
  
## Operatori shift  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x \<\< y](../../../csharp/language-reference/operators/left-shift-operator.md): spostamento dei bit a sinistra e inserimento di zero a destra.  
  
 [x \>\> y](../../../csharp/language-reference/operators/right-shift-operator.md): spostamento dei bit a destra.  Se l'operando di sinistra è `int` o `long`, i bit di sinistra vengono riempiti con il bit più significativo.  Se l'operando di sinistra è `uint` o `ulong`, i bit di sinistra vengono riempiti con zero.  
  
## Operatori relazionali e operatori di test del tipo  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x \< y](../../../csharp/language-reference/operators/less-than-operator.md): minore di \(true se x è minore di y\).  
  
 [x \> y](../../../csharp/language-reference/operators/greater-than-operator.md): maggiore di \(true se x è maggiore di y\).  
  
 [x \<\= y](../../../csharp/language-reference/operators/less-than-equal-operator.md): minore o uguale a.  
  
 [x \>\= y](../../../csharp/language-reference/operators/greater-than-equal-operator.md): minore o uguale a.  
  
 [Is](../../../csharp/language-reference/keywords/is.md): compatibilità del tipo.  Restituisce true se è possibile eseguire il cast dell'operando di sinistra valutato al tipo specificato nell'operando di destra \(un tipo statico\).  
  
 [As](../../../csharp/language-reference/keywords/as.md): conversione di tipi.  Restituisce il cast dell'operando di sinistra al tipo specificato dall'operando di destra \(un tipo statico\), ma `as` restituisce `null` dove `(T)x` genererebbe un'eccezione.  
  
## Operatori di uguaglianza  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x \=\= y](../../../csharp/language-reference/operators/equality-comparison-operator.md): uguaglianza.  Per impostazione predefinita, per i tipi di riferimento diversi da `string`, restituisce l'uguaglianza dei riferimenti \(test dell'identità\).  Tuttavia, i tipi possono eseguire l'overload di `==`, quindi, se si prevede di testare l'identità, è meglio usare il metodo `ReferenceEquals` su `object`.  
  
 [x \!\= y](../../../csharp/language-reference/operators/not-equal-operator.md): diverso da.  Vedere il commento per `==`.  Se un tipo esegue l'overload di `==`, deve eseguire l'overload di `!=`.  
  
## Operatore AND logico  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x & y](../../../csharp/language-reference/operators/and-operator.md): AND logico o bit per bit.  L'uso con i tipi Integer e con i tipi `enum` è in genere consentito.  
  
## Operatore XOR logico  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x ^ y](../../../csharp/language-reference/operators/xor-operator.md): XOR logico o bit per bit.  Di solito è possibile usarlo con i tipi Integer e con i tipi `enum`.  
  
## Operatore OR logico  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x &#124; y](../../../csharp/language-reference/operators/or-operator.md): OR logico o bit per bit.  L'uso con i tipi Integer e con i tipi `enum` è in genere consentito.  
  
## Operatore AND condizionale  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x && y](../../../csharp/language-reference/operators/conditional-and-operator.md): AND logico.  Se il primo operando è false, C\# non valuta il secondo operando.  
  
## Operatore OR condizionale  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x &#124;&#124; y](../../../csharp/language-reference/operators/conditional-or-operator.md): OR logico.  Se il primo operando è true, C\# non valuta il secondo operando.  
  
## Operatore null\-coalescing  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [x ?? y](../../../csharp/language-reference/operators/null-conditional-operator.md): restituisce `x` se è non `null`. In caso contrario, restituisce `y`.  
  
## Operatore condizionale  
 Questo operatore ha una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sull'operatore per passare alla pagina dei dettagli con gli esempi.  
  
 [t ? x : y](../../../csharp/language-reference/operators/conditional-operator.md): se `t` di test è true, valuta e restituisce `x`. In caso contrario, valuta e restituisce `y`.  
  
## Operatori di assegnazione e lambda  
 Questi operatori hanno una precedenza più alta di quelli della sezione successiva e più bassa di quelli della sezione precedente.  NOTA: è possibile fare clic sugli operatori per passare alle pagine con informazioni dettagliate ed esempi.  
  
 [x \= y](../../../csharp/language-reference/operators/assignment-operator.md): assegnazione.  
  
 [x \+\= y](../../../csharp/language-reference/operators/addition-assignment-operator.md): incremento.  Aggiunge il valore di `y` al valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  Se `x` designa un oggetto `event`, `y` deve essere una funzione appropriata che C\# aggiunge come gestore eventi.  
  
 [x \-\= y](../../../csharp/language-reference/operators/subtraction-assignment-operator-1.md): decremento.  Sottrae il valore di `y` dal valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  Se `x` designa un oggetto `event`, `y` deve essere una funzione appropriata che C\# rimuove come gestore eventi.  
  
 [x \*\= y](../../../csharp/language-reference/operators/multiplication-assignment-operator.md): assegnazione di moltiplicazione.  Moltiplica il valore di `y` per il valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x \/\= y](../../../csharp/language-reference/operators/subtraction-assignment-operator.md): assegnazione di divisione.  Divide il valore di `x` per il valore di `y`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x %\= y](../../../csharp/language-reference/operators/modulus-assignment-operator.md): assegnazione modulo.  Divide il valore di `x` per il valore di `y`, archivia il resto in `x` e restituisce il nuovo valore.  
  
 [x &\= y](../../../csharp/language-reference/operators/and-assignment-operator.md): assegnazione dell'operatore AND.  Applica AND al valore di `y` con il valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x &#124;\= y](../../../csharp/language-reference/operators/or-assignment-operator.md): assegnazione dell'operatore OR.  Applica OR al valore di `y` con il valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x ^\= y](../../../csharp/language-reference/operators/xor-assignment-operator.md): assegnazione dell'operatore XOR.  Applica XOR al valore di `y` con il valore di `x`, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x \<\<\= y](../../../csharp/language-reference/operators/left-shift-assignment-operator.md): assegnazione di spostamento a sinistra.  Sposta il valore di `x` verso sinistra di `y` posti, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [x \>\>\= y](../../../csharp/language-reference/operators/right-shift-assignment-operator.md): assegnazione di spostamento a destra.  Sposta il valore di `x` verso destra di `y` posti, archivia il risultato in `x` e restituisce il nuovo valore.  
  
 [\=\>](../../../csharp/language-reference/operators/lambda-operator.md): dichiarazione lambda.  
  
## Overflow aritmetico  
 Gli operatori aritmetici \([\+](../../../csharp/language-reference/operators/addition-operator.md), [\-](../../../csharp/language-reference/operators/subtraction-operator.md), [\*](../../../csharp/language-reference/operators/multiplication-operator.md), [\/](../../../csharp/language-reference/operators/division-operator.md)\) possono produrre risultati non compresi nell'intervallo di possibili valori per il tipo numerico coinvolto.  È consigliabile fare riferimento alla sezione di un particolare operatore per i dettagli, ma in generale:  
  
-   L'overflow aritmetico di interi genera un'eccezione <xref:System.OverflowException> o rimuove i bit più significativi del risultato.  La divisione di interi per zero genera sempre un'eccezione `DivideByZeroException`.  
  
-   L'overflow aritmetico a virgola mobile o la divisione per zero non genera mai un'eccezione, perché i tipi a virgola mobile si basano su IEEE 754 e quindi dispongono del provisioning per la rappresentazione dell'infinito e di NaN \(Not a Number\).  
  
-   L'overflow aritmetico [decimale](../../../csharp/language-reference/keywords/decimal.md) genera sempre un'eccezione <xref:System.OverflowException>.  La divisione di decimali per zero genera sempre un'eccezione <xref:System.DivideByZeroException>.  
  
 Quando si verifica un overflow di interi, ciò che accade dipende dal contesto dell'esecuzione, che può essere [verificato o non verificato](../../../csharp/language-reference/keywords/checked-and-unchecked.md).  In un contesto verificato, viene generata un'eccezione <xref:System.OverflowException>.  In un contesto non verificato, i bit più significativi del risultato vengono rimossi e l'esecuzione continua.  C\# consente dunque di scegliere se gestire o ignorare l'overflow.  
  
 Oltre agli operatori aritmetici, anche i cast da tipo integrale a tipo integrale possono causare l'overflow, ad esempio il cast di [long](../../../csharp/language-reference/keywords/long.md) a [int](../../../csharp/language-reference/keywords/int.md), e sono soggetti a esecuzione verificata o non verificata.  Tuttavia, gli operatori bit per bit e gli operatori shift non causano mai l'overflow.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [C\#](../../../csharp/csharp.md)   
 [Operatori che supportano l'overload](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)