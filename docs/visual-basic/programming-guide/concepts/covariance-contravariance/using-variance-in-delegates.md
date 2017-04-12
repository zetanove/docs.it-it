---
title: Utilizzo della varianza nei delegati (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 7b5c20f1-6416-46a3-94b6-f109c31c842c
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
ms.openlocfilehash: 5bd3e60031eac713cee3dee1399af8c6b83e6656
ms.lasthandoff: 03/13/2017

---
# <a name="using-variance-in-delegates-visual-basic"></a>Utilizzo della varianza nei delegati (Visual Basic)
Quando si assegna un metodo a un delegato, *covarianza* e *controvarianza* offrono flessibilità per la corrispondenza di un tipo delegato con una firma di metodo. La covarianza consente a un metodo per restituire tipo più derivato da quello definito nel delegato. La controvarianza consente a un metodo che dispone di tipi di parametro che sono meno derivati rispetto a quelli del tipo delegato.  
  
## <a name="example-1-covariance"></a>Esempio 1: covarianza  
  
### <a name="description"></a>Descrizione  
 In questo esempio viene illustrato come utilizzare i delegati con metodi che restituiscono tipi che derivano dal tipo restituito nella firma del delegato. Il tipo di dati restituito da `DogsHandler` è di tipo `Dogs`, che deriva dal `Mammals` tipo definito nel delegato.  
  
### <a name="code"></a>Codice  
  
```vb  
Class Mammals  
End Class  
  
Class Dogs  
    Inherits Mammals  
End Class  
Class Test  
    Public Delegate Function HandlerMethod() As Mammals  
    Public Shared Function MammalsHandler() As Mammals  
        Return Nothing  
    End Function  
    Public Shared Function DogsHandler() As Dogs  
        Return Nothing  
    End Function  
    Sub Test()  
        Dim handlerMammals As HandlerMethod = AddressOf MammalsHandler  
        ' Covariance enables this assignment.  
        Dim handlerDogs As HandlerMethod = AddressOf DogsHandler  
    End Sub  
End Class  
```  
  
## <a name="example-2-contravariance"></a>Esempio 2: controvarianza  
  
### <a name="description"></a>Descrizione  
 In questo esempio viene illustrato come utilizzare i delegati con metodi che dispongono di un tipo di parametri che sono tipi di base del tipo di parametro di firma di delegato. Con la controvarianza, è possibile utilizzare un gestore eventi anziché gestori separati. Ad esempio, è possibile creare un gestore eventi che accetta un `EventArgs` parametro di input e di utilizzarlo con un `Button.MouseClick` evento che invia un `MouseEventArgs` tipo come parametro e con un `TextBox.KeyDown` evento che invia un `KeyEventArgs` parametro.  
  
### <a name="code"></a>Codice  
  
```vb  
' Event hander that accepts a parameter of the EventArgs type.  
Private Sub MultiHandler(ByVal sender As Object,  
                         ByVal e As System.EventArgs)  
    Label1.Text = DateTime.Now  
End Sub  
  
Private Sub Form1_Load(ByVal sender As System.Object,  
    ByVal e As System.EventArgs) Handles MyBase.Load  
  
    ' You can use a method that has an EventArgs parameter,  
    ' although the event expects the KeyEventArgs parameter.  
    AddHandler Button1.KeyDown, AddressOf MultiHandler  
  
    ' You can use the same method   
    ' for the event that expects the MouseEventArgs parameter.  
    AddHandler Button1.MouseClick, AddressOf MultiHandler  
End Sub  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)   
 [Utilizzo della varianza per i delegati generici azione (Visual Basic) e Func](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
