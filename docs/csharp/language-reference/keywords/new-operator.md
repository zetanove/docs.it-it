---
title: Operatore new (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
caps.latest.revision: 22
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
ms.openlocfilehash: f0831bbbaf68c8c9e1e0e2d77ccf18e7c8b42e4a
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="new-operator-c-reference"></a>Operatore new (Riferimenti per C#)
Usato per creare oggetti e richiamare costruttori. Ad esempio:  
  
```  
Class1 obj  = new Class1();  
```  
  
 Viene usato anche per creare istanze di tipi anonimi:  
  
```  
var query = from cust in customers  
            select new {Name = cust.Name, Address = cust.PrimaryAddress};  
```  
  
 L'operatore `new` viene usato anche per richiamare il costruttore predefinito per i tipi di valore. Ad esempio:  
  
```  
int i = new int();  
```  
  
 Nell'istruzione precedente `i` viene inizializzato in `0`, ovvero il valore predefinito per il tipo `int`. L'istruzione ha lo stesso effetto dell'istruzione seguente:  
  
```  
int i = 0;  
```  
  
 Per un elenco completo dei valori predefiniti, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md).  
  
 È utile ricordare che è errato dichiarare un costruttore predefinito per uno [struct](../../../csharp/language-reference/keywords/struct.md) poiché ogni tipo di valore ha implicitamente un costruttore predefinito pubblico. È possibile dichiarare costruttori con parametri su un tipo struct per impostarne i valori iniziali, ma questa operazione è necessaria solo se sono richiesti valori diversi da quello predefinito.  
  
 Gli oggetti di tipo valore, ad esempio gli struct, vengono creati nello stack, mentre gli oggetti di tipo riferimento, ad esempio le classi, vengono creati nell'heap. Entrambi i tipi di oggetti vengono eliminati automaticamente in modo definitivo, mentre gli oggetti basati su tipi di valori vengono eliminati definitivamente quando escono dall'ambito di validità e quelli basati su tipi di riferimento vengono eliminati definitivamente in un momento non specificato dopo che è stato rimosso l'ultimo riferimento ad essi. Per i tipi di riferimento che usano risorse fisse, ad esempio grandi quantità di memoria, handle di file o connessioni di rete, può risultare preferibile adottare la finalizzazione deterministica per assicurarsi che l'oggetto venga eliminato definitivamente prima possibile. Per altre informazioni, vedere [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md).  
  
 Non è possibile eseguire l'overload dell'operatore `new`.  
  
 Se l'operatore `new` non riesce ad allocare memoria, genererà l'eccezione <xref:System.OutOfMemoryException>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono creati e inizializzati un oggetto `struct` e un oggetto classe usando l'operatore `new` e vengono quindi assegnati i valori. I valori predefiniti e assegnati sono visualizzati.  
  
 [!code-cs[csrefKeywordsOperator#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/new-operator_1.cs)]  
  
 Si noti che nell'esempio il valore predefinito di una stringa è `null` e, pertanto, non viene visualizzato.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)
