---
title: "Passaggio di parametri (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "argomenti [C#]"
  - "linguaggio C#, parametri di metodo"
  - "metodi [C#], passaggio di parametri"
  - "parametri [C#], passaggio"
  - "passaggio di parametri [C#]"
ms.assetid: a5c3003f-7441-4710-b8b1-c79de77e0b77
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Passaggio di parametri (Guida per programmatori C#)
In C\# è possibile passare argomenti a parametri per valore o per riferimento.  Il passaggio per riferimento consente ai membri delle funzioni, metodi, proprietà, indicizzatori, operatori e costruttori di modificare il valore dei parametri e rendere permanenti le modifiche nell'ambiente chiamante.  Per passare un parametro per riferimento, è possibile utilizzare la parola chiave `ref` o `out`.  Per semplicità, negli esempi riportati in questo argomento verrà utilizzata soltanto la parola chiave `ref`.  Per ulteriori informazioni sulla differenza tra `ref` e `out`, vedere [ref](../../../csharp/language-reference/keywords/ref.md), [out](../../../csharp/language-reference/keywords/out.md) e [Passaggio di matrici mediante ref e out](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md).  
  
 Nell'esempio seguente viene illustrata la differenza fra parametri di valore e di riferimento.  
  
 [!code-cs[csProgGuideParameters#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-parameters_1.cs)]  
  
 Per ulteriori informazioni, vedere i seguenti argomenti:  
  
-   [Passaggio di parametri di tipi di valore](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md)  
  
-   [Passaggio di parametri di tipi di riferimento](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)