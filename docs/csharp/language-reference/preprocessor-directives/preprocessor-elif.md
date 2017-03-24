---
title: "#elif (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#elif"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#elif (direttiva) [C#]"
ms.assetid: 731d78df-08e0-4d51-b8c8-f193c27de13f
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# #elif (Riferimenti per C#)
`#elif` consente di creare una direttiva condizionale composita.  L'espressione `#elif` viene valutata quando né l'espressione [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) che ogni precedente, eventuale espressione delle direttive `#elif` valuta a `true`.  Se un'espressione `#elif` restituisce `true`, il compilatore valuterà tutto il codice compreso tra `#elif` e la direttiva condizionale successiva.  Ad esempio:  
  
```  
#define VC7  
//...  
#if debug  
    Console.Writeline("Debug build");  
#elif VC7  
    Console.Writeline("Visual Studio 7");  
#endif  
```  
  
 È possibile utilizzare gli operatori `==` \(uguaglianza\), `!=` \(disuguaglianza\), `&&` \(and\) e `||` \(or\) per valutare più simboli.  È anche possibile raggruppare simboli e operatori tra parentesi.  
  
## Note  
 `#elif` equivale all'uso di  
  
```  
#else  
#if  
```  
  
 L'utilizzo di `#elif` è più semplice poiché ciascuna espressione `#if` richiede un'espressione [\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md), mentre un'espressione `#elif` può essere utilizzata senza un'espressione `#endif` corrispondente.  
  
 Per un esempio sull'utilizzo di `#elif`, vedere [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)