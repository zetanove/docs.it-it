---
title: Confronto di uguaglianze (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- object equality [C#]
ms.assetid: 10b865ea-4e7b-4127-9242-c9b8f57d9f04
caps.latest.revision: 14
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 9f7d8c6e816efe248739d0771d332a784b1e185f
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="equality-comparisons-c-programming-guide"></a>Confronto di uguaglianze (Guida per programmatori C#)
A volte è necessario confrontare due valori per verificarne l'uguaglianza. In alcuni casi si verifica l'*uguaglianza dei valori*, nota anche come *equivalenza*, ovvero se i valori contenuti nelle due variabili sono uguali. In altri casi, è necessario determinare se due variabili fanno riferimento allo stesso oggetto sottostante in memoria. Questo tipo di uguaglianza è detto *uguaglianza dei riferimenti* o *identità*. In questo argomento vengono descritti questi due tipi di uguaglianza e indicati i collegamenti ad altri argomenti per le informazioni dettagliate.  
  
## <a name="reference-equality"></a>Uguaglianza di riferimenti  
 Uguaglianza di riferimenti significa che due riferimenti ad oggetti puntano allo stesso oggetto sottostante. Ciò può verificarsi con un'assegnazione semplice, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideStatements#18](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/equality-comparisons_1.cs)]  
  
 In questo codice vengono creati due oggetti, ma dopo l'istruzione di assegnazione, entrambi i riferimenti fanno riferimento allo stesso oggetto. Di conseguenza, esiste un'uguaglianza dei riferimenti. Usare il metodo <xref:System.Object.ReferenceEquals%2A> per determinare se i due riferimenti fanno riferimento allo stesso oggetto.  
  
 Il concetto di uguaglianza dei riferimenti si applica solo ai tipi di riferimento. Per gli oggetti di tipo di valore non può esistere l'uguaglianza dei riferimenti poiché quando un'istanza di un tipo di valore viene assegnata a una variabile, viene creata una copia del valore. Di conseguenza, non è possibile avere due struct unboxed che fanno riferimento alla stessa posizione in memoria. Inoltre, se si usa <xref:System.Object.ReferenceEquals%2A> per confrontare due tipi di valore, il risultato sarà sempre `false`, anche se i valori contenuti negli oggetti sono tutti identici. Ciò avviene perché ogni variabile è di tipo boxed in un'istanza separata dell'oggetto. Per altre informazioni, vedere [Procedura: Testare l'uguaglianza dei riferimenti (identità)](../../../csharp/programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md).  
  
## <a name="value-equality"></a>uguaglianza di valori  
 Uguaglianza di valori significa che due oggetti contengono lo stesso valore o gli stessi valori. Per i tipi di valore primitivi, ad esempio [int](../../../csharp/language-reference/keywords/int.md) o [bool](../../../csharp/language-reference/keywords/bool.md), i test per verificare l'uguaglianza di valori sono semplici. È possibile usare l'operatore [==](../../../csharp/language-reference/operators/equality-comparison-operator.md), come indicato nell'esempio seguente.  
  
```csharp  
int a = GetOriginalValue();  
int b = GetCurrentValue();  
  
// Test for value equality.   
if( b == a)   
{  
    // The two integers are equal.  
}  
```  
  
 Per la maggior parte degli altri tipi, il test dell'uguaglianza di valori è più complesso poiché è necessario sapere in che modo viene definito dal tipo. Per le classi e gli struct con più campi o proprietà, l'uguaglianza di valori viene spesso definita in modo che tutti i campi o tutte le proprietà abbiano lo stesso valore. Ad esempio, due oggetti `Point` possono essere definiti equivalenti se pointA.X è uguale a pointB.X e pointA.Y è uguale a pointB.Y.  
  
 Tuttavia, nessun requisito prevede che l'equivalenza sia basata su tutti i campi in un tipo. Può essere basata su un subset. Quando si confrontano i tipi di cui non si è proprietari, è necessario assicurarsi di sapere esattamente in che modo viene definita l'equivalenza per quel tipo. Per altre informazioni su come definire l'uguaglianza di valori nelle classi e negli struct, vedere [Procedura: Definire l'uguaglianza di valori per un tipo](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md).  
  
### <a name="value-equality-for-floating-point-values"></a>Uguaglianza di valori per i valori a virgola mobile  
 I confronti di uguaglianza dei valori a virgola mobile ([double](../../../csharp/language-reference/keywords/double.md) e [float](../../../csharp/language-reference/keywords/float.md)) sono problematici a causa dell'imprecisione dell'aritmetica a virgola mobile nei computer binari. Per altre informazioni, vedere le osservazioni nell'argomento <xref:System.Double?displayProperty=fullName>.  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Procedura: Testare l'uguaglianza dei riferimenti (identità)](../../../csharp/programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md)|Descrive come determinare se per due variabili esiste l'uguaglianza dei riferimenti.|  
|[Procedura: Definire l'uguaglianza di valori per un tipo](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md)|Descrive come specificare una definizione personalizzata di uguaglianza dei valori per un tipo.|  
|[Guida per programmatori C#](../../../csharp/programming-guide/index.md)|Include collegamenti a informazioni dettagliate su funzionalità importanti del linguaggio C# e sulle funzionalità disponibili per C# attraverso .NET Framework.|  
|[Tipi](../../../csharp/programming-guide/types/index.md)|Informazioni sul sistema di tipi C# e collegamenti a informazioni aggiuntive.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)
