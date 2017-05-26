---
title: Cast e conversioni di tipi (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- type conversion [C#]
- data type conversion [C#]
- numeric conversions [C#]
- conversions [C#], type
- casting [C#]
- converting types [C#]
ms.assetid: 568df58a-d292-4b55-93ba-601578722878
caps.latest.revision: 52
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
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: d421f0115642efa73dbeb893dba912b96d5f4dc6
ms.contentlocale: it-it
ms.lasthandoff: 03/31/2017

---
# <a name="casting-and-type-conversions-c-programming-guide"></a>Cast e conversioni di tipi (Guida per programmatori C#)
Poiché C# è statisticamente tipizzato in fase di compilazione, dopo la prima dichiarazione, una variabile non può essere dichiarata di nuovo o usata per archiviare valori di un altro tipo, a meno che tale tipo non sia convertibile nel tipo della variabile. Ad esempio, non può essere eseguita nessuna conversione da un numero intero a una stringa arbitraria. Pertanto, dopo che si dichiara `i` come valore intero, è possibile assegnargli la stringa "Hello", come illustrato nel codice seguente.  
  
```csharp  
int i;  
i = "Hello"; // Error: "Cannot implicitly convert type 'string' to 'int'"  
```  
  
 Potrebbe tuttavia essere necessario copiare un valore in un variabile o un parametro di metodo di un altro tipo. Ad esempio, si potrebbe avere una variabile intera da passare a un metodo il cui parametro è tipizzato come `double`. O potrebbe essere necessario assegnare una variabile di classe a una variabile di un tipo interfaccia. Questi tipi di operazioni sono detti *conversioni di tipi*. In C#, è possibile eseguire i tipi di conversioni seguenti:  
  
-   **Conversioni implicite**: non è necessaria alcuna sintassi speciale perché la conversione è indipendente dai tipi e i dati non andranno persi. Gli esempi includono conversioni dai tipi integrali più piccoli ai più grandi e conversioni dalle classi derivate alle classi di base.  
  
-   **Conversioni esplicite (cast)**: le conversioni esplicite richiedono un operatore di cast. L'esecuzione di cast è obbligatoria se si prevede una possibile perdita di informazioni durante la conversione oppure se la conversione non riesce per altri motivi.  Alcuni esempi tipici includono la conversione numerica in un tipo con precisione inferiore o con un intervallo più piccolo e la conversione di un'istanza della classe di base in una classe derivata.  
  
-   **Conversioni definite dall'utente**: le conversioni definite dall'utente vengono eseguite da metodi speciali che possono essere definiti per abilitare conversioni esplicite e implicite tra tipi personalizzati che non hanno una relazione di classe basata su una classe di base. Per altre informazioni, vedere [Operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md).  
  
-   **Conversioni con le classi helper**: per eseguire la conversione tra tipi non compatibili, ad esempio numeri interi e oggetti <xref:System.DateTime?displayProperty=fullName> oppure tra stringhe esadecimali e matrici di byte, è possibile usare la classe <xref:System.BitConverter?displayProperty=fullName>, la classe <xref:System.Convert?displayProperty=fullName> e i metodi `Parse` dei tipi numerici predefiniti, ad esempio <xref:System.Int32.Parse%2A?displayProperty=fullName>. Per altre informazioni, vedere [Procedura: Convertire una matrice di byte in un int](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md), [Procedura: Convertire una stringa in un numero](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md) e [Procedura: Eseguire la conversione tra stringhe esadecimali e tipi numerici](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md).  
  
## <a name="implicit-conversions"></a>Conversioni implicite  
 Per i tipi numerici predefiniti, è possibile eseguire una conversione implicita quando il valore da archiviare può essere adattato nella variabile senza essere troncato o arrotondato. Ad esempio, una variabile di tipo [long](../../../csharp/language-reference/keywords/long.md) (numero intero a 8 byte) può archiviare qualsiasi valore archiviabile da un [int](../../../csharp/language-reference/keywords/int.md) (4 byte in computer a 32 bit). Nell'esempio seguente, il compilatore converte in modo implicito il valore a destra in un tipo `long` prima di assegnarlo a `bigNum`.  
  
 [!code-cs[csProgGuideTypes#34](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_1.cs)]  
  
 Per un elenco completo delle conversioni numeriche implicite, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
 Per i tipi di riferimento, è sempre disponibile una conversione implicita da una classe a qualsiasi classe di base diretta o indiretta o interfacce. Poiché una classe derivata contiene sempre tutti i membri di una classe di base, non è necessaria alcuna sintassi speciale.  
  
```  
Derived d = new Derived();  
Base b = d; // Always OK.  
```  
  
## <a name="explicit-conversions"></a>Conversioni esplicite  
 Tuttavia, se una conversione non può essere eseguita senza il rischio di perdita di informazioni, il compilatore richiede di eseguire una conversione esplicita, che viene chiamata *cast*. Un cast è un modo per informare esplicitamente il compilatore che si vuole eseguire la conversione e che si è a conoscenza della possibile perdita di dati. Per eseguire un cast, specificare il tipo tra parentesi davanti al valore o alla variabile da convertire. Il seguente programma esegue il cast di [double](../../../csharp/language-reference/keywords/double.md) in [int](../../../csharp/language-reference/keywords/int.md). Il programma non verrà compilato senza il cast.  
  
 [!code-cs[csProgGuideTypes#2](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_2.cs)]  
  
 Per un elenco delle conversioni numeriche esplicite consentite, vedere [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md).  
  
 Per i tipi di riferimento, è necessario un cast esplicito se si vuole eseguire la conversione da un tipo di base a un tipo derivato:  
  
```csharp  
// Create a new derived type.  
Giraffe g = new Giraffe();  
  
// Implicit conversion to base type is safe.  
Animal a = g;  
  
// Explicit conversion is required to cast back  
// to derived type. Note: This will compile but will  
// throw an exception at run time if the right-side  
// object is not in fact a Giraffe.  
Giraffe g2 = (Giraffe) a;  
```  
  
 Un'operazione di cast tra tipi di riferimento non modifica il tipo in fase di esecuzione dell'oggetto sottostante. Viene modificato solo il tipo del valore usato come riferimento a tale oggetto. Per altre informazioni, vedere [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
## <a name="type-conversion-exceptions-at-run-time"></a>Eccezioni nella conversione di tipi in fase di esecuzione  
 In alcune conversioni di tipi di riferimento, il compilatore non può determinare se un cast è valido. È possibile che un'operazione di cast compilata correttamente non riesca in fase di esecuzione. Come illustrato nell'esempio seguente, un cast di tipo che non riesce in fase di esecuzione genera un'eccezione <xref:System.InvalidCastException> da eliminare.  
  
 [!code-cs[csProgGuideTypes#41](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_3.cs)]  
  
 Il linguaggio C# offre gli operatori [is](../../../csharp/language-reference/keywords/is.md) e [as](../../../csharp/language-reference/keywords/as.md) che consentono di testare la compatibilità prima di eseguire un cast. Per altre informazioni, vedere [Procedura: Eseguire il cast sicuro tramite gli operatori as e is ](../../../csharp/programming-guide/types/how-to-safely-cast-by-using-as-and-is-operators.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  

## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [Operatore ()](../../../csharp/language-reference/operators/invocation-operator.md)   
 [explicit](../../../csharp/language-reference/keywords/explicit.md)   
 [implicit](../../../csharp/language-reference/keywords/implicit.md)   
 [Operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)   
 [Conversione di tipi generalizzati](http://msdn.microsoft.com/library/49253ae6-7657-4810-82ab-1176a6feeada)   
 [Conversione di tipi esportati](http://msdn.microsoft.com/en-us/1dfe55f4-07a2-4b61-aabf-a8cf65783a6b)   
 [Procedura: Convertire una stringa in un numero](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)
