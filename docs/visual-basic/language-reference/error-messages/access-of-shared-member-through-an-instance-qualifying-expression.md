---
title: "Accesso di membro condiviso tramite un&quot;istanza. l&quot;espressione di qualificazione non verrà valutato | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42025
- BC42025
dev_langs:
- VB
helpviewer_keywords:
- BC42025
ms.assetid: db3337e5-c349-42bf-86df-d9c1e00952a5
caps.latest.revision: 23
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 39be3c95d5acc20afe3a33be9d4db48c09f99a9c
ms.lasthandoff: 03/13/2017

---
# <a name="access-of-shared-member-through-an-instance-qualifying-expression-will-not-be-evaluated"></a>Accesso di membro condiviso tramite un'istanza; l'espressione di qualificazione non verrà valutata
Una variabile di istanza di una classe o struttura viene utilizzata per accedere a un `Shared` variabile, proprietà, procedura o evento definito nella classe o struttura. Il problema può verificarsi anche se una variabile di istanza viene utilizzata per accedere a un membro di una classe o struttura, ad esempio una costante o enumerazione o una classe annidata o una struttura condiviso in modo implicito.  
  
 Lo scopo di un membro di condivisione consiste nel creare una sola copia di tale membro e renderla disponibile per ogni istanza della classe o struttura in cui è dichiarata. È coerenza con lo scopo per accedere a un `Shared` membro tramite il nome della relativa classe o struttura, anziché tramite una variabile che contiene una singola istanza di tale classe o struttura.  
  
 L'accesso a un `Shared` membro tramite una variabile di istanza può rendere più difficile comprendere nascondendo il fatto che il membro è il codice `Shared`. Inoltre, se tale accesso fa parte di un'espressione che esegue altre azioni, ad esempio un `Function` procedure che restituisce un'istanza del membro condiviso, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] ignora l'espressione e tutte le altre azioni che altrimenti verrebbero eseguite.  
  
 Per ulteriori informazioni e un esempio, vedere [Shared](../../../visual-basic/language-reference/modifiers/shared.md).  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42025  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Utilizzare il nome della classe o struttura che definisce il `Shared` membro per accedervi, come illustrato nell'esempio seguente.  
  
```vb  
Public Class testClass  
    Public Shared Sub sayHello()  
        MsgBox("Hello")  
    End Sub  
End Class  
  
Module testModule  
    Public Sub Main()  
        ' Access a shared method through an instance variable.  
        ' This generates a warning.  
        Dim tc As New testClass  
        tc.sayHello()  
  
        ' Access a shared method by using the class name.  
        ' This does not generate a warning.  
        testClass.sayHello()  
    End Sub  
End Module  
```  
  
> [!NOTE]
>  Prestare particolare attenzione agli effetti dell'ambito quando due elementi di programmazione presentano lo stesso nome. Nell'esempio precedente, se si dichiara un'istanza utilizzando `Dim testClass as testClass = Nothing`, il compilatore considera una chiamata a `testClass.sayHello()` non appena si verifica un accesso al metodo tramite il nome della classe e nessun avviso.  
  
## <a name="see-also"></a>Vedere anche  
 [Condiviso](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Ambito in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
