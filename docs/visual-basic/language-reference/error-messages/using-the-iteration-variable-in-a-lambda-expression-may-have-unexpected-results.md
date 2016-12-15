---
title: "Using the iteration variable in a lambda expression may have unexpected results | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc42324"
  - "bc42324"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42324"
ms.assetid: b5c2c4bd-3b2a-4a73-aaeb-55728eb03b68
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Using the iteration variable in a lambda expression may have unexpected results
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'utilizzo della variabile di iterazione in un'espressione lambda può produrre risultati imprevisti.Creare una variabile locale all'interno del ciclo e assegnarvi il valore della variabile di iterazione.  
  
 Questo avviso viene visualizzato quando si utilizza una variabile di iterazione del ciclo in un'espressione lambda dichiarata all'interno del ciclo.  Nell'esempio seguente, ad esempio, viene generato questo avviso.  
  
```vb#  
For i As Integer = 1 To 10  
    ' The warning is given for the use of i.  
    Dim exampleFunc As Func(Of Integer) = Function() i  
Next  
```  
  
 Nell'esempio seguente vengono illustrati i risultati imprevisti che potrebbero verificarsi.  
  
```vb#  
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
  
 Il ciclo `For` crea una matrice di espressioni lambda, ognuna delle quali restituisce il valore della variabile di iterazione del ciclo `i`.  Quando le espressioni lambda vengono valutate nel ciclo `For Each`, dovrebbero venire visualizzati 0, 1, 2, 3 e 4, i valori successivi di `i` nel ciclo `For`.  Viene invece visualizzato il valore finale di `i` per cinque volte:  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 `5`  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42324  
  
### Per correggere l'errore  
  
-   Assegnare il valore della variabile di iterazione a una variabile locale e utilizzare la variabile locale nell'espressione lambda.  
  
    ```vb#  
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
  
## Vedere anche  
 [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)