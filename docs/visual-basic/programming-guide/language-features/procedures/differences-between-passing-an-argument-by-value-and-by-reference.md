---
title: "Differences Between Passing an Argument By Value and By Reference (Visual Basic) | Microsoft Docs"
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
  - "ByRef keyword, passing arguments by reference"
  - "Visual Basic code, procedures"
  - "procedures, passing arguments"
  - "ByVal keyword, passing arguments by value"
  - "arguments [Visual Basic], passing by value or by reference"
ms.assetid: 5f5c38fe-3e2d-494c-8fff-f4025b55ec93
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Differences Between Passing an Argument By Value and By Reference (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando si passano uno o più argomenti a una routine, ciascun argomento corrisponde a un elemento di programmazione sottostante nel codice chiamante.  È possibile passare il valore di tale elemento sottostante oppure un riferimento a esso.  Questa procedura è nota come *meccanismo di passaggio*.  
  
## Passaggio per valore  
 Per passare un argomento *per valore*, è necessario specificare la parola chiave [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) per il parametro corrispondente nella definizione della routine.  Quando si utilizza questo meccanismo di passaggio, il valore dell'elemento di programmazione sottostante viene copiato da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] in una variabile locale nella routine.  Il codice della routine non ha accesso all'elemento sottostante nel codice chiamante.  
  
## Passaggio per riferimento  
 Per passare un argomento *per riferimento*, è necessario specificare la parola chiave [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) per il parametro corrispondente nella definizione della routine.  Quando si utilizza questo meccanismo di passaggio, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] assegna alla routine un riferimento diretto all'elemento di programmazione sottostante nel codice chiamante.  
  
## Meccanismo di passaggio e tipo di elemento  
 Il meccanismo di passaggio non equivale alla classificazione del tipo di elemento sottostante.  Il passaggio per valore o per riferimento si riferisce a quanto viene fornito da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] al codice della routine.  Un tipo di valore o un tipo di riferimento si riferisce alla modalità di memorizzazione di un elemento di programmazione.  
  
 Il meccanismo di passaggio e il tipo di elemento sono, tuttavia, correlati tra loro.  Il valore di un tipo di riferimento costituisce un puntatore ai dati presenti in un altro punto della memoria.  Quando si passa un tipo di riferimento per valore, il codice della routine presenta un puntatore ai dati dell'elemento sottostante, anche se non può accedere all'elemento sottostante vero e proprio.  Se, ad esempio, l'elemento è una variabile di matrice, il codice della routine non può accedere alla variabile stessa ma può accedere ai membri della matrice.  
  
## Possibilità di modificare  
 Quando si passa un elemento non modificabile come argomento, la routine non può mai modificarlo nel codice chiamante, a prescindere dal fatto che sia passato come `ByVal` o `ByRef`.  
  
 Per un elemento modificabile, nella tabella che segue viene riepilogata l'interazione tra il tipo di elemento e il meccanismo di passaggio.  
  
|Tipo di elemento|`ByVal` passato|`ByRef` passato|  
|----------------------|---------------------|---------------------|  
|Tipo di valore \(contiene solo un valore\).|La routine non può modificare la variabile o i suoi membri.|La routine può modificare la variabile e i suoi membri.|  
|Tipo di riferimento \(contiene un puntatore a un'istanza di classe o di struttura\)|La routine non può modificare la variabile ma può modificare i membri dell'istanza ai quali essa punta.|La routine può modificare la variabile e i membri dell'istanza ai quali essa punta.|  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Differences Between Modifiable and Nonmodifiable Arguments](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [How to: Change the Value of a Procedure Argument](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [How to: Protect a Procedure Argument Against Value Changes](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [How to: Force an Argument to Be Passed by Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)