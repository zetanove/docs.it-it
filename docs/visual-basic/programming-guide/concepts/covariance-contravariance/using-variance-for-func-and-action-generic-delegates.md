---
title: Utilizzo della varianza per i delegati generici Func e Action (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 36c3012f-b39c-493b-b90f-079b5912ac1b
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
ms.openlocfilehash: 28c3f84d21f9fbc7e57ba079461194acf7612add
ms.lasthandoff: 03/13/2017

---
# <a name="using-variance-for-func-and-action-generic-delegates-visual-basic"></a>Utilizzo della varianza per i delegati generici azione (Visual Basic) e Func
In questi esempi viene illustrato come utilizzare la covarianza e controvarianza nel `Func` e `Action` delegati generici per consentire di riutilizzare i metodi e fornire una maggiore flessibilità nel codice.  
  
 Per ulteriori informazioni sulla covarianza e controvarianza, vedere [varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md).  
  
## <a name="using-delegates-with-covariant-type-parameters"></a>Utilizzo di delegati con parametri di tipo covariante  
 L'esempio seguente illustra i vantaggi del supporto di covarianza nell'interfaccia generica `Func` delegati. Il `FindByTitle` metodo accetta un parametro di `String` tipo e restituisce un oggetto del `Employee` tipo. Tuttavia, è possibile assegnare questo metodo per la `Func(Of String, Person)` delegato perché `Employee` eredita `Person`.  
  
```vb  
' Simple hierarchy of classes.  
Public Class Person  
End Class  
  
Public Class Employee  
    Inherits Person  
End Class  
  
Class Finder  
    Public Shared Function FindByTitle(  
        ByVal title As String) As Employee  
        ' This is a stub for a method that returns  
        ' an employee that has the specified title.  
        Return New Employee  
    End Function  
  
    Sub Test()  
        ' Create an instance of the delegate without using variance.  
        Dim findEmployee As Func(Of String, Employee) =  
            AddressOf FindByTitle  
  
        ' The delegate expects a method to return Person,  
        ' but you can assign it a method that returns Employee.  
        Dim findPerson As Func(Of String, Person) =  
            AddressOf FindByTitle  
  
        ' You can also assign a delegate   
        ' that returns a more derived type to a delegate   
        ' that returns a less derived type.  
        findPerson = findEmployee  
    End Sub  
End Class  
```  
  
## <a name="using-delegates-with-contravariant-type-parameters"></a>Utilizzo di delegati con parametri di tipo controvariante  
 L'esempio seguente illustra i vantaggi del supporto della controvarianza nell'interfaccia generica `Action` delegati. Il `AddToContacts` metodo accetta un parametro di `Person` tipo. Tuttavia, è possibile assegnare questo metodo per la `Action(Of Employee)` delegato perché `Employee` eredita `Person`.  
  
```vb  
Public Class Person  
End Class  
  
Public Class Employee  
    Inherits Person  
End Class  
  
Class AddressBook  
    Shared Sub AddToContacts(ByVal person As Person)  
        ' This method adds a Person object  
        ' to a contact list.  
    End Sub  
  
    Sub Test()  
        ' Create an instance of the delegate without using variance.  
        Dim addPersonToContacts As Action(Of Person) =  
            AddressOf AddToContacts  
  
        ' The Action delegate expects   
        ' a method that has an Employee parameter,  
        ' but you can assign it a method that has a Person parameter  
        ' because Employee derives from Person.  
        Dim addEmployeeToContacts As Action(Of Employee) =  
            AddressOf AddToContacts  
  
        ' You can also assign a delegate   
        ' that accepts a less derived parameter   
        ' to a delegate that accepts a more derived parameter.  
        addEmployeeToContacts = addPersonToContacts  
    End Sub  
End Class  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Covarianza e controvarianza (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/covariance-and-contravariance.md)   
 [Generics](https://msdn.microsoft.com/library/ms172192)
