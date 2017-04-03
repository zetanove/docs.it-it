---
title: AttributeUsage (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 22c45568-9a6a-4c2f-8480-f38c1caa0a99
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6f6c72c8152cc0f76085efbaa99ec63e50d1b676
ms.lasthandoff: 03/13/2017

---
# <a name="attributeusage-c"></a>AttributeUsage (C#)
Determina come usare una classe di attributi personalizzati. `AttributeUsage` è un attributo che può essere applicato alle definizioni di attributi personalizzati per controllare come può essere applicato il nuovo attributo. Le impostazioni predefinite sono simili alle seguenti quando vengono applicate in modo esplicito:  
  
```csharp  
[System.AttributeUsage(System.AttributeTargets.All,  
                   AllowMultiple = false,  
                   Inherited = true)]  
class NewAttribute : System.Attribute { }  
```  
  
 In questo esempio, la classe `NewAttribute` può essere applicata a qualsiasi entità di codice abilitata per l'attributo, ma può essere applicata solo una volta per ogni entità. Viene ereditata dalle classi derivate quando applicata a una classe di base.  
  
 Gli argomenti `AllowMultiple` e `Inherited` sono facoltativi, pertanto questo codice ha lo stesso effetto:  
  
```csharp  
[System.AttributeUsage(System.AttributeTargets.All)]  
class NewAttribute : System.Attribute { }  
```  
  
 Il primo argomento `AttributeUsage` deve consistere di uno o più elementi dell'enumerazione <xref:System.AttributeTargets>. Più tipi di destinazione possono essere collegati con l'operatore OR, nel modo seguente:  
  
```csharp  
using System;  
```  
  
```csharp  
[AttributeUsage(AttributeTargets.Property | AttributeTargets.Field)]  
class NewPropertyOrFieldAttribute : Attribute { }  
```  
  
 Se l'argomento `AllowMultiple` è impostato su `true`, l'attributo restituito può essere applicato più volte a una singola entità, nel modo seguente:  
  
```csharp  
using System;  
```  
  
```csharp  
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]  
class MultiUseAttr : Attribute { }  
  
[MultiUseAttr]  
[MultiUseAttr]  
class Class1 { }  
  
[MultiUseAttr, MultiUseAttr]  
class Class2 { }  
```  
  
 In questo caso `MultiUseAttr` può essere applicato più volte perché `AllowMultiple` è impostato su `true`. Entrambi i formati illustrati per applicare più attributi sono validi.  
  
 Se `Inherited` è impostato su `false`, l'attributo non viene ereditato da classi che derivano da una classe con attributi. Ad esempio:  
  
```csharp  
using System;  
```  
  
```csharp  
[AttributeUsage(AttributeTargets.Class, Inherited = false)]  
class Attr1 : Attribute { }  
  
[Attr1]  
class BClass { }  
  
class DClass : BClass { }  
```  
  
 In questo caso `Attr1` non viene applicato a `DClass` attraverso l'ereditarietà.  
  
## <a name="remarks"></a>Note  
 L'attributo `AttributeUsage` è un attributo monouso ovvero non può essere applicato più volte alla stessa classe. `AttributeUsage` è un alias per <xref:System.AttributeUsageAttribute>.  
  
 Per altre informazioni, vedere [Accesso agli attributi tramite reflection (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md).  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra l'effetto degli argomenti `Inherited` e `AllowMultiple` nell'attributo `AttributeUsage` e come gli attributi personalizzati applicati a una classe possono essere enumerati.  
  
```csharp  
using System;  
```  
  
```csharp  
// Create some custom attributes:  
[AttributeUsage(System.AttributeTargets.Class, Inherited = false)]  
class A1 : System.Attribute { }  
  
[AttributeUsage(System.AttributeTargets.Class)]  
class A2 : System.Attribute { }  
  
[AttributeUsage(System.AttributeTargets.Class, AllowMultiple = true)]  
class A3 : System.Attribute { }  
  
// Apply custom attributes to classes:  
[A1, A2]  
class BaseClass { }  
  
[A3, A3]  
class DerivedClass : BaseClass { }  
  
public class TestAttributeUsage  
{  
    static void Main()  
    {  
        BaseClass b = new BaseClass();  
        DerivedClass d = new DerivedClass();  
  
        // Display custom attributes for each class.  
        Console.WriteLine("Attributes on Base Class:");  
        object[] attrs = b.GetType().GetCustomAttributes(true);  
        foreach (Attribute attr in attrs)  
        {  
            Console.WriteLine(attr);  
        }  
  
        Console.WriteLine("Attributes on Derived Class:");  
        attrs = d.GetType().GetCustomAttributes(true);  
        foreach (Attribute attr in attrs)  
        {  
            Console.WriteLine(attr);  
        }  
    }  
}  
```  
  
## <a name="sample-output"></a>Esempio di output  
  
```  
Attributes on Base Class:  
A1  
A2  
Attributes on Derived Class:  
A3  
A3  
A2  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Attribute>   
 <xref:System.Reflection>   
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)   
 [Attributi](https://msdn.microsoft.com/library/5x6cd29c)   
 [Reflection (C#)](../../../../csharp/programming-guide/concepts/reflection.md)   
 [Attributi](../../../../csharp/programming-guide/concepts/attributes/index.md)   
 [Creazione di attributi personalizzati (C#)](../../../../csharp/programming-guide/concepts/attributes/creating-custom-attributes.md)   
 [Accesso agli attributi tramite reflection (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
