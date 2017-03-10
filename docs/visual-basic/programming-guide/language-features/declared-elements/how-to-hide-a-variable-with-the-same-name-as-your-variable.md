---
title: "How to: Hide a Variable with the Same Name as Your Variable (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "qualification, of element names"
  - "declarations, elements"
  - "element names, qualification"
  - "references, declared elements"
  - "declaration statements, declared elements"
  - "declaring elements"
  - "referencing declared elements"
  - "declared elements, referencing"
  - "declared elements, about declared elements"
ms.assetid: e39c0752-f19f-4d2e-a453-00df1b5fc7ee
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# How to: Hide a Variable with the Same Name as Your Variable (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per nascondere una variabile è possibile eseguirne lo *shadowing*, ossia ridefinirla con una variabile con lo stesso nome.  Sono disponibili due modi per eseguire lo shadowing di una variabile che si desidera nascondere:  
  
-   **Shadowing mediante l'ambito.** È possibile dichiarare nuovamente la variabile all'interno di una sottoarea dell'area contenente la variabile da nascondere.  
  
-   **Shadowing mediante ereditarietà.** Se la variabile da nascondere è definita a livello di classe, è possibile dichiararla nuovamente con la parola chiave [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) in una classe derivata per nasconderla tramite ereditarietà.  
  
## Due modi per nascondere una variabile  
  
#### Per nascondere una variabile eseguendone lo shadowing mediante l'ambito  
  
1.  Identificare l'area in cui è definita la variabile da nascondere, quindi determinare una sottoarea in cui ridefinirla con l'altra variabile.  
  
    |Area della variabile|Sottoarea consentita per la ridefinizione della variabile|  
    |--------------------------|---------------------------------------------------------------|  
    |Modulo|Classe all'interno del modulo|  
    |Classe|Sottoclasse all'interno della classe<br /><br /> Routine all'interno della classe|  
  
     Non è possibile ridefinire una variabile di routine in un blocco all'interno di tale routine, ad esempio in una costruzione `If`...`End If` o in un ciclo `For`.  
  
2.  Creare la sottoarea, se non esiste già.  
  
3.  All'interno della sottoarea scrivere un'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) che dichiari la variabile di shadowing.  
  
     Quando il codice all'interno della sottoarea fa riferimento al nome della variabile, il compilatore risolve il riferimento nella variabile di shadowing.  
  
     Nell'esempio riportato di seguito viene illustrato lo shadowing mediante l'ambito e viene creato un riferimento che ignora lo shadowing.  
  
    ```  
    Module shadowByScope  
        ' The following statement declares num as a module-level variable.  
        Public num As Integer  
        Sub show()  
            ' The following statement declares num as a local variable.  
            Dim num As Integer  
            ' The following statement sets the value of the local variable.  
            num = 2  
            ' The following statement displays the module-level variable.  
            MsgBox(CStr(shadowByScope.num))  
        End Sub  
        Sub useModuleLevelNum()  
            ' The following statement sets the value of the module-level variable.  
            num = 1  
            show()  
        End Sub  
    End Module  
    ```  
  
     Nell'esempio precedente viene dichiarata la variabile `num` a livello di modulo e a livello di routine \(nella routine `show`\).  La variabile locale `num` nasconde la variabile `num` a livello di modulo all'interno di `show`. La variabile locale viene quindi impostata su 2.  Tuttavia, non esiste alcuna variabile locale per nascondere `num` nella routine `useModuleLevelNum`.  Di conseguenza, la routine `useModuleLevelNum` imposta su 1 il valore della variabile a livello di modulo.  
  
     La chiamata a `MsgBox` all'interno di `show` ignora il meccanismo di shadowing specificando `num` con il nome del modulo.  Di conseguenza, verrà visualizzata la variabile a livello di modulo anziché la variabile locale.  
  
#### Per nascondere una variabile eseguendone lo shadowing mediante ereditarietà  
  
1.  Assicurarsi che la variabile da nascondere sia dichiarata in una classe e a livello di classe \(all'esterno di una qualsiasi routine\).  In caso contrario, non sarà possibile eseguire lo shadowing mediante ereditarietà.  
  
2.  Definire una classe derivata dalla classe della variabile, se non ne esiste già una.  
  
3.  All'interno della classe derivata scrivere un'istruzione `Dim` che dichiari la variabile,  includendo la parola chiave [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) nella dichiarazione.  
  
     Quando il codice nella classe derivata fa riferimento al nome della variabile, il compilatore risolve il riferimento nella variabile.  
  
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
  
     Nell'esempio precedente la variabile `shadowString` viene dichiarata nella classe base e viene quindi nascosta nella classe derivata.  La routine `showStrings` della classe derivata visualizza la versione di shadowing della stringa quando il nome `shadowString` non è qualificato,  Verrà quindi visualizzata la versione nascosta quando il nome `shadowString` viene qualificato con la parola chiave `MyBase`.  
  
## Programmazione efficiente  
 Il meccanismo di shadowing introduce più versioni di una variabile con lo stesso nome.  Quando un'istruzione di codice fa riferimento al nome della variabile, la versione in cui il compilatore risolve il riferimento dipende da fattori quali la posizione dell'istruzione di codice e la presenza di una stringa di qualificazione.  Questa caratteristica può aumentare il rischio di fare riferimento a una versione non desiderata di una variabile nascosta.  È possibile ridurre tale rischio specificando in modo completo tutti i riferimenti a una variabile nascosta.  
  
## Vedere anche  
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Shadowing in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Differences Between Shadowing and Overriding](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)   
 [How to: Hide an Inherited Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)   
 [How to: Access a Variable Hidden by a Derived Class](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Me, My, MyBase, and MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [Inheritance Basics](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)