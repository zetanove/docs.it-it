---
title: sizeof (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- sizeof_CSharpKeyword
- sizeof
dev_langs:
- CSharp
helpviewer_keywords:
- sizeof keyword [C#]
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
caps.latest.revision: 20
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
ms.openlocfilehash: 7a1944caceaba3ffb8d83a8f67e5ef2975bf9644
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="sizeof-c-reference"></a>sizeof (Riferimenti per C#)
Usato per ottenere la dimensione in byte per un tipo non gestito. I tipi non gestiti includono i tipi predefiniti che sono elencati nella tabella riportata di seguito, nonché quanto segue:  
  
-   Tipi enum  
  
-   Tipi puntatore  
  
-   Struct definiti dall'utente che non contengono campi o proprietà che sono tipi di riferimento  
  
 Nell'esempio seguente viene illustrato come ottenere la dimensione di un `int`:  
  
```csharp  
// Constant value 4:  
int intSize = sizeof(int);   
```  
  
## <a name="remarks"></a>Note  
 A partire dalla versione 2.0 di C#, l'applicazione di `sizeof` ai tipi predefiniti non richiede più l'uso della modalità [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  
  
 Non è possibile eseguire l'overload dell'operatore `sizeof`. I valori restituiti dall'operatore `sizeof` sono di tipo `int`. Nella tabella seguente vengono illustrati i valori costanti che vengono sostituiti con espressioni `sizeof` che dispongono di determinati tipi predefiniti come operandi.  
  
|Espressione|Valore costante|  
|----------------|--------------------|  
|`sizeof(sbyte)`|1|  
|`sizeof(byte)`|1|  
|`sizeof(short)`|2|  
|`sizeof(ushort)`|2|  
|`sizeof(int)`|4|  
|`sizeof(uint)`|4|  
|`sizeof(long)`|8|  
|`sizeof(ulong)`|8|  
|`sizeof(char)`|2 (Unicode)|  
|`sizeof(float)`|4|  
|`sizeof(double)`|8|  
|`sizeof(decimal)`|16|  
|`sizeof(bool)`|1|  
  
 Per tutti gli altri tipi, inclusi gli struct, l'operatore `sizeof` può essere usato solo nei blocchi di codice unsafe. Sebbene sia possibile usare il metodo <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=fullName>, il valore restituito da questo metodo non è sempre uguale al valore restituito da `sizeof`. <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=fullName> restituisce la dimensione dopo il marshalling del tipo, mentre `sizeof` restituisce la dimensione allocata da Common Language Runtime, che include eventuali spaziature interne.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csrefKeywordsOperator#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/sizeof_1.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per gli operatori](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [enum](../../../csharp/language-reference/keywords/enum.md)   
 [Codice di tipo unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md)   
 [Costanti](../../../csharp/programming-guide/classes-and-structs/constants.md)
