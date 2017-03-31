---
title: 'Procedura: Creare un&quot;unione C-C++ tramite attributi (C#) | Microsoft Docs'
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
ms.assetid: 85f35e56-26e0-4d31-9f3a-89bd4005e71a
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
ms.openlocfilehash: dd6bc60dfd1c6146d8fa72abdcfc6a00006817aa
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-cc-union-by-using-attributes-c"></a>Procedura: Creare un'unione C-C++ tramite attributi (C#)
L'uso degli attributi consente di personalizzare la disposizione degli struct in memoria. Ad esempio, tramite gli attributi `StructLayout(LayoutKind.Explicit)` e `FieldOffset` è possibile creare una struttura che in C/C++ è nota come unione.  
  
## <a name="example"></a>Esempio  
 In questo segmento di codice tutti i campi di `TestUnion` iniziano in corrispondenza della stessa posizione di memoria.  
  
```csharp  
// Add a using directive for System.Runtime.InteropServices.  
  
       [System.Runtime.InteropServices.StructLayout(LayoutKind.Explicit)]  
       struct TestUnion  
       {  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public int i;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public double d;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public char c;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public byte b;  
       }  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente i campi iniziano in corrispondenza di posizioni diverse impostate in modo esplicito.  
  
```csharp  
// Add a using directive for System.Runtime.InteropServices.  
  
       [System.Runtime.InteropServices.StructLayout(LayoutKind.Explicit)]  
       struct TestExplicit  
       {  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public long lg;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public int i1;  
  
           [System.Runtime.InteropServices.FieldOffset(4)]  
           public int i2;  
  
           [System.Runtime.InteropServices.FieldOffset(8)]  
           public double d;  
  
           [System.Runtime.InteropServices.FieldOffset(12)]  
           public char c;  
  
           [System.Runtime.InteropServices.FieldOffset(14)]  
           public byte b;  
       }  
```  
  
 I due campi integer, `i1` e `i2`, condividono le stesse posizioni di memoria di `lg`. Questo tipo di controllo sul layout degli struct è utile quando si usa la chiamata di piattaforma.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Reflection>   
 <xref:System.Attribute>   
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)   
 [Attributi](https://msdn.microsoft.com/library/5x6cd29c)   
 [Reflection (C#)](../../../../csharp/programming-guide/concepts/reflection.md)   
 [Attributes (C#)](../../../../csharp/programming-guide/concepts/attributes/index.md)  (Attributi (C#))  
 [Creazione di attributi personalizzati (C#)](../../../../csharp/programming-guide/concepts/attributes/creating-custom-attributes.md)   
 [Accessing Attributes by Using Reflection (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md) (Accesso agli attributi tramite reflection (C#))
