---
title: "How to: Create a New Variable (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Dim statement"
  - "variables [Visual Basic], creating"
ms.assetid: 35300be3-77b0-4bef-a156-034d3cdedde0
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# How to: Create a New Variable (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile creare una nuova variabile utilizzando un'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md).  
  
### Per creare una nuova variabile  
  
1.  Dichiarare la variabile in un'istruzione `Dim`.  
  
    ```  
  
    Dim newCustomer  
    ```  
  
2.  Includere specifiche per le caratteristiche della variabile, ad esempio [Private](../../../../visual-basic/language-reference/modifiers/private.md), [Static](../../../../visual-basic/language-reference/modifiers/static.md), [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) o [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md).  Per ulteriori informazioni, vedere [Declared Element Characteristics](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md).  
  
    ```  
    Public Static newCustomer  
    ```  
  
     Non è necessaria la parola chiave `Dim` se si utilizzano altre parole chiave nella dichiarazione.  
  
3.  Inserire il nome della variabile dopo le specifiche. Tale nome deve rispettare le regole e le convenzioni [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  Per ulteriori informazioni, vedere [Declared Element Names](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
    ```  
    Public Static newCustomer  
    ```  
  
4.  Dopo il nome inserire la clausola [As](../../../../visual-basic/language-reference/statements/as-clause.md) per specificare il tipo di dati della variabile.  
  
    ```  
    Public Static newCustomer As Customer   
    ```  
  
     Se non si specifica il tipo di dati, verrà utilizzato il tipo predefinito `Object`.  
  
5.  Dopo la clausola `As`, inserire il segno uguale \(`=`\) dopo il quale inserire il valore iniziale della variabile.  
  
     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] assegna il valore specificato alla variabile a ogni esecuzione dell'istruzione `Dim`.  Se non si specifica un valore iniziale, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] assegna il valore iniziale predefinito per il tipo di dati della variabile la prima volta che inserisce il codice contenente l'istruzione `Dim`.  
  
     Se la variabile è un tipo di riferimento, è possibile creare un'istanza della rispettiva classe includendo la parola chiave [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md) nella clausola `As`.  Se non si utilizza `New`, il valore iniziale della variabile è [Nothing](../../../../visual-basic/language-reference/nothing.md).  
  
    ```  
    Public Static newCustomer As New Customer  
    ```  
  
## Vedere anche  
 [Variables](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Declared Element Names](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Declared Element Characteristics](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Statements](../../../../visual-basic/language-reference/statements/index.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md)