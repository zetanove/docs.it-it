---
title: "Passaggio di parametri di tipi di valore (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "parametri di metodo [C#], tipi di valori"
  - "parametri [C#], valore"
ms.assetid: 193ab86f-5f9b-4359-ac29-7cdf8afad3a6
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Passaggio di parametri di tipi di valore (Guida per programmatori C#)
Una variabile associata a un [tipo che rappresenta un valore](../../../csharp/language-reference/keywords/value-types.md) contiene direttamente i dati, mentre una variabile associata a un [tipo che rappresenta un riferimento](../../../csharp/language-reference/keywords/reference-types.md) contiene un riferimento ai dati.  Passando una variabile di tipo di valore a un metodo dal valore significa passare una copia della variabile al metodo.  Tutte le modifiche al parametro che si verificano nel metodo non hanno alcun effetto sui dati originali archiviati nella variabile di argomenti.  Se si desidera che il metodo chiamato per modificare il valore del parametro, è necessario passarli per riferimento, utilizzando il [riferimento](../../../csharp/language-reference/keywords/ref.md) o  [indietro](../../../csharp/language-reference/keywords/out.md) parola chiave.  Per semplicità, negli esempi che seguono viene utilizzata solo la parola chiave `ref`.  
  
## Passaggio di tipi di valore per valore  
 Nell'esempio che segue viene illustrato il passaggio di parametri associati a tipi che rappresentano un valore per valore.  La variabile `n` viene passata per valore al metodo `SquareIt`.  Eventuali modifiche apportate nel metodo non avranno alcun effetto sul valore originale della variabile.  
  
 [!code-cs[csProgGuideParameters#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-value-type-param_1.cs)]  
  
 la variabile `n` è un tipo di valore.  Contiene i dati, il valore `5`.  Quando si richiama `SquareIt`, il contenuto di `n` viene copiato nel parametro `x`, che viene elevato al quadrato all'interno del metodo.  in `Main`, tuttavia, il valore di  `n` è lo stesso dopo avere chiamato  `SquareIt` metodo come era prima.  La modifica eseguita nel metodo influisce solo sulla variabile locale `x`.  
  
## Passaggio di tipi di valore per riferimento  
 L'esempio seguente è lo stesso dell'esempio precedente, tranne per il fatto che l'argomento viene passato come `ref` parametro.  Il valore dell'argomento sottostante, `n`, viene modificato quando  `x` viene modificato nel metodo.  
  
 [!code-cs[csProgGuideParameters#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-value-type-param_2.cs)]  
  
 In questo esempio non viene passato il valore di `n`, ma solo un riferimento a `n`.  Il parametro `x` non è di tipo [int](../../../csharp/language-reference/keywords/int.md) ma è un riferimento a un valore `int`, in questo caso un riferimento a `n`.  Pertanto, quando `x` è quadrato nel metodo, cìò che è quadrato è quello  `x` si riferisce,  `n`.  
  
## Scambio di tipi di valore  
 Un esempio comune di modificare i valori degli argomenti è un metodo di scambio, dove si passano due variabili al metodo e il metodo scambia i relativi contenuti.  È necessario passare argomenti al metodo di scambio per riferimento.  In caso contrario, sostituire le copie locali dei parametri nel metodo e nessuna modifica si verifica nel metodo di chiamata.  Nell'esempio seguente viene scambiata i valori Integer.  
  
 [!code-cs[csProgGuideParameters#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-value-type-param_3.cs)]  
  
 Quando si chiama `SwapByRef` il metodo utilizza,  `ref` parola chiave nella chiamata, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideParameters#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-value-type-param_4.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Passaggio di parametri](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [Passaggio di parametri di tipi di riferimento](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)