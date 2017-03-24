---
title: "internal (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "internal_CSharpKeyword"
  - "internal"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "internal (parola chiave) [C#]"
ms.assetid: 6ee0785c-d7c8-49b8-bb72-0a4dfbcb6461
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# internal (Riferimenti per C#)
La parola chiave `internal` è [modificatore di accesso](../../../csharp/language-reference/keywords/access-modifiers.md) per i tipi e i membri del tipo.  I tipi e i membri interni sono accessibili soltanto all'interno dei file nello stesso assembly, come nell'esempio riportato di seguito:  
  
```  
public class BaseClass   
{  
    // Only accessible within the same assembly  
    internal static int x = 0;  
}  
```  
  
 È possibile accedere ai tipi o ai membri che dispongono di modificatore di accesso `protected internal` dall'assembly corrente o dai tipi derivati dalla classe che li contiene.  
  
 Per un confronto tra il modificatore di accesso `internal` e gli altri modificatori di accesso, vedere [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md) e [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 Per ulteriori informazioni sugli assembly, vedere [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md).  
  
 L'accesso interno viene generalmente utilizzato a livello di sviluppo dei componenti poiché consente a un gruppo di componenti di interagire in modo privato senza esporre le proprie funzionalità al resto del codice dell'applicazione.  Ad esempio, un framework per la compilazione di interfacce utente grafiche potrebbe fornire le classi `Control` e `Form` che interagiscono utilizzando membri con accesso interno.  Poiché questi membri sono interni, non sono esposti al codice che utilizza il framework.  
  
 È errato fare riferimento a un tipo o a un membro con accesso interno all'esterno dell'assembly in cui è stato definito.  
  
## Esempio  
 Nell'esempio sono inclusi due file, `Assembly1.cs` e `Assembly1`\_`a.cs`.  Il primo file contiene una classe base interna `BaseClass`.  Nel secondo file, un tentativo di creare un'istanza di `BaseClass` genererà un errore.  
  
```  
// Assembly1.cs  
// Compile with: /target:library  
internal class BaseClass   
{  
   public static int intM = 0;  
}  
```  
  
```  
// Assembly1_a.cs  
// Compile with: /reference:Assembly1.dll  
class TestAccess   
{  
   static void Main()   
   {  
      BaseClass myBase = new BaseClass();   // CS0122  
   }  
}  
```  
  
## Esempio  
 Nell'esempio riportato di seguito, utilizzare gli stessi file dell'esempio 1 e modificare il livello di accessibilità di `BaseClass` impostandolo su `public`.  Modificare anche il livello di accessibilità del membro `IntM` impostandolo su `internal`.  In questo caso, è possibile creare l'istanza della classe, ma non è possibile accedere al membro interno.  
  
```  
// Assembly2.cs  
// Compile with: /target:library  
public class BaseClass   
{  
   internal static int intM = 0;  
}  
```  
  
```  
// Assembly2_a.cs  
// Compile with: /reference:Assembly1.dll  
public class TestAccess   
{  
   static void Main()   
   {  
      BaseClass myBase = new BaseClass();   // Ok.  
      BaseClass.intM = 444;    // CS0117  
   }  
}  
```  
  
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
 [private](../../../csharp/language-reference/keywords/private.md)   
 [Protected](../../../csharp/language-reference/keywords/protected.md)