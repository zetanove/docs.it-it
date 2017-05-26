---
title: Usare i tipi nullable (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- nullable types [C#], about nullable types
ms.assetid: 0bacbe72-ce15-4b14-83e1-9c14e6380c28
caps.latest.revision: 31
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a780a11d8dd238187eb82933359bbb151bb3c333
ms.openlocfilehash: 88397167b12a00bf5e99a0537148a2957b9f0bd8
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="using-nullable-types-c-programming-guide"></a>Utilizzo dei tipi nullable (Guida per programmatori C#)
I tipi nullable possono rappresentare tutti i valori di un tipo sottostante e un valore [null](../../../csharp/language-reference/keywords/null.md) aggiuntivo. I tipi nullable vengono dichiarati in una delle due modalità riportate di seguito:  
  
 `System.Nullable<T> variable`  
  
 -oppure-  
  
 `T? variable`  
  
 `T` è il tipo sottostante del tipo nullable. `T` può essere qualsiasi tipo di valore, incluso `struct`; non può essere un tipo di riferimento.  
  
 Per un esempio di quando è possibile usare un tipo nullable, considerare una comune variabile booleana che supporta solo due valori: true e false. Non esiste alcun valore corrispondente a "non definito". In molte applicazioni di programmazione, in particolare nelle interazioni tra database, le variabili possono avere uno stato non definito. Ad esempio un campo di un database può contenere i valori true o false, ma può anche non contenere alcun valore. Allo stesso modo è possibile impostare i tipi di riferimento su `null` per indicare che non sono inizializzati.  
  
 Questa disparità può comportare un lavoro di programmazione aggiuntivo e l'aggiunta di variabili per l'archiviazione delle informazioni sullo stato, dell'uso di valori speciali e così via. Il modificatore del tipo nullable in C# consente di creare variabili di tipo valore che indicano un valore indefinito.  
  
## <a name="examples-of-nullable-types"></a>Esempi di tipi nullable  
 È possibile usare come base per un tipo nullable qualsiasi tipo di valore. Ad esempio:  
  
 [!code-cs[csProgGuideTypes#4](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_1.cs)]  
  
## <a name="the-members-of-nullable-types"></a>Membri dei tipi nullable  
 Ogni istanza di un tipo nullable ha due proprietà pubbliche di sola lettura:  
  
-   `HasValue`  
  
     `HasValue` è di tipo `bool`. È impostata su `true` quando la variabile contiene un valore diverso da null.  
  
-   `Value`  
  
     `Value` è dello stesso tipo del tipo sottostante. Se `HasValue` è `true`, `Value` contiene un valore significativo. Se `HasValue` è `false`, l'accesso a `Value` genera un'eccezione <xref:System.InvalidOperationException>.  
  
 In questo esempio il membro `HasValue` viene usato per verificare se la variabile contiene un valore prima che tenti di visualizzarlo.  
  
 [!code-cs[csProgGuideTypes#5](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_2.cs)]  
  
 La verifica della presenza del valore può anche essere eseguita come nell'esempio seguente:  
  
 [!code-cs[csProgGuideTypes#6](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_3.cs)]  
  
## <a name="explicit-conversions"></a>Conversioni esplicite  
 È possibile eseguire il cast di un tipo nullable in un tipo normale, in modo esplicito tramite il cast o con la proprietà `Value`. Ad esempio:  
  
 [!code-cs[csProgGuideTypes#7](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_4.cs)]  
  
 Se viene impostata una conversione definita dall'utente tra due tipi di dati, la stessa conversione può essere usata anche con le versioni nullable di questi tipi di dati.  
  
## <a name="implicit-conversions"></a>Conversioni implicite  
 Una variabile di tipo nullable può essere impostata su null con la parola chiave `null`, come visualizzato nell'esempio seguente:  
  
 [!code-cs[csProgGuideTypes#8](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_5.cs)]  
  
 La conversione da un tipo normale a un tipo nullable è implicita.  
  
 [!code-cs[csProgGuideTypes#9](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_6.cs)]  
  
## <a name="operators"></a>Operatori  
 Gli operatori unari e binari predefiniti e gli eventuali operatori definiti dall'utente esistenti per i tipi di valore possono essere usati anche dai tipi nullable. Questi operatori generano un valore null se gli operandi sono null. In caso contrario, l'operatore usa il valore contenuto per calcolare il risultato. Ad esempio:  
  
 [!code-cs[csProgGuideTypes#10](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_7.cs)]  
  
 Quando si eseguono confronti con tipi nullable, se il valore di uno dei tipi nullable è null e l'altro non lo è, tutti i confronti restituiscono `false` ad eccezione di `!=` (diverso da). È importante non presupporre che poiché un particolare confronto restituisce `false` il caso opposto restituirà `true`. Nell'esempio seguente, 10 non è maggiore, minore né uguale a null. Solo `num1 != num2` restituisce `true`.  
  
 [!code-cs[csProgGuideTypes#11](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_8.cs)]  
  
 Un confronto di uguaglianza tra due tipi nullable che sono entrambi null restituisce `true`.  
  
## <a name="the--operator"></a>Operatore ??  
 L'operatore `??` definisce un valore predefinito restituito quando un tipo nullable è assegnato a un tipo non nullable.  
  
 [!code-cs[csProgGuideTypes#12](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_9.cs)]  
  
 L'operatore può essere usato anche con più tipi nullable. Ad esempio:  
  
 [!code-cs[csProgGuideTypes#13](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_10.cs)]  
  
## <a name="the-bool-type"></a>Tipo bool?  
 Il tipo nullable `bool?` può contenere tre valori diversi: [true](../../../csharp/language-reference/keywords/true.md), [false](../../../csharp/language-reference/keywords/false.md) e [null](../../../csharp/language-reference/keywords/null.md). Per informazioni su come eseguire il cast da bool? a bool, vedere [Procedura: Eseguire il cast sicuro da bool? a bool](../../../csharp/programming-guide/nullable-types/how-to-safely-cast-from-bool-to-bool.md).  
  
 I valori nullable booleani sono come il tipo di variabile booleano usato in SQL. Per garantire che i risultati prodotti dagli operatori `&` e `|` siano coerenti con il tipo booleano a tre valori in SQL, sono disponibili gli operatori predefiniti seguenti:  
  
 `bool? operator &(bool? x, bool? y)`  
  
 `bool? operator |(bool? x, bool? y)`  
  
 Nella seguente tabella vengono elencati i risultati di questi operatori:  
  
|X|y|x&y|x&#124;y|  
|-------|-------|---------|--------------|  
|true|true|true|true|  
|true|false|false|true|  
|true|Null|Null|true|  
|false|true|false|true|  
|false|false|false|false|  
|false|Null|false|Null|  
|Null|true|Null|true|  
|Null|false|false|Null|  
|Null|Null|Null|Null|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)   
 [Conversione boxing dei tipi nullable](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)   
 [Tipi di valori nullable](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
