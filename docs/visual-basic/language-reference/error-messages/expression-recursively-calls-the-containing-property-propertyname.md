---
title: "Espressione in modo ricorsivo chiama la proprietà che contiene &quot;&lt;propertyname&gt;&quot; | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42026
- BC42026
dev_langs:
- VB
helpviewer_keywords:
- BC42026
ms.assetid: 4fde9db6-3bf3-48dc-8e05-981bf08969da
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
ms.openlocfilehash: ca20bf1a539f2727a80f8e781c1e9ebc5a4a253d
ms.lasthandoff: 03/13/2017

---
# <a name="expression-recursively-calls-the-containing-property-39ltpropertynamegt39"></a>Espressione in modo ricorsivo chiama la proprietà che contiene '&lt;propertyname&gt;'
Un'istruzione all'interno di `Set` routine di una definizione di proprietà archivia un valore nel nome della proprietà.  
  
 L'approccio consigliato per contenere il valore di una proprietà consiste nel definire un `Private` variabile nel contenitore della proprietà e utilizzarlo in entrambe le `Get` e `Set` procedure. Il `Set` routine deve archiviare, quindi il valore in ingresso in questa `Private` variabile.  
  
 Il `Get` routine si comporta come un `Function` procedura per assegnare un valore per il nome della proprietà e restituire il controllo in corrispondenza di `End Get` istruzione. Si consiglia, tuttavia, consiste nell'includere il `Private` variabile come valore in un [istruzione Return](../../../visual-basic/language-reference/statements/return-statement.md).  
  
 Il `Set` routine si comporta come un `Sub` routine, che non restituisce un valore. Pertanto, il nome della routine o proprietà hanno alcun significato speciale all'interno di un `Set` ed è possibile archiviare un valore al suo interno.  
  
 Nell'esempio seguente viene illustrato l'approccio che può causare questo errore, aggiungendo l'approccio consigliato.  
  
```  
Public Class illustrateProperties  
' The code in the following property causes this error.  
    Public Property badProp() As Char  
        Get  
            Dim charValue As Char  
            ' Insert code to update charValue.  
            badProp = charValue  
        End Get  
        Set(ByVal Value As Char)  
            ' The following statement causes this error.  
            badProp = Value  
            ' The value stored in the local variable badProp  
            ' is not used by the Get procedure in this property.  
        End Set  
    End Property  
' The following code uses the recommended approach.  
    Private propValue As Char  
    Public Property goodProp() As Char  
        Get  
            ' Insert code to update propValue.  
            Return propValue  
        End Get  
        Set(ByVal Value As Char)  
            propValue = Value  
        End Set  
    End Property  
End Class  
```  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42026  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Riscrivere la definizione di proprietà per utilizzare l'approccio consigliato come illustrato nell'esempio precedente.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà (routine)](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Property (istruzione)](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Istruzione Set](../../../visual-basic/language-reference/statements/set-statement.md)
