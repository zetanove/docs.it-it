---
title: "unsafe (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "unsafe_CSharpKeyword"
  - "unsafe"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "unsafe (parola chiave) [C#]"
ms.assetid: 7e818009-1c6e-4b9e-b769-3728a01586a0
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# unsafe (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `unsafe` denota un contesto unsafe, che è richiesto per qualsiasi operazione che comporti l'uso dei puntatori.  Per ulteriori informazioni, vedere [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md).  
  
 È possibile utilizzare il modificatore `unsafe` nella dichiarazione di un tipo o di un membro.  L'intero ambito testuale del tipo o del membro viene pertanto considerato un contesto unsafe.  Di seguito è ad esempio riportato un metodo dichiarato con il modificatore `unsafe`:  
  
```  
  
      unsafe static void FastCopy(byte[] src, byte[] dst, int count)  
{  
    // Unsafe context: can use pointers here.  
}  
```  
  
 L'ambito del contesto unsafe si estende dall'elenco dei parametri fino alla fine del metodo. In questo modo, è possibile utilizzare puntatori anche nell'elenco dei parametri.  
  
```  
  
unsafe static void FastCopy ( byte* ps, byte* pd, int count ) {...}  
```  
  
 È anche possibile utilizzare un blocco unsafe per consentire l'uso di un codice unsafe all'interno del blocco.  Di seguito è riportato un esempio:  
  
```  
  
      unsafe  
{  
    // Unsafe context: can use pointers here.  
}  
```  
  
 Per compilare codice unsafe, è necessario specificare l'opzione del compilatore [\/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md).  Il codice unsafe non può essere verificato da Common Language Runtime.  
  
## Esempio  
 [!code-cs[csrefKeywordsModifiers#22](../../../csharp/language-reference/keywords/codesnippet/CSharp/unsafe_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Buffer a dimensione fissa](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)