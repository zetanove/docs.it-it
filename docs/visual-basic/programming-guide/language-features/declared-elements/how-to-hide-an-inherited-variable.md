---
title: "How to: Hide an Inherited Variable (Visual Basic) | Microsoft Docs"
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
  - "element names, qualification"
  - "references, declared elements"
  - "declaration statements, declared elements"
  - "referencing declared elements"
  - "declared elements, referencing"
  - "declared elements, about declared elements"
  - "variables [Visual Basic], hiding inherited"
ms.assetid: 765728d9-7351-4a30-999d-b5f34f024412
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Hide an Inherited Variable (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Una classe derivata eredita tutte le definizioni della relativa classe base.  Se si desidera definire una variabile utilizzando lo stesso nome di un elemento della classe base, è possibile nascondere tale elemento al momento della definizione della variabile nella classe derivata.  Se si esegue questa operazione, il codice della classe derivata accede alla variabile, a meno che il meccanismo di shadowing non venga esplicitamente ignorato.  
  
 Un altro motivo per nascondere una variabile ereditata per proteggerla da una revisione della classe base.  La classe base può infatti essere sottoposta a una modifica che altera l'elemento che viene ereditato.  In questo caso, il modificatore `Shadows` impone la risoluzione dei riferimenti dalla classe derivata nella variabile anziché nell'elemento della classe base.  
  
### Per nascondere una variabile ereditata  
  
1.  Assicurarsi che la variabile che si desidera nascondere sia dichiarata a livello di classe \(all'esterno di qualsiasi routine\).  In caso contrario, non è necessario nasconderla.  
  
2.  All'interno della classe derivata, scrivere un'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) che dichiari la variabile.  Utilizzare lo stesso nome della variabile ereditata.  
  
3.  includendo la parola chiave [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) nella dichiarazione.  
  
     Quando il codice nella classe derivata fa riferimento al nome della variabile, il compilatore risolve il riferimento nella variabile.  
  
     Nell'esempio riportato di seguito viene illustrato come nascondere una variabile ereditata.  
  
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
  
     Nell'esempio precedente la variabile `shadowString` viene dichiarata nella classe base e viene quindi nascosta nella classe derivata.  La routine `showStrings` della classe derivata visualizza la versione di shadowing della stringa quando il nome `shadowString` non è qualificato,  quindi visualizza la versione nascosta quando `shadowString` viene qualificato con la parola chiave `MyBase`.  
  
## Programmazione efficiente  
 Il meccanismo di shadowing introduce più versioni di una variabile con lo stesso nome.  Quando un'istruzione di codice fa riferimento al nome della variabile, la versione in cui il compilatore risolve il riferimento dipende da fattori quali la posizione dell'istruzione di codice e la presenza di una stringa di qualificazione.  Questa caratteristica può aumentare il rischio di fare riferimento a una versione non desiderata di una variabile nascosta.  È possibile ridurre tale rischio specificando in modo completo tutti i riferimenti a una variabile nascosta.  
  
## Vedere anche  
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Shadowing in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Differences Between Shadowing and Overriding](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)   
 [How to: Hide a Variable with the Same Name as Your Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)   
 [How to: Access a Variable Hidden by a Derived Class](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Me, My, MyBase, and MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [Inheritance Basics](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)