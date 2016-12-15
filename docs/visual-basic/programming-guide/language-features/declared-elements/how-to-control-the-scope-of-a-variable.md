---
title: "How to: Control the Scope of a Variable (Visual Basic) | Microsoft Docs"
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
  - "variables [Visual Basic], scope"
  - "declared elements, scope"
  - "visibility, declared elements"
  - "variables [Visual Basic], visibility"
  - "scope, declared elements"
  - "scope, variables"
  - "scope, Visual Basic"
  - "declared elements, visibility"
  - "visibility, variables"
ms.assetid: 44b7f62a-cb5c-4d50-bce9-60ae68f87072
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Control the Scope of a Variable (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'*ambito* di una variabile, ovvero l'area in cui la variabile è visibile per riferimento, corrisponde in genere all'area in cui la variabile è dichiarata.  In alcuni casi, l'ambito della variabile può essere modificato dal relativo *livello di accesso*.  
  
 Per ulteriori informazioni, vedere [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md).  
  
## Ambito a livello di blocco o di routine  
  
#### Per rendere una variabile visibile solo all'interno di un blocco  
  
-   Inserire l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) relativa alla variabile tra l'istruzione di dichiarazione iniziale e quella finale del blocco, ad esempio tra le istruzioni `For` e `Next` di un ciclo `For`.  
  
     È possibile fare riferimento alla variabile solo dall'interno del blocco.  
  
#### Per rendere una variabile visibile solo all'interno di una routine  
  
-   Inserire l'istruzione `Dim` relativa alla variabile all'interno della routine ma all'esterno di un qualsiasi blocco, ad esempio un blocco `With`...`End With`.  
  
     È possibile fare riferimento alla variabile solo dall'interno della routine, inclusi gli eventuali blocchi contenuti nella routine.  
  
## Ambito a livello di modulo o di spazio dei nomi  
 Per comodità, la singola espressione *a livello di modulo* fa riferimento ai moduli, alle classi e alle strutture.  L'ambito di una variabile a livello di modulo dipende dal livello di accesso della variabile  e dallo spazio dei nomi contenente il modulo, la classe o la struttura.  
  
#### Per rendere una variabile visibile in un modulo, una classe o una struttura  
  
1.  Inserire l'istruzione `Dim` relativa alla variabile all'interno del modulo, della classe o della struttura ma all'esterno di una qualsiasi routine.  
  
2.  Includere la parola chiave [Private](../../../../visual-basic/language-reference/modifiers/private.md) nell'istruzione `Dim`.  
  
3.  È possibile fare riferimento alla variabile da qualsiasi punto all'interno del modulo, della classe o della struttura, ma non dall'esterno.  
  
#### Per rendere una variabile visibile in uno spazio dei nomi  
  
1.  Inserire l'istruzione `Dim` relativa alla variabile all'interno del modulo, della classe o della struttura ma all'esterno di una qualsiasi routine.  
  
2.  Includere la parola chiave [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) o [Public](../../../../visual-basic/language-reference/modifiers/public.md) nell'istruzione `Dim`.  
  
3.  È possibile fare riferimento alla variabile da qualsiasi punto all'interno dello spazio dei nomi contenente il modulo, la classe o la struttura.  
  
## Esempio  
 Nell'esempio riportato di seguito viene dichiarata una variabile a livello di modulo e la visibilità della variabile viene limitata al codice interno al modulo.  
  
```  
Module demonstrateScope  
    Private strMsg As String  
    Sub initializePrivateVariable()  
        strMsg = "This variable cannot be used outside this module."  
    End Sub  
    Sub usePrivateVariable()  
        MsgBox(strMsg)  
    End Sub  
End Module  
```  
  
 Nell'esempio precedente tutte le routine definite nel modulo `demonstrateScope` possono fare riferimento alla variabile `String` `strMsg`.  Quando viene chiamata la routine `usePrivateVariable`, il contenuto della variabile di stringa `strMsg` viene visualizzato in una finestra di dialogo.  
  
 Modificando l'esempio precedente come indicato di seguito, è possibile fare riferimento alla variabile di stringa `strMsg` da qualsiasi parte di codice nello spazio dei nomi della relativa dichiarazione.  
  
```  
Public strMsg As String  
```  
  
## Programmazione efficiente  
 Più ristretto è l'ambito di una variabile, minori saranno le possibilità di fare riferimento accidentalmente a tale variabile al posto di un'altra con lo stesso nome.  Questo consente inoltre di ridurre al minimo i problemi di corrispondenza dei riferimenti.  
  
## Sicurezza di .NET Framework  
 Più ristretto è l'ambito di una variabile, minori saranno le probabilità che la variabile possa essere utilizzata in modo improprio da malware.  
  
## Vedere anche  
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Lifetime in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Variables](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md)