---
title: "How to: Declare a Structure (Visual Basic) | Microsoft Docs"
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
  - "declarations, structures"
  - "structure statements"
  - "statements [Visual Basic], structure"
  - "structures, declaring"
ms.assetid: d5e98381-eb81-47d4-af83-48cc534a2572
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# How to: Declare a Structure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le dichiarazioni di struttura iniziano con l'istruzione [Structure Statement](../../../../visual-basic/language-reference/statements/structure-statement.md) e terminano con l'istruzione `End` `Structure`.  Fra queste due istruzioni è necessario dichiarare almeno un *elemento*.  Gli elementi possono essere di qualsiasi tipo di dati, ma almeno uno di essi deve essere una variabile non condivisa oppure un evento non personalizzato e non condiviso.  
  
 Non è possibile inizializzare alcun elemento della struttura nella dichiarazione della struttura.  Quando si dichiara una variabile come tipo di struttura, vengono assegnati valori agli elementi accedendovi mediante la variabile.  
  
 Per una descrizione delle differenze fra le strutture e le classi, vedere [Structures and Classes](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md).  
  
 A scopo dimostrativo, si supponga di voler tenere traccia del nome, dell'interno telefonico e dello stipendio di un dipendente.  Una struttura consente di eseguire questa operazione in una singola variabile.  
  
### Per dichiarare una struttura  
  
1.  Creare le istruzioni iniziale e finale della struttura.  
  
     È possibile specificare il livello di accesso utilizzando la parola chiave [Public](../../../../visual-basic/language-reference/modifiers/public.md), [Protected](../../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) o [Private](../../../../visual-basic/language-reference/modifiers/private.md) o impostarlo in maniera predefinita su `Public`.  
  
    ```  
    Private Structure employee  
    End Structure  
    ```  
  
2.  Aggiungere elementi al corpo della struttura.  
  
     Una struttura deve contenere almeno un elemento.  È necessario dichiarare ciascun elemento e specificare per esso un livello di accesso.  Se si utilizza l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) senza alcuna parola chiave, l'accessibilità viene automaticamente impostata sul valore predefinito `Public`.  
  
    ```  
    Private Structure employee  
        Public givenName As String  
        Public familyName As String  
        Public phoneExtension As Long  
        Private salary As Decimal  
        Public Sub giveRaise(raise As Double)  
            salary *= raise  
        End Sub  
        Public Event salaryReviewTime()  
    End Structure  
    ```  
  
     Il campo `salary` dell'esempio precedente è `Private`, ovvero non è accessibile dall'esterno della struttura nemmeno dalla classe contenitore.  La routine `giveRaise` è invece `Public`, pertanto può essere chiamata dall'esterno della struttura.  Analogamente, è possibile generare l'evento `salaryReviewTime` esternamente alla struttura.  
  
     Oltre alle variabili, alle routine `Sub` e agli eventi, in una struttura è possibile definire anche costanti, routine `Function` e proprietà.  È possibile designare almeno una proprietà come *predefinita*, purché accetti almeno un argomento.  È possibile gestire un evento con una routine [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) `Sub`.  Per ulteriori informazioni, vedere [How to: Declare and Call a Default Property in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md).  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Composite Data Types](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Structure Variables](../../../../visual-basic/programming-guide/language-features/data-types/structure-variables.md)   
 [Structures and Other Programming Elements](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)   
 [Structures and Classes](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)   
 [User\-Defined Data Type](../../../../visual-basic/language-reference/data-types/user-defined-data-type.md)