---
title: "Passing Arguments by Position and by Name (Visual Basic) | Microsoft Docs"
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
  - "arguments [Visual Basic], passing by name"
  - "procedures, arguments"
  - ":= passing arguments"
  - "procedure arguments"
  - "Visual Basic code, procedures"
  - "named arguments, passing arguments"
  - "arguments [Visual Basic], passing by position"
  - "Function procedures, passing arguments"
  - "named parameters, passing arguments"
  - "named arguments"
  - "passing parameters, named parameter arguments"
  - "passing parameters, by position"
  - "procedures, calling"
  - "named parameters"
  - "Sub procedures, passing arguments"
  - "argument passing"
  - "passing parameters, by name"
  - "argument passing, by position"
  - "arguments [Visual Basic], listing by name"
ms.assetid: 1ad7358f-1da9-48da-a95b-f3c7ed41eff3
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Passing Arguments by Position and by Name (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Quando si chiama una routine `Sub` o `Function`, è possibile passare gli argomenti *per posizione*, vale a dire nell'ordine in cui vengono visualizzati nella definizione della routine, oppure *per nome*, senza tener conto della posizione.  
  
 Quando si passa un argomento per nome, si specifica il nome dichiarato dell'argomento seguito da un segno di due punti e da un segno di uguale \(`:=`\), seguiti dal valore dell'argomento.  È possibile fornire gli argomenti nominati in qualsiasi ordine.  
  
 Nella seguente routine `Sub` ad esempio vengono utilizzati tre argomenti:  
  
 [!code-vb[VbVbcnProcedures#41](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_1.vb)]  
  
 Quando si chiama questa routine, è possibile fornire gli argomenti tramite posizione, tramite nome o utilizzando una combinazione dei due criteri.  
  
## Passaggio di argomenti tramite posizione  
 È possibile chiamare la routine  `studentInfo`  con i relativi argomenti passati per posizione e delimitati da virgole, come mostrato nell'esempio seguente:  
  
 [!code-vb[VbVbcnProcedures#42](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_2.vb)]  
  
 Se si omette un argomento facoltativo in un elenco di argomenti di posizione, indicarne la posizione con una virgola.  Nell'esempio riportato di seguito viene chiamata la routine `studentInfo` senza l'argomento  `age` .  
  
 [!code-vb[VbVbcnProcedures#43](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_3.vb)]  
  
## Passaggio di argomenti tramite nome  
 In alternativa, è possibile chiamare `studentInfo` con gli argomenti passati per nome e delimitati da virgole, come mostrato nell'esempio seguente:  
  
 [!code-vb[VbVbcnProcedures#44](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_4.vb)]  
  
## Combinazione di argomenti tramite posizione e tramite nome  
 È possibile fornire argomenti tramite posizione e tramite nome in un'unica chiamata di routine, come mostrato nell'esempio che segue:  
  
 [!code-vb[VbVbcnProcedures#45](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/passing-arguments-by-position-and-by-name_5.vb)]  
  
 Nell'esempio precedente non è necessaria alcuna virgola aggiuntiva per indicare la posizione dell'argomento `age` omesso, in quanto  `birth`  viene passato per nome.  
  
 Quando si specificano argomenti sia per posizione che per nome, è necessario che tutti gli argomenti di posizione siano indicati per primi.  Una volta fornito un argomento tramite nome, è necessario passare tramite nome tutti quelli rimanenti.  
  
## Passaggio di argomenti facoltativi tramite nome  
 Il passaggio di argomenti tramite nome è particolarmente utile quando si chiama una routine che contiene più argomenti facoltativi.  Se si forniscono gli argomenti tramite nome, non è necessario utilizzare virgole per indicare gli argomenti di posizione mancanti.  Il passaggio di argomenti tramite nome, inoltre, rende più facile registrare gli argomenti in fase di passaggio e quelli omessi.  
  
## Restrizioni al passaggio di argomenti tramite nome  
 Non è possibile passare argomenti tramite nome per evitare di inserire argomenti obbligatori.  È possibile omettere solo gli argomenti facoltativi.  
  
 Non è possibile passare una matrice di parametri tramite nome,  perché, quando si chiama una routine, si fornisce un numero non definito di argomenti separati da virgole per la matrice di parametro e il compilatore non può associare più argomenti a un singolo nome.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Parameter Arrays](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)   
 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)