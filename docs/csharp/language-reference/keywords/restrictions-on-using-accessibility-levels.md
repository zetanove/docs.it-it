---
title: "Restrizioni relative all&#39;utilizzo dei livelli di accessibilit&#224; (Riferimenti per C#) | Microsoft Docs"
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
  - "modificatori di accesso [C#], restrizioni relative ai livelli di accessibilità"
ms.assetid: 987e2f22-46bf-4fea-80ee-270b9cd01045
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Restrizioni relative all&#39;utilizzo dei livelli di accessibilit&#224; (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando si specifica un tipo in una dichiarazione, verificare se il livello di accessibilità del tipo dipende dal livello di accessibilità di un membro o di altro tipo.  Ad esempio, la classe base diretta deve avere almeno la stessa accessibilità della classe derivata.  Le dichiarazioni seguenti generano un errore di compilazione in quanto la classe base `BaseClass` è meno accessibile di `MyClass`:  
  
```  
class BaseClass {...}  
public class MyClass: BaseClass {...} // Error  
```  
  
 Nella seguente tabella sono riepilogate le restrizioni relative ai livelli di accessibilità dichiarati.  
  
|Contesto|Note|  
|--------------|----------|  
|[Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)|La classe base diretta di un tipo classe deve avere almeno lo stesso livello di accessibilità del tipo classe.|  
|[Interfacce](../../../csharp/programming-guide/interfaces/index.md)|Le interfacce di base esplicite di un tipo di interfaccia devono avere almeno lo stesso livello di accessibilità del tipo di interfaccia.|  
|[Delegati](../../../csharp/programming-guide/delegates/index.md)|Il tipo restituito e i tipi di parametri di un tipo delegato devono avere almeno lo stesso livello di accessibilità del tipo delegato.|  
|[Costanti](../../../csharp/programming-guide/classes-and-structs/constants.md)|Il tipo di una costante deve avere almeno lo stesso livello di accessibilità della costante.|  
|[Campi](../../../csharp/programming-guide/classes-and-structs/fields.md)|Il tipo di un campo deve avere almeno lo stesso livello di accessibilità del campo.|  
|[Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)|Il tipo restituito e i tipi di parametri di un metodo devono avere almeno lo stesso livello di accessibilità del metodo.|  
|[Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)|Il tipo di una proprietà deve avere almeno lo stesso livello di accessibilità della proprietà.|  
|[Eventi](../../../csharp/programming-guide/events/index.md)|Il tipo di un evento deve avere almeno lo stesso livello di accessibilità dell'evento.|  
|[Indicizzatori](../../../csharp/programming-guide/indexers/index.md)|Il tipo e i tipi di parametri di un indicizzatore devono avere almeno lo stesso livello di accessibilità dell'indicizzatore.|  
|[Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)|Il tipo restituito e i tipi di parametri di un operatore devono avere almeno lo stesso livello di accessibilità dell'operatore.|  
|[Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)|I tipi dei parametri di un costruttore devono avere almeno lo stesso livello di accessibilità del costruttore.|  
  
## Esempio  
 L'esempio riportato di seguito contiene dichiarazioni errate di tipi diversi.  Il commento che segue ciascuna dichiarazione indica l'errore di compilazione previsto.  
  
```  
// Restrictions on Using Accessibility Levels  
// CS0052 expected as well as CS0053, CS0056, and CS0057  
// To make the program work, change access level of both class B  
// and MyPrivateMethod() to public.  
  
using System;  
  
// A delegate:  
delegate int MyDelegate();  
  
class B  
{  
    // A private method:  
    static int MyPrivateMethod()  
    {  
        return 0;  
    }  
}  
  
public class A  
{  
    // Error: The type B is less accessible than the field A.myField.  
    public B myField = new B();  
  
    // Error: The type B is less accessible  
    // than the constant A.myConst.  
    public readonly B myConst = new B();  
  
    public B MyMethod()  
    {  
        // Error: The type B is less accessible   
        // than the method A.MyMethod.  
        return new B();  
    }  
  
    // Error: The type B is less accessible than the property A.MyProp  
    public B MyProp  
    {  
        set  
        {  
        }  
    }  
  
    MyDelegate d = new MyDelegate(B.MyPrivateMethod);  
    // Even when B is declared public, you still get the error:   
    // "The parameter B.MyPrivateMethod is not accessible due to   
    // protection level."  
  
    public static B operator +(A m1, B m2)  
    {  
        // Error: The type B is less accessible  
        // than the operator A.operator +(A,B)  
        return new B();  
    }  
  
    static void Main()  
    {  
        Console.Write("Compiled successfully");  
    }  
}  
```  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [Dominio di accessibilità](../../../csharp/language-reference/keywords/accessibility-domain.md)   
 [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [Protected](../../../csharp/language-reference/keywords/protected.md)   
 [interne](../../../csharp/language-reference/keywords/internal.md)