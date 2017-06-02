---
title: "Proprietà (Guida per programmatori C#) | Microsoft Docs"
ms.date: 2017-03-10
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.properties
dev_langs:
- CSharp
helpviewer_keywords:
- properties [C#]
- C# language, properties
ms.assetid: e295a8a2-b357-4ee7-a12e-385a44146fa8
caps.latest.revision: 38
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
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6f4d2bf3ad04fedafb44f8fed63f7234d48af63b
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="properties-c-programming-guide"></a>Proprietà (Guida per programmatori C#)

Una proprietà è un membro che fornisce un meccanismo flessibile per leggere, scrivere o calcolare il valore di un campo privato. Le proprietà possono essere usate come se fossero membri dati pubblici, ma sono in realtà metodi speciali denominati *funzioni di accesso*. Questo consente di accedere facilmente ai dati e di alzare di livello la sicurezza e la flessibilità dei metodi.  

## <a name="properties-overview"></a>Panoramica delle proprietà  
  
- Le proprietà consentono a una classe di esporre un modo pubblico per ottenere e impostare i valori, nascondendo però il codice di implementazione o di verifica.  
  
- Una funzione di accesso della proprietà [get](../../../csharp/language-reference/keywords/get.md) viene usata per restituire il valore della proprietà, mentre una funzione di accesso della proprietà [set](../../../csharp/language-reference/keywords/set.md) viene usata per assegnare un nuovo valore. Queste funzioni di accesso possono avere diversi livelli di accesso. Per altre informazioni, vedere [Limitazione dell'accessibilità delle funzioni di accesso](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md).  
  
- La parola chiave [value](../../../csharp/language-reference/keywords/value.md) viene usata per definire il valore che deve essere assegnato dalla funzione di accesso `set`.  
- Le proprietà possono essere di *lettura/scrittura* con entrambe le funzione di accesso `get` e `set`, di *sola lettura* con la funzione di accesso `get` e senza la funzione di accesso `set` o di *sola scrittura* con la funzione di accesso `set` e senza la funzione di accesso `get`. Le proprietà di sola scrittura sono rare e vengono in genere usate per limitare l'accesso ai dati sensibili.

- Le proprietà semplici che non richiedono alcun codice di funzione di accesso personalizzata possono essere implementate come definizioni del corpo dell'espressione o come [proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md).
 
## <a name="properties-with-backing-fields"></a>Proprietà con campi sottostanti

Un modello di base per l'implementazione di una proprietà prevede l'uso di un campo sottostante privato per l'impostazione e il recupero del valore della proprietà. La funzione di accesso `get` restituisce il valore del campo privato e la funzione di accesso `set` può eseguire una convalida dei dati prima di assegnare un valore al campo privato. Entrambe le funzioni di accesso possono anche eseguire una conversione o un calcolo nei dati prima che vengano archiviati o restituiti.

L'esempio seguente illustra il modello. Nell'esempio la classe `TimePeriod` rappresenta un intervallo di tempo. Internamente la classe archivia l'intervallo di tempo in secondi in un campo privato denominato `seconds`. Una proprietà di lettura/scrittura denominata `Hours` consente al cliente di specificare l'intervallo di tempo in ore. Entrambe le funzioni di accesso `get` e `set` eseguono la conversione necessaria tra ore e secondi. Inoltre, la funzione di accesso `set` convalida i dati e genera @System.ArgumentOutOfRangeException se il numero di ore non è valido. 
   
 [!code-cs[Properties#1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-1.cs)]  
  
## <a name="expression-body-definitions"></a>Definizioni del corpo dell'espressione  

 Le funzioni di accesso delle proprietà sono spesso costituite da istruzioni a riga singola che assegnano o restituiscono il risultato di un'espressione. È possibile implementare queste proprietà come membri con corpo di espressione. Le definizioni del corpo dell'espressione sono costituite dal simbolo `=>` seguito dall'espressione per l'assegnazione o il recupero dalla proprietà.

 A partire da C# 6, le proprietà di sola lettura possono implementare la funzione di accesso `get` come membro con corpo di espressione. In questo caso non viene usata la parola chiave della funzione di accesso `get` né la parola chiave `return`. L'esempio seguente implementa la proprietà `Name` di sola lettura come membro con corpo di espressione.

 [!code-cs[Properties#2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-2.cs)]  

 A partire da C# 7, entrambe le funzioni di accesso `get` e `set` possono essere implementate come membri con corpo di espressione. In questo caso, è necessario che siano presenti le parole chiave `get` e `set`. L'esempio seguente illustra l'uso di definizioni del corpo dell'espressione per entrambe le funzioni di accesso. Si noti che la parola chiave `return` non viene usata con la funzione di accesso `get`.
 
  [!code-cs[Properties#3](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-3.cs)]  

## <a name="auto-implemented-properties"></a>Proprietà implementate automaticamente

In alcuni casi, le funzioni di accesso `get` e `set` delle proprietà si limitano ad assegnare o a recuperare un valore da un campo sottostante senza includere alcuna logica aggiuntiva. Usando le proprietà implementate automaticamente è possibile semplificare il codice e fare in modo che il compilatore C# specifichi automaticamente in modo trasparente il campo sottostante. 

Se una proprietà ha entrambe le funzioni di accesso `get` e `set`, entrambe le funzioni devono essere implementate automaticamente. È possibile definire una proprietà implementata automaticamente usando le parole chiave `get` e `set` senza specificare alcuna implementazione. L'esempio seguente ripete l'esempio precedente, ad eccezione del fatto che `Name` e `Price` sono proprietà implementate automaticamente. Si noti che l'esempio rimuove anche il costruttore con parametri in modo che gli oggetti `SaleItem` vengano ora inizializzati con una chiamata al costruttore predefinito e un [inizializzatore di oggetto](object-and-collection-initializers.md).

  [!code-cs[Properties#4](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-4.cs)]  

## <a name="related-sections"></a>Sezioni correlate  
  
-   [Uso delle proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)  
  
-   [Proprietà dell'interfaccia](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)  
  
-   [Confronto tra proprietà e indicizzatori](../../../csharp/programming-guide/indexers/comparison-between-properties-and-indexers.md)  
  
-   [Limitazione dell'accessibilità delle funzioni di accesso](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)  
  
-   [Proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Uso delle proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [Parola chiave get](../../../csharp/language-reference/keywords/get.md)    
 [Parola chiave set](../../../csharp/language-reference/keywords/set.md)    

