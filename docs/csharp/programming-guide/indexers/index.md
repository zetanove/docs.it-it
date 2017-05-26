---
title: Indicizzatori (Guida per programmatori C#) | Microsoft Docs
ms.date: 2017-03-10
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.indexers
dev_langs:
- CSharp
helpviewer_keywords:
- indexers [C#]
- C# language, indexers
ms.assetid: 022cd27d-d5e0-4cfe-8b97-dc018cc3355d
caps.latest.revision: 29
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
ms.openlocfilehash: 0b5ca4707903f03b6ab7138137fb3107cfb0cce2
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="indexers-c-programming-guide"></a>Indicizzatori (Guida per programmatori C#)

Gli indicizzatori consentono di indicizzare le istanze di una classe o struct esattamente come le matrici. Il valore indicizzato può essere impostato o recuperato senza specificare in modo esplicito un membro di istanza o tipo. Gli indicizzatori sono analoghi alle [proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md), con la differenza che le relative funzioni di accesso accettano i parametri.  
 
 Nell'esempio seguente viene definita una classe generica con i semplici metodi delle funzioni di accesso [get](../../../csharp/language-reference/keywords/get.md) e [set](../../../csharp/language-reference/keywords/set.md) per assegnare e recuperare i valori. La classe `Program` crea un'istanza di questa classe per archiviare le stringhe.  
  
 [!code-cs[indexers#1](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-1.cs)]  
  
> [!NOTE]
>  Per altri esempi, vedere [Sezioni correlate](../../../csharp/programming-guide/indexers/index.md#BKMK_RelatedSections).  
  
## <a name="expression-body-definitions"></a>Definizioni del corpo dell'espressione  
 
È normale che un indicizzatore ottenga o imposti una funzione di accesso in modo che sia costituita da una singola istruzione che restituisce o imposta un valore. I membri con corpo di espressione offrono una sintassi semplificata per supportare questo scenario. A partire da C# 6 è possibile implementare un indicizzatore di sola lettura come membro con corpo di espressione, come mostrato nell'esempio seguente.

[!code-cs[indexers#2](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-2.cs)]  

Si noti che `=>` introduce il corpo dell'espressione e che la parola chiave `get` non è usata. 

A partire da C# 7, le funzioni di accesso get e set possono essere implementate entrambe come membri con corpo di espressione. In questo caso, è necessario usare entrambe le parole chiave `get` e `set`. Ad esempio:

[!code-cs[indexers#3](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-3.cs)]  
  
## <a name="indexers-overview"></a>Panoramica sugli indicizzatori  
  
-   Gli indicizzatori consentono di indicizzare gli oggetti in modo simile alle matrici.  
  
-   Una funzione di accesso `get` restituisce un valore. Una funzione di accesso `set` assegna un valore.  
  
-   La parola chiave [this](../../../csharp/language-reference/keywords/this.md) viene usata per definire gli indicizzatori.  
  
-   La parola chiave [value](../../../csharp/language-reference/keywords/value.md) viene usata per definire il valore assegnato dall'indicizzatore `set`.  
  
-   Non è necessario che gli indicizzatori vengano indicizzati da un valore Integer, perché la definizione del meccanismo di ricerca specifico dipende dall'utente.  
  
-   Gli indicizzatori possono essere sottoposti a overload.  
  
-   Gli indicizzatori possono avere più di un parametro formale, ad esempio quando si accede a una matrice bidimensionale.  
  
##  <a name="BKMK_RelatedSections"></a> Sezioni correlate  
  
-   [Uso degli indicizzatori](../../../csharp/programming-guide/indexers/using-indexers.md)  
  
-   [Indicizzatori nelle interfacce](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)  
  
-   [Confronto tra proprietà e indicizzatori](../../../csharp/programming-guide/indexers/comparison-between-properties-and-indexers.md)  
  
-   [Limitazione dell'accessibilità delle funzioni di accesso](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)
