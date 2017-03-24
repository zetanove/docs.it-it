---
title: 'Procedura: richiamare un metodo delegato (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
ms.assetid: b56866ae-abf9-4a5a-a855-486359455e9c
caps.latest.revision: 10
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 29b20eb6089886c8111711388472004bbacea312
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-invoke-a-delegate-method-visual-basic"></a>Procedura: richiamare un metodo delegato (Visual Basic)
In questo esempio viene illustrato come associare un delegato di un metodo e quindi richiamare il metodo tramite il delegato.  
  
### <a name="create-the-delegate-and-matching-procedures"></a>Creare il delegato e le procedure corrispondenti  
  
1.  Crea un delegato denominato `MySubDelegate`.  
  
    ```  
    Delegate Sub MySubDelegate(ByVal x As Integer)  
    ```  
  
2.  Dichiarare una classe che contiene un metodo con la stessa firma del delegato.  
  
    ```  
    Class class1  
        Sub Sub1(ByVal x As Integer)  
            MsgBox("The value of x is: " & CStr(x))  
        End Sub  
    End Class  
    ```  
  
3.  Definire un metodo che crea un'istanza del delegato e richiama il metodo associato al delegato chiamando incorporata `Invoke` metodo.  
  
    ```  
    Protected Sub DelegateTest()  
        Dim c1 As New class1  
        ' Create an instance of the delegate.  
        Dim msd As MySubDelegate = AddressOf c1.Sub1  
        ' Call the method.  
        msd.Invoke(10)  
    End Sub  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Delegate (istruzione)](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Delegati](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Eventi](../../../../visual-basic/programming-guide/language-features/events/index.md)   
 [Applicazioni multithread](http://msdn.microsoft.com/library/a06a1a56-dd16-44e8-bc01-2c2255511bc6)
