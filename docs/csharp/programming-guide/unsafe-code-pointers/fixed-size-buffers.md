---
title: Buffer a dimensione fissa (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- fixed size buffers [C#]
- unsafe buffers [C#]
- unsafe code [C#], fixed size buffers
ms.assetid: 6220d454-947c-4977-ac9d-9308c6ed5051
caps.latest.revision: 31
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6c5cacb588dc263e5b72e4b3cd93ad10b4b681f2
ms.lasthandoff: 03/13/2017

---
# <a name="fixed-size-buffers-c-programming-guide"></a>Buffer a dimensione fissa (Guida per programmatori C#)
In C# è possibile usare l'istruzione [fixed](../../../csharp/language-reference/keywords/fixed-statement.md) per creare un buffer con una matrice di dimensioni fisse in una struttura di dati. Ciò si rivela utile quando si usa codice esistente, ad esempio codice scritto in altri linguaggi, DLL preesistenti o progetti COM. La matrice fissa può accettare attributi o modificatori consentiti per i membri struct normali. L'unica restrizione è rappresentata dal fatto che il tipo di matrice deve essere `bool`, `byte`, `char`, `short`, `int`, `long`, `sbyte`, `ushort`, `uint`, `ulong`, `float` o `double`.  
  
```  
private fixed char name[30];  
```  
  
## <a name="remarks"></a>Note  
 Nelle versioni precedenti di C# era difficile dichiarare una struttura a dimensioni fisse di tipo C++, in quanto uno struct C# contenente una matrice non include gli elementi della matrice. Lo struct contiene invece un riferimento agli elementi.  
  
 In C# 2.0 è stata aggiunta la possibilità di incorporare una matrice di dimensioni fisse in uno [struct](../../../csharp/language-reference/keywords/struct.md) quando viene usata in un blocco di codice [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  
  
 Ad esempio, prima di C# 2.0, lo struct `struct` seguente avrebbe avuto una dimensione di 8 byte. La matrice `pathName` è un riferimento alla matrice con allocazione heap:  
  
 [!code-cs[csProgGuidePointers#19](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/fixed-size-buffers_1.cs)]  
  
 A partire da C# 2.0, un oggetto `struct` può contenere una matrice incorporata. Nell'esempio seguente la matrice `fixedBuffer` è di dimensioni fisse. Per accedere agli elementi della matrice, si usa un'istruzione `fixed` per definire un puntatore al primo elemento. L'istruzione `fixed` blocca un'istanza di `fixedBuffer` a un percorso specifico nella memoria.  
  
 [!code-cs[csProgGuidePointers#20](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/fixed-size-buffers_2.cs)]  
  
 Le dimensioni della matrice `char` a 128 elementi sono di 256 byte. I buffer [char](../../../csharp/language-reference/keywords/char.md) a dimensione fissa accettano sempre due byte per carattere, indipendentemente dalla codifica. Questo vale anche quando viene eseguito il marshalling di buffer char in metodi API o struct con `CharSet = CharSet.Auto` o `CharSet = CharSet.Ansi`. Per altre informazioni, vedere <xref:System.Runtime.InteropServices.CharSet>.  
  
 Un'altra matrice a dimensione fissa comune è la matrice [bool](../../../csharp/language-reference/keywords/bool.md). Gli elementi in una matrice `bool` hanno sempre le dimensioni di un byte. Le matrici `bool` non sono adatte per la creazione di matrici o buffer di bit.  
  
> [!NOTE]
>  Eccezione fatta per la memoria creata con [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md), il compilatore C# e Common Language Runtime (CLR) non eseguono controlli di sicurezza per sovraccarico del buffer. Come per tutto il codice unsafe, è necessario prestare la massima attenzione.  
  
 I buffer unsafe sono diversi dalle normali matrici per i motivi seguenti:  
  
-   È possibile usare i buffer unsafe solo in un contesto unsafe.  
  
-   I buffer unsafe sono sempre vettori, ovvero matrici unidimensionali.  
  
-   La dichiarazione della matrice deve includere un conteggio, ad esempio `char id[8]`. Non è invece possibile usare `char id[]`.  
  
-   I buffer unsafe possono essere solo campi di istanza di struct in un contesto unsafe.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Codice di tipo unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [Interoperabilità](../../../csharp/programming-guide/interop/index.md)
