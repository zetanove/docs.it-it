---
title: 'Procedura: Usare i puntatori per copiare una matrice di byte (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- byte arrays [C#]
- arrays [C#], byte
- pointers [C#], to copy bytes
ms.assetid: ec16fbb4-a24e-45f5-a763-9499d3fabe0a
caps.latest.revision: 21
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
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: b9d6f93a92b48fcbdd70475ae4c1b8a62ddd9125
ms.contentlocale: it-it
ms.lasthandoff: 04/08/2017

---
# <a name="how-to-use-pointers-to-copy-an-array-of-bytes--c-programming-guide"></a>Procedura: utilizzare puntatori per copiare una matrice di byte (Guida per programmatori C#)
Nell'esempio seguente vengono usati i puntatori per copiare i byte da una matrice a un'altra.  
  
 In questo esempio viene usata la parola chiave [unsafe](../../../csharp/language-reference/keywords/unsafe.md), che consente l'uso di puntatori nel metodo `Copy`. Per dichiarare i puntatori nelle matrici di origine e destinazione, viene usata l'istruzione [fixed](../../../csharp/language-reference/keywords/fixed-statement.md), che *aggiunge* la posizione delle matrici di origine e destinazione nella memoria in modo che non vengano rimosse da Garbage Collection. I blocchi di memoria per le matrici vengono rimossi quando il blocco `fixed` è completato. Il metodo `Copy` in questo esempio usa la parola chiave `unsafe`. Deve pertanto essere compilato con l'opzione del compilatore **/unsafe**. Per impostare l'opzione in Visual Studio, fare clic con il pulsante destro del mouse sul nome del progetto e scegliere **Proprietà**. Nella scheda **Compilazione**, selezionare **Consenti codice di tipo unsafe**.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuidePointers#3](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-use-pointers-to-copy-an-array-of-bytes_1.cs)]  
  
 [!code-cs[csProgGuidePointers#18](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-use-pointers-to-copy-an-array-of-bytes_2.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [-unsafe (opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)   
 [Garbage Collection](../../../standard/garbage-collection/index.md)
