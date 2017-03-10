---
title: "bool (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "bool_CSharpKeyword"
  - "bool"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "bool (parola chiave) [C#]"
ms.assetid: 551cfe35-2632-4343-af49-33ad12da08e2
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# bool (Riferimenti per C#)
La parola chiave `bool` è un alias di <xref:System.Boolean?displayProperty=fullName>.  Viene utilizzata per dichiarare variabili per archiviare i valori Boolean, [true](../../../csharp/language-reference/keywords/true.md) e [false](../../../csharp/language-reference/keywords/false.md).  
  
> [!NOTE]
>  Se è necessaria una variabile booleana che possa avere anche il valore `null`, utilizzare `bool?`.  Per ulteriori informazioni, vedere [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md).  
  
## Valori letterali  
 È possibile assegnare un valore Boolean a una variabile `bool`.  È inoltre possibile assegnare un'espressione che restituisce `bool` a una variabile `bool`.  
  
 [!code-cs[csrefKeywordsTypes#1](../../../csharp/language-reference/keywords/codesnippet/csharp/bool_1.cs)]  
  
 Il valore predefinito di una variabile `bool` è `false`.  Il valore predefinito di una variabile `bool?` è `null`.  
  
## Conversioni  
 In C\+\+ un valore di tipo `bool` può essere convertito in un valore di tipo `int`. In altri termini, `false` è equivalente a zero e `true` è equivalente a valori diversi da zero.  In C\# non viene eseguita alcuna conversione tra il tipo `bool` e gli altri tipi.  Ad esempio, l'istruzione `if` seguente non è valida in C\#:  
  
 [!code-cs[csrefKeywordsTypes#2](../../../csharp/language-reference/keywords/codesnippet/csharp/bool_2.cs)]  
  
 Per eseguire il test di una variabile di tipo `int`, è necessario confrontarla esplicitamente con un valore, ad esempio zero, come illustrato di seguito:  
  
 [!code-cs[csrefKeywordsTypes#3](../../../csharp/language-reference/keywords/codesnippet/csharp/bool_3.cs)]  
  
## Esempio  
 In questo esempio, il programma controlla che il carattere inserito da tastiera sia una lettera.  In caso affermativo, controlla se il carattere è minuscolo o maiuscolo  Questi controlli vengono eseguiti con <xref:System.Char.IsLetter%2A> e <xref:System.Char.IsLower%2A>, che restituiscono il tipo `bool`:  
  
 [!code-cs[csrefKeywordsTypes#4](../../../csharp/language-reference/keywords/codesnippet/csharp/bool_4.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)