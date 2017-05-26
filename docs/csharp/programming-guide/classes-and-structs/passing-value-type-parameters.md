---
title: Passaggio di parametri di tipo di valore (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- method parameters [C#], value types
- parameters [C#], value
ms.assetid: 193ab86f-5f9b-4359-ac29-7cdf8afad3a6
caps.latest.revision: 17
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
ms.openlocfilehash: b0735f9a42fad01695c1ad64cfb937dce8e3cb93
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="passing-value-type-parameters-c-programming-guide"></a>Passaggio di parametri di tipo di valore (Guida per programmatori C#)
Una variabile [di tipo valore](../../../csharp/language-reference/keywords/value-types.md) contiene direttamente i dati, mentre una variabile [di tipo riferimento](../../../csharp/language-reference/keywords/reference-types.md) contiene un riferimento ai dati. Quando si passa una variabile di tipo valore a un metodo per valore, si passa una copia della variabile al metodo. Tutte le modifiche al parametro apportate all'interno del metodo non hanno alcun effetto sui dati originali archiviati nella variabile di argomento. Se si vuole che il metodo chiamato modifichi il valore del parametro, è necessario passarlo per riferimento usando la parola chiave [ref](../../../csharp/language-reference/keywords/ref.md) o [out](../../../csharp/language-reference/keywords/out.md). Per semplicità, negli esempi seguenti viene usato `ref`.  
  
## <a name="passing-value-types-by-value"></a>Passaggio di tipi di valore per valore  
 Nell'esempio seguente viene illustrato il passaggio di parametri di tipo valore per valore. La variabile `n` viene passata al metodo `SquareIt` per valore. Tutte le modifiche apportate all'interno del metodo non hanno alcun effetto sul valore originale della variabile.  
  
 [!code-cs[csProgGuideParameters#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_1.cs)]  
  
 La variabile `n` è un tipo valore. Contiene i propri dati, il valore `5`. Quando si richiama `SquareIt`, il contenuto di `n` viene copiato nel parametro `x`, che viene elevato al quadrato all'interno del metodo. In `Main`, tuttavia, il valore di `n` dopo la chiamata del metodo `SquareIt` rimane invariato. La modifica apportata all'interno del metodo ha effetto soltanto sulla variabile locale `x`.  
  
## <a name="passing-value-types-by-reference"></a>Passaggio di tipi di valore per riferimento  
 L'esempio seguente è identico a quello precedente, tranne per il fatto che l'argomento viene passato come parametro `ref`. Il valore dell'argomento sottostante, `n`, viene modificato quando si modifica `x` nel metodo.  
  
 [!code-cs[csProgGuideParameters#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_2.cs)]  
  
 Nell'esempio seguente non viene passato il valore di `n`, ma un riferimento a `n`. Il parametro `x` non è di tipo [int](../../../csharp/language-reference/keywords/int.md) ma è un riferimento a un valore `int`, in questo caso un riferimento a `n`. Di conseguenza, quando `x` viene elevato al quadrato all'interno del metodo, il valore effettivamente elevato al quadrato è quello a cui `x` fa riferimento, ovvero `n`.  
  
## <a name="swapping-value-types"></a>Scambio di tipi di valore  
 Un esempio comune di modifica dei valori degli argomenti è un metodo swap, dove si passano due variabili al metodo e il metodo scambia i relativi contenuti. È necessario passare argomenti al metodo swap per riferimento. In caso contrario, vengono scambiate le copie locali dei parametri all'interno del metodo e al metodo che esegue la chiamata non viene apportata alcuna modifica. L'esempio seguente scambia i valori integer.  
  
 [!code-cs[csProgGuideParameters#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_3.cs)]  
  
 Quando si chiama il metodo `SwapByRef`, usare nella chiamata la parole chiave `ref`, come mostrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideParameters#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-value-type-parameters_4.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Passaggio di parametri](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [Passaggio di parametri di tipo di riferimento](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)
