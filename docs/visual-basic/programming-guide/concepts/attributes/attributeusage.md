---
title: AttributeUsage (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 48757216-c21d-4051-86d5-8a3e03c39d2c
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bf56f40033f9d1547d63fccd25e3c0561bb62cb1
ms.lasthandoff: 03/13/2017

---
# <a name="attributeusage-visual-basic"></a>AttributeUsage (Visual Basic)
Determina come è possibile utilizzare una classe di attributi personalizzati. `AttributeUsage`è un attributo che può essere applicato alle definizioni di attributo personalizzato per controllare come può essere applicato il nuovo attributo. Le impostazioni predefinite simile al seguente quando applicato in modo esplicito:  
  
```vb  
<System.AttributeUsage(System.AttributeTargets.All,   
                   AllowMultiple:=False,   
                   Inherited:=True)>   
Class NewAttribute  
    Inherits System.Attribute  
End Class  
```  
  
 In questo esempio, la `NewAttribute` classe può essere applicato a qualsiasi entità di codice in grado di attributo, ma può essere applicato solo una volta per ogni entità. Viene ereditata dalle classi derivate quando applicato a una classe di base.  
  
 Il `AllowMultiple` e `Inherited` gli argomenti sono facoltativi, pertanto questo codice ha lo stesso effetto:  
  
```vb  
<System.AttributeUsage(System.AttributeTargets.All)>   
Class NewAttribute  
    Inherits System.Attribute  
End Class  
```  
  
 Il primo `AttributeUsage` argomento deve essere uno o più elementi del <xref:System.AttributeTargets>enumerazione.</xref:System.AttributeTargets> Più tipi di destinazione possono essere collegati con l'operatore OR, simile al seguente:  
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Property Or AttributeTargets.Field)>   
Class NewPropertyOrFieldAttribute  
    Inherits Attribute  
End Class  
```  
  
 Se il `AllowMultiple` argomento è impostato su `true`, quindi l'attributo risulta può essere applicato più volte per una singola entità, simile al seguente:  
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Class, AllowMultiple:=True)>   
Class MultiUseAttr  
    Inherits Attribute  
End Class  
  
<MultiUseAttr(), MultiUseAttr()>   
Class Class1  
End Class  
```  
  
 In questo caso `MultiUseAttr` può essere applicato più volte perché `AllowMultiple` è impostato su `true`. Entrambi i formati indicati per applicare più attributi sono validi.  
  
 Se `Inherited` è impostato su `false`, quindi l'attributo non viene ereditato da classi che derivano da una classe con attribuita. Ad esempio:  
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Class, Inherited:=False)>   
Class Attr1  
    Inherits Attribute  
End Class  
  
<Attr1()>   
Class BClass  
  
End Class    
  
Class DClass  
    Inherits BClass  
End Class  
```  
  
 In questo caso `Attr1` non viene applicata ai `DClass` tramite ereditarietà.  
  
## <a name="remarks"></a>Note  
 Il `AttributeUsage` è un attributo monouso ovvero non può essere applicato più volte alla stessa classe. `AttributeUsage`è un alias per <xref:System.AttributeUsageAttribute>.</xref:System.AttributeUsageAttribute>  
  
 Per ulteriori informazioni, vedere [accesso agli attributi tramite Reflection utilizzando (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato l'effetto di `Inherited` e `AllowMultiple` argomenti per il `AttributeUsage` attributo, e come è possono enumerare gli attributi personalizzati applicati a una classe.  
  
```vb  
Imports System  
```  
  
```vb  
' Create some custom attributes:  
<AttributeUsage(System.AttributeTargets.Class, Inherited:=False)>   
Class A1  
    Inherits System.Attribute  
End Class  
  
<AttributeUsage(System.AttributeTargets.Class)>   
Class A2  
    Inherits System.Attribute  
End Class      
  
<AttributeUsage(System.AttributeTargets.Class, AllowMultiple:=True)>   
Class A3  
    Inherits System.Attribute  
End Class  
  
' Apply custom attributes to classes:  
<A1(), A2()>   
Class BaseClass  
  
End Class  
  
<A3(), A3()>   
Class DerivedClass  
    Inherits BaseClass  
End Class  
  
Public Class TestAttributeUsage  
    Sub Main()  
        Dim b As New BaseClass  
        Dim d As New DerivedClass  
        ' Display custom attributes for each class.  
        Console.WriteLine("Attributes on Base Class:")  
        Dim attrs() As Object = b.GetType().GetCustomAttributes(True)  
  
        For Each attr In attrs  
            Console.WriteLine(attr)  
        Next  
  
        Console.WriteLine("Attributes on Derived Class:")  
        attrs = d.GetType().GetCustomAttributes(True)  
        For Each attr In attrs  
            Console.WriteLine(attr)  
        Next              
    End Sub  
End Class  
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
 <xref:System.Attribute></xref:System.Attribute>   
 <xref:System.Reflection></xref:System.Reflection>   
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)   
 [Attributi](https://msdn.microsoft.com/library/5x6cd29c)   
 [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [Attributi (Visual Basic)](../../../../visual-basic/language-reference/attributes.md)   
 [Creazione di attributi personalizzati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/creating-custom-attributes.md)   
 [Accesso agli attributi tramite Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
