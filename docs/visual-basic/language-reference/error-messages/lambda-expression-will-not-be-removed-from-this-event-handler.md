---
title: "Lambda expression will not be removed from this event handler | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc42326"
  - "vbc42326"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42326"
ms.assetid: 63214dc6-0112-4245-8ebf-7c9e8f5a5782
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Lambda expression will not be removed from this event handler
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'espressione lambda non verrà rimossa da questo gestore eventi.Assegnare l'espressione lambda a una variabile e utilizzare la variabile per aggiungere e rimuovere l'evento.  
  
 Quando le espressioni lambda vengono utilizzate con i gestori eventi, è possibile non vedere il comportamento previsto.  Il compilatore genera un nuovo metodo per ogni definizione dell'espressione lambda, anche se sono identiche.  Pertanto, nel codice seguente verrà visualizzato `False`.  
  
```vb#  
Module Module1  
  
    Sub Main()  
        Dim fun1 As ChangeInteger = Function(p As Integer) p + 1  
        Dim fun2 As ChangeInteger = Function(p As Integer) p + 1  
        Console.WriteLine(fun1 = fun2)  
    End Sub  
  
    Delegate Function ChangeInteger(ByVal x As Integer) As Integer  
  
End Module  
```  
  
 Quando le espressioni lambda vengono utilizzate con i gestori eventi, è possibile che vengano restituiti risultati imprevisti.  Nell'esempio seguente l'espressione lambda aggiunta da `AddHandler` non viene rimossa dall'istruzione `RemoveHandler`.  
  
```vb#  
Module Module1  
  
    Event ProcessInteger(ByVal x As Integer)  
  
    Sub Main()  
  
        ' The following line adds one listener to the event.  
        AddHandler ProcessInteger, Function(m As Integer) m  
  
        ' The following statement searches the current listeners   
        ' for a match to remove. However, this lambda is not the same  
        ' as the previous one, so nothing is removed.  
        RemoveHandler ProcessInteger, Function(m As Integer) m  
  
    End Sub  
End Module  
```  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42326  
  
### Per correggere l'errore  
  
-   Per evitare la visualizzazione dell'avviso e rimuovere l'espressione lambda, assegnare l'espressione lambda a una variabile e utilizzare la variabile nelle istruzioni `AddHandler` e `RemoveHandler`, come mostrato nell'esempio seguente.  
  
    ```vb#  
    Module Module1  
  
        Event ProcessInteger(ByVal x As Integer)  
  
        Dim PrintHandler As ProcessIntegerEventHandler  
  
        Sub Main()  
  
            ' Assign the lambda expression to a variable.  
            PrintHandler = Function(m As Integer) m  
  
            ' Use the variable to add the listener.  
            AddHandler ProcessInteger, PrintHandler  
  
            ' Use the variable again when you want to remove the listener.  
            RemoveHandler ProcessInteger, PrintHandler  
  
        End Sub  
    End Module  
    ```  
  
## Vedere anche  
 [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Relaxed Delegate Conversion](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)