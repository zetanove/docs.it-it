---
title: "void (Riferimenti per C#) | Microsoft Docs"
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
  - "void_CSharpKeyword"
  - "void"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "void (parola chiave) [C#]"
ms.assetid: 0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# void (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una volta utilizzato come tipo restituito di un metodo, `void` specifica che il metodo non restituisce un valore.  
  
 `void` non è consentito nell'elenco di parametri di un metodo.  Un metodo che non richiede parametri e che non restituisce alcun valore viene dichiarato come segue:  
  
```  
public void SampleMethod()  
{  
    // Body of the method.  
}  
  
```  
  
 `void` viene utilizzato anche in un contesto unsafe per dichiarare un puntatore a un tipo sconosciuto.  Per ulteriori informazioni, vedere [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md).  
  
 `void` è un alias per il tipo <xref:System.Void?displayProperty=fullName> di .NET Framework.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Tipi valore](../../../csharp/language-reference/keywords/value-types.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)