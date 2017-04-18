---
title: Accesso agli attributi tramite Reflection (Visual Basic) | Documenti di Microsoft
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
ms.assetid: c56e41da-5433-464f-a7bf-2a722e78bc9f
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4763eccc5d1a6bdf3e89c1c4d825d5ff5c6caa3e
ms.lasthandoff: 03/13/2017

---
# <a name="accessing-attributes-by-using-reflection-visual-basic"></a>Accesso agli attributi tramite Reflection (Visual Basic)
Il fatto che è possibile definire gli attributi personalizzati e inserirli nel codice sorgente sarebbe di scarso valore senza un metodo per recuperare le informazioni e che agisce su di esso. Tramite la reflection per recuperare le informazioni che è state definite con gli attributi personalizzati. Il metodo chiave è `GetCustomAttributes`, che restituisce una matrice di oggetti che rappresentano gli equivalenti in fase di esecuzione degli attributi di codice sorgente. Questo metodo dispone di diverse versioni di overload. Per ulteriori informazioni, vedere <xref:System.Attribute>.</xref:System.Attribute>  
  
 Specifica un attributo, ad esempio:  
  
```vb  
<Author("P. Ackerman", Version:=1.1)>   
Class SampleClass  
    ' P. Ackerman's code goes here...  
End Class  
```  
  
 è concettualmente equivalente a questa:  
  
```vb  
Dim anonymousAuthorObject As Author = New Author("P. Ackerman")  
anonymousAuthorObject.version = 1.1  
```  
  
 Tuttavia, il codice viene eseguito solo `SampleClass` viene eseguita una query per gli attributi. La chiamata a `GetCustomAttributes` su `SampleClass` provoca un `Author` oggetto viene costruito e inizializzato come descritto in precedenza. Se la classe dispone di altri attributi, gli altri oggetti attributo sono costruiti in modo analogo. `GetCustomAttributes`Restituisce quindi il `Author` oggetto e altri oggetti attributo in una matrice. È quindi possibile scorrere questa matrice, determinare gli attributi che sono stati applicati in base al tipo di ogni elemento della matrice ed estrarre informazioni da oggetti attributo.  
  
## <a name="example"></a>Esempio  
 Ecco un esempio completo. Un attributo personalizzato viene definito, applicato a varie entità e recuperato tramite reflection.  
  
```vb  
' Multiuse attribute  
<System.AttributeUsage(System.AttributeTargets.Class Or   
                       System.AttributeTargets.Struct,   
                       AllowMultiple:=True)>   
Public Class Author  
    Inherits System.Attribute  
    Private name As String  
    Public version As Double  
    Sub New(ByVal authorName As String)  
        name = authorName  
  
        ' Default value  
        version = 1.0  
    End Sub  
  
    Function GetName() As String  
        Return name  
    End Function          
End Class  
  
' Class with the Author attribute  
<Author("P. Ackerman")>   
Public Class FirstClass  
End Class  
  
' Class without the Author attribute  
Public Class SecondClass  
End Class  
  
' Class with multiple Author attributes.  
<Author("P. Ackerman"), Author("R. Koch", Version:=2.0)>   
Public Class ThirdClass  
End Class  
  
Class TestAuthorAttribute  
    Sub Main()  
        PrintAuthorInfo(GetType(FirstClass))  
        PrintAuthorInfo(GetType(SecondClass))  
        PrintAuthorInfo(GetType(ThirdClass))  
    End Sub  
  
    Private Shared Sub PrintAuthorInfo(ByVal t As System.Type)  
        System.Console.WriteLine("Author information for {0}", t)  
  
        ' Using reflection  
        Dim attrs() As System.Attribute = System.Attribute.GetCustomAttributes(t)  
  
        ' Displaying output  
        For Each attr In attrs  
            Dim a As Author = CType(attr, Author)  
            System.Console.WriteLine("   {0}, version {1:f}", a.GetName(), a.version)  
        Next              
    End Sub  
  
    ' Output:  
    '   Author information for FirstClass  
    '     P. Ackerman, version 1.00  
    ' Author information for SecondClass  
    ' Author information for ThirdClass  
    '  R. Koch, version 2.00  
    '  P. Ackerman, version 1.00  
  
End Class  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Reflection></xref:System.Reflection>   
 <xref:System.Attribute></xref:System.Attribute>   
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)   
 [Recupero di informazioni memorizzate negli attributi](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c)   
 [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [Attributi (Visual Basic)](../../../../visual-basic/language-reference/attributes.md)   
 [Creazione di attributi personalizzati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/creating-custom-attributes.md)
