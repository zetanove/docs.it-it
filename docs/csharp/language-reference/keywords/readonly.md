---
title: "readonly (Riferimenti per C#) | Microsoft Docs"
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
  - "readonly_CSharpKeyword"
  - "readonly"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "readonly (parola chiave) [C#]"
ms.assetid: 2f8081f6-0de2-4903-898d-99696c48d2f4
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# readonly (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `readonly` è un modificatore che è possibile utilizzare per i campi.  Se la dichiarazione di un campo include un modificatore `readonly`, le assegnazioni ai campi introdotte dalla dichiarazione potranno esistere solo come parte della dichiarazione o in un costruttore della stessa classe.  
  
## Esempio  
 Nell'esempio riportato di seguito, il valore del campo `year` non può essere modificato nel metodo `ChangeYear`, anche se ad esso è assegnato un valore nel costruttore della classe:  
  
 [!code-cs[csrefKeywordsModifiers#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/readonly_1.cs)]  
  
 È possibile assegnare un valore a un campo `readonly` solo nei contesti descritti di seguito:  
  
-   Quando si inizializza la variabile nella dichiarazione, ad esempio:  
  
    ```  
    public readonly int y = 5;  
    ```  
  
-   Per un campo di un'istanza, nei costruttori di istanza della classe contenente la dichiarazione di campo oppure, per un campo static, nel costruttore static della classe contenente la dichiarazione di campo.  Questi sono gli unici contesti in cui è valido passare un campo `readonly` come parametro [out](../../../csharp/language-reference/keywords/out.md) o [ref](../../../csharp/language-reference/keywords/ref.md).  
  
> [!NOTE]
>  La parola chiave `readonly` è diversa dalla parola chiave [const](../../../csharp/language-reference/keywords/const.md).  Un campo `const` può essere inizializzato solo nella dichiarazione del campo,  Un campo `readonly` può essere inizializzato nella dichiarazione o in un costruttore.  I campi `readonly` possono quindi presentare valori diversi a seconda del costruttore utilizzato.  Inoltre, mentre un campo `const` rappresenta una costante della fase di compilazione, il campo `readonly` può essere utilizzato per le costanti in fase di esecuzione, come nell'esempio riportato di seguito:  
  
```  
public static readonly uint timeStamp = (uint)DateTime.Now.Ticks;  
```  
  
## Esempio  
 [!code-cs[csrefKeywordsModifiers#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/readonly_2.cs)]  
  
 Nell'esempio precedente, se si utilizza una dichiarazione di questo tipo:  
  
 `p2.y = 66;        // Error`  
  
 verrà visualizzato il seguente messaggio di errore del compilatore:  
  
 `The left-hand side of an assignment must be an l-value`  
  
 Si tratta dello stesso errore che viene restituito quando si tenta di assegnare un valore a una costante.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [const](../../../csharp/language-reference/keywords/const.md)   
 [Campi](../../../csharp/programming-guide/classes-and-structs/fields.md)