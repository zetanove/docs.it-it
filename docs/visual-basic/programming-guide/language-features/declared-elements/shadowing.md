---
title: "Shadowing in Visual Basic | Microsoft Docs"
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
  - "inheritance, shadowing"
  - "overriding, and shadowing"
  - "shadowing"
  - "duplicate names"
  - "shadowing, by inheritance"
  - "declared elements, referencing"
  - "shadowing, by scope"
  - "declared elements, hiding"
  - "naming conflicts, shadowing"
  - "declared elements, shadowing"
  - "shadowing, and overriding"
  - "scope, shadowing"
  - "Shadows keyword, about"
  - "objects [Visual Basic], names"
  - "names, shadowing"
ms.assetid: 54bb4c25-12c4-4181-b4a0-93546053964e
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# Shadowing in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando a due elementi di programmazione è assegnato lo stesso nome, è possibile che uno dei due nasconda l'altro, o che ne esegua lo *shadowing*.  In una situazione di questo tipo, non è possibile fare riferimento all'elemento nascosto. Quando nel codice viene utilizzato il nome dell'elemento, il compilatore [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] risolve tale nome nell'elemento di shadowing.  
  
## Scopo  
 Lo scopo principale dello shadowing è di proteggere la definizione dei membri della classe.  È possibile che la classe base sia sottoposta a una modifica che crea un elemento con lo stesso nome di quello già definito.  In tal caso, il modificatore `Shadows` impone che i riferimenti attraverso la classe vengano risolti nel membro definito, anziché nel nuovo elemento della classe base.  
  
## Tipi di shadowing  
 Un elemento può nascondere un altro elemento in due modi diversi.  È possibile che l'elemento di shadowing sia dichiarato all'interno di una sottoarea dell'area contenente l'elemento nascosto. In questo caso, lo shadowing viene ottenuto *mediante l'ambito*.  Se invece un membro di una classe base viene ridefinito da una classe di derivazione, lo shadowing viene ottenuto *mediante ereditarietà*.  
  
### Shadowing mediante l'ambito  
 È possibile che gli elementi di programmazione nello stesso modulo, classe o struttura abbiano lo stesso nome ma ambiti diversi.  Quando due elementi vengono dichiarati in questo modo e il codice fa riferimento al nome che hanno in comune, l'elemento con ambito ristretto \(ovvero l'ambito blocco\) nasconde l'altro elemento.  
  
 È ad esempio possibile che un blocco definisca una variabile `Public` denominata `temp`, mentre una routine all'interno del modulo dichiara una variabile locale denominata anch'essa `temp`.  I riferimenti a `temp` dall'interno della routine accedono alla variabile locale, mentre i riferimenti a `temp` dall'esterno della routine accedono alla variabile `Public`.  In questo caso, la variabile `temp` della routine nasconde la variabile `temp` del modulo.  
  
 Nella figura riportata più avanti sono presenti due variabili, entrambe denominate `temp`.  La variabile locale `temp` nasconde la variabile membro `temp` quando l'accesso viene eseguito dall'interno della relativa routine `p`.  La parola chiave `MyClass`, tuttavia, consente di ignorare lo shadowing e di accedere alla variabile membro.  
  
 ![Diagramma grafico dello shadowing tramite l'ambito](../../../../visual-basic/programming-guide/language-features/declared-elements/media/shadowscope.gif "ShadowScope")  
Shadowing mediante l'ambito  
  
 Per un esempio di shadowing mediante l'ambito, vedere [How to: Hide a Variable with the Same Name as Your Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md).  
  
### Shadowing mediante ereditarietà  
 Se una classe derivata ridefinisce un elemento di programmazione ereditato da una classe base, l'elemento ridefinito nasconderà l'elemento originale.  È possibile nascondere qualsiasi tipo di elemento dichiarato o insieme di elementi in overload con qualsiasi altro tipo.  Una variabile `Integer` è ad esempio in grado di nascondere una routine `Function`.  Se si nasconde una routine con un'altra routine, è possibile utilizzare un elenco di parametri differente e un tipo restituito differente.  
  
 Nella figura riportata più avanti sono presenti una classe base `b` e una classe derivata `d` che eredita da `b`.  La classe base definisce una routine denominata `proc`, mentre la classe derivata la nasconde con un'altra routine con lo stesso nome.  La prima istruzione `Call` accede alla routine `proc` di shadowing nella classe derivata.  La parola chiave `MyBase`, tuttavia, consente di ignorare lo shadowing e di accedere alla routine nascosta nella classe base.  
  
 ![Diagramma grafico dello shadowing tramite eredità](../../../../visual-basic/programming-guide/language-features/declared-elements/media/shadowinherit.gif "ShadowInherit")  
Shadowing mediante ereditarietà  
  
 Per un esempio di shadowing mediante ereditarietà, vedere [How to: Hide a Variable with the Same Name as Your Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md) e [How to: Hide an Inherited Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md).  
  
#### Shadowing e livello di accesso  
 L'elemento di shadowing non è sempre accessibile dal codice mediante la classe derivata.  È possibile, ad esempio, che l'elemento venga dichiarato `Private`.  In tal caso, lo shadowing viene annullato e il compilatore risolve qualsiasi riferimento allo stesso elemento come se non fosse stato definito alcuno shadowing.  Questo elemento è l'elemento accessibile posizionato il minor numero possibile di passaggi derivazionali all'indietro rispetto alla classe di shadowing.  Se l'elemento nascosto è una routine, il riferimento viene risolto nella versione accessibile più vicina con lo stesso nome, elenco di parametri e tipo restituito.  
  
 Nell'esempio riportato di seguito viene illustrata una gerarchia di ereditarietà costituita da tre classi.  Ciascuna classe definisce una routine `Sub` `display` mentre ciascuna classe derivata nasconde la routine `display` nella propria classe base.  
  
```  
Public Class firstClass  
    Public Sub display()  
        MsgBox("This is firstClass")  
    End Sub  
End Class  
Public Class secondClass  
    Inherits firstClass  
    Private Shadows Sub display()  
        MsgBox("This is secondClass")  
    End Sub  
End Class  
Public Class thirdClass  
    Inherits secondClass  
    Public Shadows Sub display()  
        MsgBox("This is thirdClass")  
    End Sub  
End Class  
Module callDisplay  
    Dim first As New firstClass  
    Dim second As New secondClass  
    Dim third As New thirdClass  
    Public Sub callDisplayProcedures()  
        ' The following statement displays "This is firstClass".  
        first.display()  
        ' The following statement displays "This is firstClass".  
        second.display()  
        ' The following statement displays "This is thirdClass".  
        third.display()  
    End Sub  
End Module  
```  
  
 Nell'esempio precedente la classe derivata `secondClass` nasconde la routine `display` con una routine `Private`.  Quando il modulo `callDisplay` chiama `display` in `secondClass`, il codice chiamante si trova all'esterno di `secondClass` e non può quindi accedere alla routine `display` privata.  Lo shadowing viene annullato e il compilatore risolve il riferimento nella routine `display` della classe base.  
  
 Tuttavia, l'altra classe derivata `thirdClass` dichiara `display` come `Public`, consentendo al codice in `callDisplay` di accedere alla routine.  
  
## Shadowing e override  
 Non confondere lo shadowing con l'override.  Entrambi vengono utilizzati quando una classe derivata eredita da una classe base ed entrambi consentono di ridefinire un elemento dichiarato con un altro.  Esistono tuttavia differenze significative tra queste due tecniche.  Per un confronto, vedere [Differences Between Shadowing and Overriding](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md).  
  
## Shadowing e overload  
 Se si nasconde lo stesso elemento della classe base con più di un elemento nella classe derivata, gli elementi di shadowing diventeranno versioni di overload di tale elemento.  Per ulteriori informazioni, vedere [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md).  
  
## Accesso a un elemento nascosto  
 Quando si accede a un elemento da una classe derivata, normalmente lo si fa tramite l'istanza corrente di tale classe, qualificando il nome dell'elemento con la parola chiave `Me`.  Se la classe derivata nasconde l'elemento nella classe base, è possibile accedere all'elemento della classe base qualificandolo con la parola chiave `MyBase`.  
  
 Per un esempio di accesso a un elemento nascosto, vedere [How to: Access a Variable Hidden by a Derived Class](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md).  
  
### Dichiarazione di una variabile oggetto  
 La modalità di creazione della variabile oggetto può anche determinare se la classe derivata accederà a un elemento di shadowing o all'elemento nascosto.  Nell'esempio riportato di seguito vengono creati due oggetti da una classe derivata, ma un oggetto viene dichiarato come classe base e l'altro come classe derivata.  
  
```  
Public Class baseCls  
    ' The following statement declares the element that is to be shadowed.  
    Public z As Integer = 100  
End Class  
Public Class dervCls  
    Inherits baseCls  
    ' The following statement declares the shadowing element.  
    Public Shadows z As String = "*"  
End Class  
Public Class useClasses  
    ' The following statement creates the object declared as the base class.  
    Dim basObj As baseCls = New dervCls()  
    ' Note that dervCls widens to its base class baseCls.  
    ' The following statement creates the object declared as the derived class.  
    Dim derObj As dervCls = New dervCls()  
    Public Sub showZ()   
    ' The following statement outputs 100 (the shadowed element).  
        MsgBox("Accessed through base class: " & basObj.z)  
    ' The following statement outputs "*" (the shadowing element).  
        MsgBox("Accessed through derived class: " & derObj.z)  
    End Sub  
End Class  
```  
  
 Nell'esempio precedente la variabile `basObj` viene dichiarata come classe base.  L'assegnazione dell'oggetto `dervCls` a tale classe costituisce una conversione di ampliamento e risulta quindi valida.  La classe base tuttavia non è in grado di accedere alla versione di shadowing della variabile `z` nella classe derivata, quindi il compilatore risolve `basObj.z` nel valore di classe base originale.  
  
## Vedere anche  
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Me, My, MyBase, and MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [Inheritance Basics](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)