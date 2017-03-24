---
title: "Procedura: accedere a un elemento di matrice mediante un puntatore (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "puntatori [C#], accesso a matrici"
ms.assetid: 6c46f2af-a730-4855-8638-f136d9abaa12
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Procedura: accedere a un elemento di matrice mediante un puntatore (Guida per programmatori C#)
In un contesto unsafe è possibile accedere a un elemento in memoria utilizzando l'accesso all'elemento mediante puntatore come illustrato nell'esempio seguente:  
  
```  
 char* charPointer = stackalloc char[123];  
for (int i = 65; i < 123; i++)  
{  
    charPointer[i] = (char)i; //access array elements  
}  
```  
  
 L'espressione racchiusa tra parentesi quadre deve essere convertibile in modo implicito in `int`, `uint`, `long` o `ulong`.  L'operazione p\[e\] è equivalente a \*\(p\+e\).  Analogamente a C e C\+\+, l'accesso a elemento del puntatore non implica la verifica di errori relativi a indici di matrici non compresi nell'intervallo.  
  
## Esempio  
 In questo esempio 123 posizioni di memoria vengono allocate a una matrice di caratteri denominata `charPointer`.  La matrice viene utilizzata per visualizzare le lettere in minuscolo e maiuscolo in due cicli [for](../../../csharp/language-reference/keywords/for.md).  
  
 Si noti che l'espressione `charPointer[i]` è equivalente a `*(charPointer + i)` ed è possibile ottenere lo stesso risultato utilizzando una delle due espressioni.  
  
 [!code-cs[csProgGuidePointers#11](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-an-array-element-with-a-pointer_1.cs)]  
  
 [!code-cs[csProgGuidePointers#12](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-an-array-element-with-a-pointer_2.cs)]  
  
  **Lettere maiuscole:**  
**ABCDEFGHIJKLMNOPQRSTUVWXYZ**  
**Lettere minuscole:**  
**abcdefghijklmnopqrstuvwxyz**   
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)