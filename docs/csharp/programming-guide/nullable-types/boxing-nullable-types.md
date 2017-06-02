---
title: Conversione boxing di tipi nullable (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- boxing [C#], nullable types
- unboxing [C#], nullable types
- nullable types [C#], boxing and unboxing
ms.assetid: bdb5b626-abc0-405d-8f64-0f0a0bf883a4
caps.latest.revision: 12
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
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: e4ff2e8a31ca5a59494f80597460e90107e78c8a
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="boxing-nullable-types-c-programming-guide"></a>Conversione boxing di tipi nullable (Guida per programmatori C#)
Gli oggetti basati su tipi nullable sono boxed solo se l'oggetto è diverso da null. Se <xref:System.Nullable%601.HasValue%2A> è `false`, il riferimento all'oggetto viene assegnato a `null` anziché alla conversione boxing. Ad esempio:  
  
```csharp  
bool? b = null;  
object o = b;  
// Now o is null.  
```  
  
 Se l'oggetto è diverso da null (ovvero se <xref:System.Nullable%601.HasValue%2A> è `true`) viene eseguita la conversione boxing, ma solo il tipo sottostante su cui è basato l'oggetto viene boxed. La conversione boxing di un tipo di valore nullable diverso da null converte il tipo di valore stesso, non <xref:System.Nullable%601?displayProperty=fullName> che include il tipo di valore. Ad esempio:  
  
```csharp  
bool? b = false;  
int? i = 44;  
object bBoxed = b; // bBoxed contains a boxed bool.  
object iBoxed = i; // iBoxed contains a boxed int.  
```  
  
 I due oggetti boxed sono identici a quelli creati dalla conversione boxing di tipi non nullable. E, proprio come i tipi boxed non nullable, possono essere boxed in tipi nullable, come illustrato nell'esempio seguente:  
  
```csharp  
bool? b2 = (bool?)bBoxed;  
int? i2 = (int?)iBoxed;  
```  
  
## <a name="remarks"></a>Note  
 Il comportamento di tipi nullable boxed offre due vantaggi:  
  
1.  È possibile testare gli oggetti nullable e la relativa controparte boxed per i valori null:  
  
    ```csharp  
    bool? b = null;  
    object boxedB = b;  
    if (b == null)  
    {  
      // True.  
    }  
    if (boxedB == null)  
    {  
      // Also true.  
    }  
    ```  
  
2.  I tipi nullable boxed supportano la funzionalità del tipo sottostante:  
  
    ```csharp  
    double? d = 44.4;  
    object iBoxed = d;  
    // Access IConvertible interface implemented by double.  
    IConvertible ic = (IConvertible)iBoxed;  
    int i = ic.ToInt32(null);  
    string str = ic.ToString();  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)   
 [Procedura: Identificare un tipo nullable](../../../csharp/programming-guide/nullable-types/how-to-identify-a-nullable-type.md)
