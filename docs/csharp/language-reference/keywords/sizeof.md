---
title: "sizeof (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "sizeof_CSharpKeyword"
  - "sizeof"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "sizeof (parola chiave) [C#]"
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# sizeof (Riferimenti per C#)
Utilizzato per ottenere la dimensione in byte di un tipo non gestito.  I tipi non gestiti includono i tipi incorporati elencati nella tabella seguente, nonché gli elementi seguenti:  
  
-   Tipi enum  
  
-   Tipi puntatore  
  
-   Struct definiti dall'utente che non contengono campi o proprietà che corrispondono a tipi di riferimento  
  
 Nell'esempio seguente viene illustrato come recuperare la dimensione di un tipo `int`:  
  
```c#  
// Constant value 4:  
int intSize = sizeof(int);   
```  
  
## Note  
 A partire dalla versione 2.0 di C\#, l'applicazione di `sizeof` ai tipi incorporati non richiede più l'utilizzo della modalità [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  
  
 Non è possibile sottoporre l'operatore `sizeof` a overload.  I valori restituiti dall'operatore `sizeof` sono di tipo `int`.  Nella tabella seguente vengono illustrati i valori costanti che sostituiscono le espressioni `sizeof` con determinati tipi incorporati come operandi.  
  
|Espressione|Valore costante|  
|-----------------|---------------------|  
|`sizeof(sbyte)`|1|  
|`sizeof(byte)`|1|  
|`sizeof(short)`|2|  
|`sizeof(ushort)`|2|  
|`sizeof(int)`|4|  
|`sizeof(uint)`|4|  
|`sizeof(long)`|8|  
|`sizeof(ulong)`|8|  
|`sizeof(char)`|2 \(Unicode\)|  
|`sizeof(float)`|4|  
|`sizeof(double)`|8|  
|`sizeof(decimal)`|16|  
|`sizeof(bool)`|1|  
  
 Per tutti gli altri tipi, inclusi gli struct, l'operatore `sizeof` può essere utilizzato soltanto in blocchi di codice unsafe.  Sebbene sia possibile utilizzare il metodo <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=fullName>, il valore restituito da questo metodo non corrisponde sempre al valore restituito da `sizeof`.  <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=fullName> restituisce la dimensione dopo il marshalling del tipo, mentre `sizeof` restituisce la dimensione allocata da Common Language Runtime, incluso l'eventuale riempimento.  
  
## Esempio  
 [!code-cs[csrefKeywordsOperator#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/sizeof_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [enum](../../../csharp/language-reference/keywords/enum.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md)   
 [Costanti](../../../csharp/programming-guide/classes-and-structs/constants.md)