---
title: "Buffer a dimensione fissa (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "buffer a dimensione fissa [C#]"
  - "buffer unsafe [C#]"
  - "codice unsafe [C#], buffer di dimensione fissa"
ms.assetid: 6220d454-947c-4977-ac9d-9308c6ed5051
caps.latest.revision: 31
caps.handback.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Buffer a dimensione fissa (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In C\# è possibile utilizzare l'istruzione [fixed](../../../csharp/language-reference/keywords/fixed-statement.md) per creare un buffer con una matrice di dimensioni fisse in una struttura di dati.  Ciò si rivela particolarmente utile quando si utilizza codice esistente, ad esempio codice scritto in altri linguaggi, DLL preesistenti o progetti COM.  La matrice fissa può accettare attributi o modificatori consentiti per i membri struttura normali.  L'unica restrizione è rappresentata dal fatto che il tipo di matrice deve essere `bool`, `byte`, `char`, `short`, `int`, `long`, `sbyte`, `ushort`, `uint`, `ulong`, `float` o `double`.  
  
```  
private fixed char name[30];  
```  
  
## Note  
 Nelle versioni precedenti di C\# era difficile dichiarare una struttura a dimensioni fisse di tipo C\+\+, in quanto uno struct C\# contenente una matrice non include gli elementi della matrice.  Lo struct contiene invece un riferimento agli elementi.  
  
 In C\# 2.0 è stata aggiunta la possibilità di incorporare una matrice di dimensioni fisse in una [struttura](../../../csharp/language-reference/keywords/struct.md) utilizzata in un blocco di codice [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  
  
 Ad esempio, prima di C\# 2.0, il seguente `struct` avrebbe avuto una dimensione di 8 byte.  La matrice `pathName` è un riferimento alla matrice allocata sull'heap:  
  
 [!code-cs[csProgGuidePointers#19](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/fixed-size-buffers_1.cs)]  
  
 Iniziando con C\# 2.0, uno `struct` può contenere una matrice incorporata.  Nell'esempio che segue, la matrice `fixedBuffer` è di dimensioni fisse.  Per accedere agli elementi della matrice, si utilizza l'istruzione `fixed` per definire un puntatore al primo elemento.  L'istruzione `fixed` unisce un'istanza di `fixedBuffer` a un percorso specifico in memoria.  
  
 [!code-cs[csProgGuidePointers#20](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/fixed-size-buffers_2.cs)]  
  
 La dimensione della matrice `char` a 128 elementi è di 256 byte.  I buffer [char](../../../csharp/language-reference/keywords/char.md) a dimensione fissa accettano sempre due byte per carattere, indipendentemente dalla codifica.  Questo vale anche quando viene eseguito il marshalling tra i buffer char e le strutture o i metodi API con `CharSet = CharSet.Auto` o `CharSet = CharSet.Ansi`.  Per ulteriori informazioni, vedere <xref:System.Runtime.InteropServices.CharSet>.  
  
 Un'altra matrice a dimensione fissa comune è la matrice [bool](../../../csharp/language-reference/keywords/bool.md).  Gli elementi in una matrice `bool` hanno sempre la dimensione di un byte.  Le matrici `bool` non sono adatte per la creazione di matrici o buffer del bit.  
  
> [!NOTE]
>  A eccezione della memoria creata con [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md), il compilatore C\# e Common Language Runtime \(CLR\) non eseguono controlli di sicurezza per sovraccarico del buffer.  Come con tutto il codice unsafe, è necessario prestare la massima attenzione.  
  
 I buffer unsafe sono diversi dalle normali matrici per i seguenti motivi:  
  
-   È possibile utilizzare i buffer unsafe solo in un contesto unsafe.  
  
-   I buffer unsafe sono sempre vettori, ovvero matrici unidimensionali.  
  
-   La dichiarazione della matrice deve includere un conteggio, ad esempio `char id[8]`.  Non è invece possibile utilizzare `char id[]`.  
  
-   I buffer unsafe possono essere solo campi di istanza di strutture in un contesto unsafe.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [Interoperabilità](../../../csharp/programming-guide/interop/interoperability.md)