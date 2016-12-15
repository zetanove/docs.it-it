---
title: "How to: Access a Variable Hidden by a Derived Class (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "qualification, of element names"
  - "base classes, accessing elements"
  - "element names, qualification"
  - "references, declared elements"
  - "declared elements, referencing"
  - "variables [Visual Basic], accessing hidden"
ms.assetid: ae21a8ac-9cd4-4fba-a3ec-ecc4321ef93c
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Access a Variable Hidden by a Derived Class (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Quando il codice di una classe derivata accede a una variabile, il compilatore risolve in genere il riferimento alla versione accessibile più vicina, ovvero alla versione a cui è possibile accedere con il minor numero di passaggi di derivazione all'indietro a partire dalla classe.  Se la variabile è definita nella classe derivata, normalmente il codice accede a tale definizione.  
  
 La variabile della classe derivata può nascondere una variabile della classe base.  È tuttavia possibile accedere alla variabile della classe base qualificandola con la parola chiave `MyBase`.  
  
### Per accedere a una variabile della classe base nascosta da una classe derivata  
  
-   In un'espressione o in un'istruzione di assegnazione inserire prima del nome della variabile la parola chiave `MyBase` e un punto \(`.`\).  
  
     Il compilatore risolve il riferimento alla versione della classe base della variabile.  
  
     Nell'esempio riportato di seguito viene illustrato lo shadowing mediante ereditarietà.  Vengono creati due riferimenti, uno che accede alla variabile di shadowing e l'altro che ignora lo shadowing.  
  
    ```  
    Public Class shadowBaseClass  
        Public shadowString As String = "This is the base class string."  
    End Class  
    Public Class shadowDerivedClass  
        Inherits shadowBaseClass  
        Public Shadows shadowString As String = "This is the derived class string."  
        Public Sub showStrings()  
            Dim s As String = "Unqualified shadowString: " & shadowString &  
                vbCrLf & "MyBase.shadowString: " & MyBase.shadowString  
            MsgBox(s)  
        End Sub  
    End Class  
    ```  
  
     Nell'esempio precedente la variabile `shadowString` viene dichiarata nella classe base e viene quindi nascosta nella classe derivata.  La routine `showStrings` della classe derivata visualizza la versione di shadowing della stringa quando il nome `shadowString` non è qualificato,  quindi visualizza la versione nascosta quando `shadowString` viene qualificato con la parola chiave `MyBase` .  
  
## Programmazione efficiente  
 Per ridurre il rischio di fare riferimento a una versione non desiderata di una variabile nascosta, è possibile specificare in modo completo tutti i riferimenti alla variabile nascosta.  Il meccanismo di shadowing introduce più versioni di una variabile con lo stesso nome.  Quando un'istruzione di codice fa riferimento al nome della variabile, la versione in cui il compilatore risolve il riferimento dipende da fattori quali la posizione dell'istruzione di codice e la presenza di una stringa di qualificazione.  Questa caratteristica può aumentare il rischio di fare riferimento alla versione errata della variabile.  
  
## Vedere anche  
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Shadowing in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Differences Between Shadowing and Overriding](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)   
 [How to: Hide a Variable with the Same Name as Your Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)   
 [How to: Hide an Inherited Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Me, My, MyBase, and MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [Inheritance Basics](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)