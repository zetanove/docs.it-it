---
title: "Utilizzo la variabile di iterazione in un&quot;espressione lambda può produrre risultati imprevisti | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42324
- bc42324
dev_langs:
- VB
helpviewer_keywords:
- BC42324
ms.assetid: b5c2c4bd-3b2a-4a73-aaeb-55728eb03b68
caps.latest.revision: 8
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
ms.openlocfilehash: 5b293ec344d816e40d369757fa4d11710b7ecd8d
ms.lasthandoff: 03/13/2017

---
# <a name="using-the-iteration-variable-in-a-lambda-expression-may-have-unexpected-results"></a>L'utilizzo della variabile di iterazione in un'espressione lambda può produrre risultati imprevisti
L'uso della variabile di iterazione in un'espressione lambda può produrre risultati imprevisti. In alternativa, creare una variabile locale all'interno del ciclo e viene assegnato il valore della variabile di iterazione.  
  
 Questo avviso viene visualizzato quando si utilizza una variabile di iterazione del ciclo in un'espressione lambda che viene dichiarata all'interno del ciclo. Ad esempio, l'esempio seguente genera questo avviso.  
  
```vb  
For i As Integer = 1 To 10  
    ' The warning is given for the use of i.  
    Dim exampleFunc As Func(Of Integer) = Function() i  
Next  
```  
  
 Nell'esempio seguente viene illustrato che potrebbero verificarsi risultati imprevisti.  
  
```vb  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            array1(i) = Function() i  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
 Il `For` ciclo crea una matrice di espressioni lambda, ognuna delle quali restituisce il valore della variabile di iterazione del ciclo `i`. Quando vengono valutate le espressioni lambda nel `For Each` ciclo, si aspetterebbe di vedere 0, 1, 2, 3 e 4, i valori successivi di `i` nel `For` ciclo. Vedere invece il valore finale del `i` per cinque volte:  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42324  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Assegnare il valore della variabile di iterazione a una variabile locale e utilizzare la variabile locale nell'espressione lambda.  
  
```vb  
Module Module1  
    Sub Main()  
        Dim array1 As Func(Of Integer)() = New Func(Of Integer)(4) {}  
  
        For i As Integer = 0 To 4  
            Dim j = i  
            array1(i) = Function() j  
        Next  
  
        For Each funcElement In array1  
            System.Console.WriteLine(funcElement())  
        Next  
  
    End Sub  
End Module  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
