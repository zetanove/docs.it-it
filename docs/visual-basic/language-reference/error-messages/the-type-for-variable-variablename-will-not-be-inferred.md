---
title: "Inferenza del tipo per la variabile &#39;&lt;variablename&gt;&#39; non riuscita perch&#233; &#232; associato a un campo nell&#39;ambito che lo contiene | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc42110"
  - "bc42110"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42110"
ms.assetid: ef4442eb-08d1-434f-a03b-4aa2ed4e4414
caps.latest.revision: 33
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 33
---
# Inferenza del tipo per la variabile &#39;&lt;variablename&gt;&#39; non riuscita perch&#233; &#232; associato a un campo nell&#39;ambito che lo contiene
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il tipo della variabile '\<nomevariabile\>' non verrà dedotto perché associato a un ambito di inclusione.Cambiare il nome di '\<nomevariabile\>' o utilizzare il nome completo, ad esempio 'Me.nomevariabile' o 'MyBase.nomevariabile'.  
  
 Una variabile di controllo del ciclo nel codice ha lo stesso nome di un campo della classe e di altro ambito che lo contiene.  Poiché la variabile di controllo è utilizzata senza una clausola `As`, è associata al campo nell'ambito che la contiene e il compilatore non è in grado di creare per essa una nuova variabile né di dedurne il tipo.  
  
 Nell'esempio riportato di seguito, `Index`, la variabile di controllo nell'istruzione `For`, è associata al campo `Index` nella classe `Customer`.  Il compilatore non crea una nuova variabile per la variabile di controllo `Index` né ne deduce il tipo.  
  
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
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42110  
  
### Se viene visualizzato questo avvertimento  
  
-   Rendere locale la variabile di controllo del ciclo impostandone il nome su un identificatore che non sia anche il nome di un campo della classe.  
  
    ```  
    For I = 1 To 10  
    ```  
  
-   Chiarire che la variabile di controllo del ciclo è associata al campo della classe inserendo il prefisso `Me.` davanti al nome della variabile.  
  
    ```  
    For Me.Index = 1 To 10  
    ```  
  
-   Anziché affidarsi all'inferenza dei tipi locali, utilizzare la clausola `As` per specificare un tipo per la variabile di controllo del ciclo.  
  
    ```  
    For Index As Integer = 1 To 10  
    ```  
  
## Esempio  
 Nel codice riportato di seguito viene illustrato l'esempio precedente a cui è stata applicata la prima correzione.  
  
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
  
## Vedere anche  
 [Option Infer Statement](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [How to: Refer to the Current Instance of an Object](../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Me, My, MyBase, and MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)