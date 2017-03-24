---
title: "volatile (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "volatile_CSharpKeyword"
  - "volatile"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "volatile (parola chiave) [C#]"
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
caps.latest.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 29
---
# volatile (Riferimenti per C#)
La parola chiave `volatile` indica che un campo potrebbe essere modificato da più thread in esecuzione contemporaneamente.  I campi dichiarati `volatile` non sono soggetti a ottimizzazioni del compilatore che presuppongono l'accesso da un singolo thread.  In questo modo nel campo è sempre presente il valore più aggiornato.  
  
 Il modificatore `volatile` è utilizzato in genere per un campo al quale accedono più thread senza ricorrere all'istruzione [lock](../../../csharp/language-reference/keywords/lock-statement.md) per la serializzazione dell'accesso.  
  
 La parola chiave `volatile` può essere applicata ai seguenti tipi di campi:  
  
-   Tipi di riferimento.  
  
-   Tipi puntatore in un contesto unsafe.  Si noti che mentre il puntatore stesso può essere volatile, l'oggetto al quale punta non può esserlo.  In altre parole, non è possibile dichiarare un "puntatore volatile".  
  
-   Tipi quali sbyte, byte, short, ushort, int, uint, char, float e bool.  
  
-   Il tipo enum con uno dei tipi di base seguenti: byte, sbyte, short, ushort, int o uint.  
  
-   Parametri di tipo generico riconosciuti come tipi di riferimento.  
  
-   <xref:System.IntPtr> e <xref:System.UIntPtr>.  
  
 La parola chiave volatile può essere applicata solo a campi di una classe o una struttura.  Le variabili locali non possono essere dichiarate `volatile`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come dichiarare la variabile di un campo pubblico come `volatile`.  
  
 [!code-cs[csrefKeywordsModifiers#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_1.cs)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come creare un thread ausiliario o di lavoro da utilizzare per eseguire l'elaborazione in parallelo con quella del thread primario.  Per informazioni complementari sul multithreading, vedere [Threading](../Topic/Managed%20Threading.md) e [Threading](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md).  
  
 [!code-cs[csProgGuideThreading#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)