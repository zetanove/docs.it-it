---
title: Direttiva using static (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2017-03-10
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- using static directive [C#]
ms.assetid: 8b8f9e34-c75e-469b-ba85-6f2eb4090314
author: rpetrusha
ms.author: ronpet
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
ms.sourcegitcommit: f111ba3db26f247cbc56ee296b652bc04efb837d
ms.openlocfilehash: 66c68530f5684e4d75b9aaa21334e54dde5b64b6
ms.contentlocale: it-it
ms.lasthandoff: 05/02/2017

---
# <a name="using-static-directive-c-reference"></a>Direttiva using static (Riferimenti per C#)

La direttiva `using static` consente di definire un tipo i cui membri statici sono accessibili senza specificare un nome di tipo. La sintassi è la seguente:

```csharp
using static <fully-qualified-type-name>
```

dove *fully-qualified-type-name* è il nome del tipo i cui membri statici possono essere usati come riferimento senza specificare un nome di tipo. Se non si specifica un nome di tipo completo (il nome completo dello spazio dei nomi con il nome del tipo), C# genera l'errore del compilatore CS0246: "Impossibile trovare il nome del tipo o dello spazio dei nomi '<type-name>'."

La direttiva `using static` si applica a qualsiasi tipo che includa membri statici, anche qualora siano presenti membri di istanza. Tuttavia, i membri di istanza possono essere chiamati solo tramite l'istanza del tipo.

La direttiva `using static` è stata introdotta in C# 6.

## <a name="remarks"></a>Note
 
Quando si chiama un membro statico si fornisce in genere il nome del tipo e il nome del membro. Immettere ripetutamente lo stesso nome di tipo per chiamare i membri del tipo può generare codice troppo dettagliato e incomprensibile. Ad esempio, la seguente definizione di una classe `Circle` fa riferimento a un numero di membri della classe @System.Math.
  
[!code-cs[using-static#1](../../../../samples/snippets/csharp/language-reference/keywords/using/using-static1.cs#1)]

Eliminando la necessità di fare riferimento in modo esplicito alla classe @System.Math ogni volta che si fa riferimento a un membro, la direttiva `using static` genera un codice più chiaro:

[!code-cs[using-static#2](../../../../samples/snippets/csharp/language-reference/keywords/using/using-static2.cs#1)]

`using static` importa solo i membri statici accessibili e i tipi annidati dichiarati nel tipo specificato.  I membri ereditati non vengono importati.  È possibile eseguire l'importazione da qualsiasi tipo denominato con una direttiva using static, inclusi i moduli Visual Basic.  Se nei metadati vengono visualizzate funzioni di primo livello F# come membri statici di un tipo denominato il cui nome è un identificatore C# valido, le funzioni F# possono essere importate.  
  
 `using static` crea metodi di estensione dichiarati nel tipo specificato disponibile per la ricerca del metodo di estensione.  Tuttavia, i nomi dei metodi di estensione non vengono importati nell'ambito del riferimento non qualificato nel codice.  
  
 I metodi con lo stesso nome importati da tipi diversi tramite direttive `using static` diverse nella stessa unità di compilazione o nello stesso spazio dei nomi costituiscono un gruppo di metodi.  La risoluzione dell'overload in questi gruppi di metodi segue le normali regole C#.  
  
## <a name="example"></a>Esempio

L'esempio seguente usa la direttiva `using static` per rendere i membri statici della classe @System.Console, @System.Math e @System.String disponibili senza dover specificare il nome del tipo.

[!code-cs[using-static#3](../../../../samples/snippets/csharp/language-reference/keywords/using/using-static3.cs)]

Nell'esempio la direttiva `using static` può anche essere stata applicata al tipo @System.Double. In questo caso sarebbe stato possibile chiamare il metodo @System.Double.TryParse(System.String,System.Double@) senza specificare un nome di tipo. Ciò crea tuttavia codice meno leggibile, poiché è necessario controllare le istruzioni `using static` per quale metodo `TryParse` di tipo numerico viene chiamato.

## <a name="see-also"></a>Vedere anche

[Direttiva using](using-directive.md)   
[Riferimenti per C#](../../../csharp/language-reference/index.md)   
[Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
[Uso degli spazi dei nomi](../../../csharp/programming-guide/namespaces/using-namespaces.md)   
[Parole chiave per gli spazi dei nomi](../../../csharp/language-reference/keywords/namespace-keywords.md)   
[Spazi dei nomi](../../../csharp/programming-guide/namespaces/index.md)   

