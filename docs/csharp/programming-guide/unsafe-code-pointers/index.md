---
title: "Codice unsafe e puntatori (Guida per programmatori C#) | Microsoft Docs"
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
  - "sicurezza [C#], indipendenza dai tipi"
  - "C# (linguaggio), codice unsafe"
  - "indipendenza dai tipi [C#]"
  - "unsafe (parola chiave) [C#]"
  - "codice unsafe [C#]"
  - "C# (linguaggio), puntatori"
  - "puntatori [C#], informazioni"
ms.assetid: b0fcca10-a92d-4f2a-835b-b0ccae6739ee
caps.latest.revision: 24
caps.handback.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Codice unsafe e puntatori (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Per garantire la sicurezza e assicurare l'indipendenza dai tipi, per impostazione predefinita in C\# non è supportata l'aritmetica dei puntatori.  Tuttavia, utilizzando la parola chiave [unsafe](../../../csharp/language-reference/keywords/unsafe.md), è possibile definire un contesto unsafe in cui utilizzare i puntatori.  Per ulteriori informazioni sui puntatori, vedere l'argomento [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md).  
  
> [!NOTE]
>  Nell'ambiente Common Language Runtime \(CLR\) il codice unsafe viene indicato come codice non verificabile.  In C\# il codice unsafe non è necessariamente pericoloso. Si tratta semplicemente di un codice che non può essere sottoposto a un controllo di sicurezza da parte di CLR.  Quest'ultimo, pertanto, eseguirà soltanto codice unsafe contenuto all'interno di un assembly completamente attendibile.  Se si utilizza codice unsafe, è responsabilità del programmatore garantire che tale codice non introduca problemi di sicurezza o errori di puntatore.  
  
## Cenni preliminari sul codice unsafe  
 Di seguito sono elencate le proprietà del codice unsafe:  
  
-   I metodi, i tipi e i blocchi di codice possono essere definiti come unsafe.  
  
-   In alcuni casi, il codice unsafe può migliorare le prestazioni di un'applicazione grazie alla rimozione dei controlli sui limiti delle matrici.  
  
-   Il codice unsafe è necessario quando si chiamano funzioni native che richiedono puntatori.  
  
-   L'utilizzo di codice unsafe introduce problemi di sicurezza e di stabilità.  
  
-   Per compilare codice unsafe in C\#, è necessario compilare l'applicazione con l'opzione [\/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md).  
  
## Sezioni correlate  
 Per ulteriori informazioni, vedere:  
  
-   [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)  
  
-   [Buffer a dimensione fissa](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)  
  
-   [Procedura: utilizzare puntatori per copiare una matrice di byte](../../../csharp/programming-guide/unsafe-code-pointers/how-to-use-pointers-to-copy-an-array-of-bytes.md)  
  
-   [non protette](../../../csharp/language-reference/keywords/unsafe.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)