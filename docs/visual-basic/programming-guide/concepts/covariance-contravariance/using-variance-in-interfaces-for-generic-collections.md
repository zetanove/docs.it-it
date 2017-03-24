---
title: Utilizzo della varianza nelle interfacce per le raccolte generiche (Visual Basic) | Documenti di Microsoft
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
ms.assetid: c867fcea-7462-4995-b9c5-542feec74036
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
ms.openlocfilehash: 86184c7de3fe16148bf954b16d703ca682216337
ms.lasthandoff: 03/13/2017

---
# <a name="using-variance-in-interfaces-for-generic-collections-visual-basic"></a>Utilizzo della varianza nelle interfacce per le raccolte generiche (Visual Basic)
Un'interfaccia covariante consente ai metodi restituire più tipi derivati da quelle specificate nell'interfaccia. Un'interfaccia controvariante consente ai metodi di accettare parametri di tipi meno derivati di quelli specificati nell'interfaccia.  
  
 In .NET Framework 4, diverse interfacce esistenti diventano covarianti e controvarianti. Sono inclusi <xref:System.Collections.Generic.IEnumerable%601>e <xref:System.IComparable%601>.</xref:System.IComparable%601> </xref:System.Collections.Generic.IEnumerable%601> In questo modo è possibile riutilizzare i metodi che operano con raccolte generiche di tipi di base per le raccolte di tipi derivati.  
  
 Per un elenco di interfacce variant in .NET Framework, vedere [varianza nelle interfacce generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md).  
  
## <a name="converting-generic-collections"></a>Conversione di raccolte generiche  
 L'esempio seguente illustra i vantaggi del supporto di covarianza nel <xref:System.Collections.Generic.IEnumerable%601>interfaccia.</xref:System.Collections.Generic.IEnumerable%601> Il `PrintFullName` metodo accetta una raccolta del `IEnumerable(Of Person)` tipo come parametro. Tuttavia, è possibile riutilizzarlo per una raccolta di `IEnumerable(Of Person)` tipo perché `Employee` eredita `Person`.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
## <a name="comparing-generic-collections"></a>Confronto di raccolte generiche  
 L'esempio seguente illustra i vantaggi del supporto della controvarianza nella <xref:System.Collections.Generic.IComparer%601>interfaccia.</xref:System.Collections.Generic.IComparer%601> La classe `PersonComparer` implementa l'interfaccia `IComparer(Of Person)`. Tuttavia, è possibile riutilizzare questa classe per una sequenza di oggetti di confrontare il `Employee` tipo perché `Employee` eredita `Person`.  
  
```vb  
' Simple hierarhcy of classes.  
Public Class Person  
    Public Property FirstName As String  
    Public Property LastName As String  
End Class  
  
Public Class Employee  
    Inherits Person  
End Class  
' The custom comparer for the Person type  
' with standard implementations of Equals()  
' and GetHashCode() methods.  
Class PersonComparer  
    Implements IEqualityComparer(Of Person)  
  
    Public Function Equals1(  
        ByVal x As Person,  
        ByVal y As Person) As Boolean _  
        Implements IEqualityComparer(Of Person).Equals  
  
        If x Is y Then Return True  
        If x Is Nothing OrElse y Is Nothing Then Return False  
        Return (x.FirstName = y.FirstName) AndAlso  
            (x.LastName = y.LastName)  
    End Function  
    Public Function GetHashCode1(  
        ByVal person As Person) As Integer _  
        Implements IEqualityComparer(Of Person).GetHashCode  
  
        If person Is Nothing Then Return 0  
        Dim hashFirstName =  
            If(person.FirstName Is Nothing,  
            0, person.FirstName.GetHashCode())  
        Dim hashLastName = person.LastName.GetHashCode()  
        Return hashFirstName Xor hashLastName  
    End Function  
End Class  
  
Sub Main()  
    Dim employees = New List(Of Employee) From {  
        New Employee With {.FirstName = "Michael", .LastName = "Alexander"},  
        New Employee With {.FirstName = "Jeff", .LastName = "Price"}  
    }  
  
    ' You can pass PersonComparer,   
    ' which implements IEqualityComparer(Of Person),  
    ' although the method expects IEqualityComparer(Of Employee)  
  
    Dim noduplicates As IEnumerable(Of Employee) = employees.Distinct(New PersonComparer())  
  
    For Each employee In noduplicates  
        Console.WriteLine(employee.FirstName & " " & employee.LastName)  
    Next  
End Sub  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Varianza nelle interfacce generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
