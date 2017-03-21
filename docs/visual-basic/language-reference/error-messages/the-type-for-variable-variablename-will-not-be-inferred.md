---
title: "Tipo per la variabile &quot;&lt;NomeVariabile&gt;&quot; non verrà dedotto perché associato a un campo in un ambito contenitore | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42110
- bc42110
dev_langs:
- VB
helpviewer_keywords:
- BC42110
ms.assetid: ef4442eb-08d1-434f-a03b-4aa2ed4e4414
caps.latest.revision: 33
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ab7d69c34a58dc898553868258c4fdf6b81db343
ms.lasthandoff: 03/13/2017

---
# <a name="the-type-for-variable-39ltvariablenamegt39-will-not-be-inferred-because-it-is-bound-to-a-field-in-an-enclosing-scope"></a>Tipo per la variabile '&lt;NomeVariabile&gt;' non verrà dedotto perché associato a un campo in un ambito contenitore
Tipo per la variabile '\<nomevariabile >' non verrà dedotto perché associato a un campo in un ambito contenitore. Modificare il nome di '\<nomevariabile >', oppure utilizzare il nome completo (ad esempio, 'Variablename' o 'MyBase').  
  
 Una variabile di controllo del ciclo nel codice ha lo stesso nome di un campo della classe o di altro ambito che lo contiene. Poiché la variabile di controllo viene utilizzata senza un `As` clausola, è associato al campo nell'ambito e il compilatore non creare una nuova variabile per o dedurre il tipo.  
  
 Nell'esempio seguente, `Index`, la variabile di controllo nel `For` istruzione, è associato al `Index` campo la `Customer` classe. Il compilatore non crea una nuova variabile per la variabile di controllo `Index` o dedurre il tipo.  
  
```  
Class Customer  
  
    ' The class has a field named Index.  
    Private Index As Integer  
  
    Sub Main()  
  
    ' The following line will raise this warning.  
        For Index = 1 To 10  
            ' ...  
        Next  
  
    End Sub  
End Class  
  
```  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42110  
  
### <a name="to-address-this-warning"></a>Per risolvere questo avviso  
  
-   Rendere la variabile di controllo locale modificando il nome a un identificatore che non è anche il nome di un campo della classe.  
  
    ```  
    For I = 1 To 10  
    ```  
  
-   Chiarire che la variabile di controllo associata al campo della classe anteponendo `Me.` al nome della variabile.  
  
    ```  
    For Me.Index = 1 To 10  
    ```  
  
-   Anziché affidarsi all'inferenza del tipo locale, utilizzare un `As` clausola per specificare un tipo per la variabile di controllo.  
  
    ```  
    For Index As Integer = 1 To 10  
    ```  
  
## <a name="example"></a>Esempio  
 Il codice seguente viene illustrato l'esempio precedente la correzione prima sul posto.  
  
```  
Class Customer  
  
    ' The class has a field named Index.  
    Private Index As Integer  
  
    Sub Main()  
  
        For I = 1 To 10  
            ' ...  
        Next  
  
    End Sub  
End Class  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Option Infer](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Per ogni corso... Next (istruzione)](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [For... Next (istruzione)](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Procedura: fare riferimento all'istanza corrente di un oggetto](../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [Inferenza del tipo locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Me, My, MyBase e MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
