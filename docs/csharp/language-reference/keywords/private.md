---
title: "private (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "private_CSharpKeyword"
  - "private"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "private (parola chiave) [C#]"
ms.assetid: 654c0bb8-e6ac-4086-bf96-7474fa6aa1c8
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# private (Riferimenti per C#)
La parola chiave `private` è un modificatore di accesso per membri.  L'accesso privato è il livello di accesso più restrittivo.  I membri privati sono accessibili solo all'interno del corpo della classe o della struttura in cui sono stati dichiarati, come nell'esempio riportato di seguito:  
  
```  
class Employee  
{  
    private int i;  
    double d;   // private access by default  
}  
```  
  
 Anche i tipi annidati dello stesso corpo possono accedere a tali membri privati.  
  
 Fare riferimento a un membro privato all'esterno della classe o della struttura in cui è stato dichiarato genera un errore in fase di compilazione.  
  
 Per un confronto tra il modificatore di accesso `private` e gli altri modificatori di accesso, vedere [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md) e [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
## Esempio  
 Nell'esempio riportato di seguito la classe `Employee` contiene due membri dati privati, `name` e `salary`.  Essendo privati, i membri risulteranno accessibili solo ai metodi di membro.  I metodi pubblici `GetName` e `Salary` vengono aggiunti per consentire il controllo dell'accesso ai membri privati.  È possibile accedere al membro `name` tramite un metodo pubblico e al membro `salary` tramite una proprietà pubblica di sola lettura.  Per ulteriori informazioni, vedere [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md).  
  
 [!code-cs[csrefKeywordsModifiers#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/private_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [Protected](../../../csharp/language-reference/keywords/protected.md)   
 [interne](../../../csharp/language-reference/keywords/internal.md)