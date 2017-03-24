---
title: "Shadows (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Shadows"
  - "shadows"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "shadowing"
  - "duplicate names"
  - "scope, shadowing"
  - "Shadows keyword"
  - "names, shadowing"
ms.assetid: 6bf687cd-0544-4797-b51b-911125ec57c6
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Shadows (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che un elemento di programmazione dichiarato ridichiara e nasconde un elemento omonimo o un insieme di elementi di overload di una classe base.  
  
## Note  
 Lo scopo principale dello shadowing, un meccanismo che consente di *nascondere in base al nome*, è quello di conservare la definizione dei membri della classe.  È possibile che la classe base sia sottoposta a una modifica che crea un elemento con lo stesso nome di quello già definito.  In tal caso, il modificatore `Shadows` impone che i riferimenti attraverso la classe vengano risolti nel membro definito, anziché nel nuovo elemento della classe base.  
  
 Sebbene lo shadowing e l'override ridefiniscano entrambi un elemento ereditato, esistono sostanziali differenze tra i due metodi.  Per ulteriori informazioni, vedere [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md).  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile utilizzare `Shadows` solo a livello di classe.  In altri termini, il contesto della dichiarazione per un elemento `Shadows` deve essere una classe e non un file di origine, uno spazio dei nomi, un'interfaccia, un modulo, una struttura o una routine.  
  
     In una singola istruzione di dichiarazione è possibile dichiarare un unico elemento di shadowing.  
  
-   **Modificatori combinati.** Non è possibile specificare `Shadows` insieme a `Overloads`, `Overrides` o `Static` nella stessa dichiarazione.  
  
-   **Tipi degli elementi.** È possibile nascondere qualsiasi tipo di elemento dichiarato con qualsiasi altro tipo.  Se si nasconde una proprietà o una routine con un'altra proprietà o routine, non è necessario che i parametri e il tipo restituito corrispondano a quelli della proprietà o della routine della classe base.  
  
-   **Accesso.** In genere, l'elemento nascosto nella classe base non è disponibile dall'interno della classe derivata che lo nasconde.  Si applicano tuttavia le considerazioni riportate di seguito.  
  
    -   Se l'elemento di shadowing non è accessibile dal codice che fa riferimento ad esso, il riferimento viene risolto nell'elemento nascosto.  Se, ad esempio, un elemento `Private` nasconde un elemento della classe base, il codice che non dispone dell'autorizzazione per accedere all'elemento `Private` accede invece all'elemento della classe base.  
  
    -   Se si nasconde un elemento, è possibile comunque accedervi attraverso un oggetto dichiarato con il tipo della classe base.  È inoltre possibile accedere a tale elemento mediante `MyBase`.  
  
 Il modificatore `Shadows` può essere utilizzato nei seguenti contesti:  
  
 [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Istruzione Const](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Istruzione Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Istruzione Dim](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Istruzione Enum](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Static](../../../visual-basic/language-reference/modifiers/static.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Me, My, MyBase, and MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)   
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)   
 [Overloads](../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)   
 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)