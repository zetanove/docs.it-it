---
title: Creazione di attributi personalizzati (C#) | Microsoft Docs
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
ms.assetid: 500e1977-c6de-462d-abce-78a0eb1eda22
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
ms.openlocfilehash: b71bf8fe1f4d448bf373fcab4bccd89bca4672b8
ms.lasthandoff: 03/13/2017

---
# <a name="creating-custom-attributes-c"></a>Creazione di attributi personalizzati (C#)
È possibile creare i propri attributi personalizzati definendo una classe Attribute, una classe che deriva direttamente o indirettamente da <xref:System.Attribute>, semplificando e rendendo più rapida l'identificazione delle definizioni degli attributi nei metadati. Si supponga di voler contrassegnare i tipi con il nome del programmatore che ha scritto il tipo. Si potrebbe definire una classe Attribute `Author` personalizzata:  
  
```csharp  
[System.AttributeUsage(System.AttributeTargets.Class |  
                       System.AttributeTargets.Struct)  
]  
public class Author : System.Attribute  
{  
    private string name;  
    public double version;  
  
    public Author(string name)  
    {  
        this.name = name;  
        version = 1.0;  
    }  
}  
```  
  
 Il nome della classe è il nome dell'attributo, `Author`. La classe deriva da `System.Attribute`, quindi è una classe Attribute personalizzata. I parametri del costruttore sono parametri posizionali dell'attributo personalizzato. In questo esempio `name` è un parametro posizionale. Tutte le proprietà o i campi pubblici di lettura/scrittura sono parametri denominati. In questo caso `version` è l'unico parametro denominato. Si noti l'uso dell'attributo `AttributeUsage` per rendere l'attributo `Author` valido solo per la classe e le dichiarazioni `struct`.  
  
 È possibile usare questo nuovo attributo come indicato di seguito:  
  
```csharp  
[Author("P. Ackerman", version = 1.1)]  
class SampleClass  
{  
    // P. Ackerman's code goes here...  
}  
```  
  
 `AttributeUsage` ha un parametro denominato, `AllowMultiple`, che consente di rendere un attributo personalizzato monouso o multiuso. Nell'esempio di codice seguente viene creato un attributo multiuso.  
  
```csharp  
[System.AttributeUsage(System.AttributeTargets.Class |  
                       System.AttributeTargets.Struct,  
                       AllowMultiple = true)  // multiuse attribute  
]  
public class Author : System.Attribute  
```  
  
 Nell'esempio vengono applicati a una classe più attributi dello stesso tipo.  
  
```csharp  
[Author("P. Ackerman", version = 1.1)]  
[Author("R. Koch", version = 1.2)]  
class SampleClass  
{  
    // P. Ackerman's code goes here...  
    // R. Koch's code goes here...  
}  
```  
  
> [!NOTE]
>  Se la classe Attribute contiene una proprietà, tale proprietà deve essere di lettura/scrittura.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Reflection>   
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)   
 [Scrittura di attributi personalizzati](http://msdn.microsoft.com/library/97216f69-bde8-49fd-ac40-f18c500ef5dc)   
 [Reflection (C#)](../../../../csharp/programming-guide/concepts/reflection.md)   
 [Attributi (C#)](../../../../csharp/programming-guide/concepts/attributes/index.md)   
 [Accessing Attributes by Using Reflection (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)  (Accesso agli attributi con reflection (C#))  
 [AttributeUsage (C#)](../../../../csharp/programming-guide/concepts/attributes/attributeusage.md)
