---
title: "How to: Change the Value of a Procedure Argument (Visual Basic) | Microsoft Docs"
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
  - "procedures, arguments"
  - "procedures, parameters"
  - "procedure arguments"
  - "arguments [Visual Basic], passing by reference"
  - "Visual Basic code, procedures"
  - "arguments [Visual Basic], ByVal"
  - "arguments [Visual Basic], passing by value"
  - "procedure parameters"
  - "arguments [Visual Basic], ByRef"
  - "arguments [Visual Basic], changing value"
ms.assetid: 6fad2368-5da7-4c07-8bf8-0f4e65a1be67
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# How to: Change the Value of a Procedure Argument (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando viene effettuata una chiamata a una routine, ciascun argomento specificato corrisponde a uno dei parametri definiti nella routine.  In alcuni casi, il codice della routine può modificare il valore sottostante a un argomento nel codice chiamante.  In altri, la routine può modificare solo la relativa copia locale di un argomento.  
  
 Quando si effettua una chiamata alla routine, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] viene creata una copia locale di ogni argomento passato [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md).  Per ciascun argomento passato [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] assegna al codice della routine un riferimento diretto all'elemento di programmazione sottostante all'argomento nel codice chiamante.  
  
 Se tale elemento sottostante è modificabile e l'argomento viene passato `ByRef`, il codice della routine può utilizzare il riferimento diretto per modificare il valore dell'elemento nel codice chiamante.  
  
## Modifica del valore sottostante  
  
#### Per modificare il valore sottostante di un argomento di routine nel codice chiamante  
  
1.  Nella dichiarazione della routine specificare [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) per il parametro che corrisponde all'argomento.  
  
2.  Nel codice chiamante passare un elemento di programmazione modificabile come argomento.  
  
3.  Nel codice chiamante non racchiudere l'argomento tra parentesi nell'elenco degli argomenti.  
  
4.  Nel codice della routine utilizzare il nome del parametro per assegnare un valore all'elemento sottostante nel codice chiamante.  
  
 Per una dimostrazione, vedere l'esempio riportato di seguito.  
  
## Modifica delle copie locali  
 Se l'elemento sottostante nel codice chiamante non è modificabile o se l'argomento viene passato `ByVal`, la routine non può modificare il relativo valore nel codice chiamante.  Può invece modificare la relativa copia locale di questo tipo di argomento.  
  
#### Per modificare la copia di un argomento di routine nel codice della routine  
  
1.  Nella dichiarazione della routine specificare [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) per il parametro che corrisponde all'argomento.  
  
     In alternativa  
  
     Nel codice chiamante racchiudere l'argomento tra parentesi nell'elenco degli argomenti.  In questo modo, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] verrà forzato a passare l'argomento per valore, anche se nel parametro corrispondente è specificato `ByRef`.  
  
2.  Nel codice della routine utilizzare il nome del parametro per assegnare un valore alla copia locale dell'argomento.  Il valore sottostante nel codice chiamante non verrà modificato.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrate due routine che accettano una variabile di matrice e operano sui relativi elementi.  La routine `increase` aggiunge semplicemente uno a ogni elemento.  La routine `replace` assegna una nuova matrice al parametro `a()`, quindi aggiunge uno a ogni elemento.  
  
 [!code-vb[VbVbcnProcedures#35](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#36](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#37](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_3.vb)]  
  
 Alla prima chiamata di `MsgBox` viene visualizzato "After increase\(n\): 11, 21, 31, 41".  Poiché la matrice `n` è un tipo di riferimento, la routine `replace` può modificarne i membri, anche se il meccanismo di passaggio è `ByVal`.  
  
 Alla seconda chiamata `MsgBox` viene visualizzato il seguente messaggio: "After replace\(n\): 101, 201, 301".  Poiché `n` viene passato `ByRef`, la routine `replace` può modificare la variabile `n` nel codice chiamante e assegnare a quest'ultima una nuova matrice.  Poiché `n` è un tipo di riferimento, la routine `replace` può anche modificarne i membri.  
  
 È possibile impedire alla routine di modificare la variabile nel codice chiamante.  Per informazioni, vedere [How to: Protect a Procedure Argument Against Value Changes](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md).  
  
## Compilazione del codice  
 Quando si passa una variabile tramite riferimento, è necessario usare la parola chiave `ByRef` per specificare tale meccanismo.  
  
 Per impostazione predefinita, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] gli argomenti vengono passati per valore.   È comunque buona norma di programmazione includere la parola chiave [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) con ogni parametro dichiarato,  al fine di agevolare la lettura del codice.  
  
## Sicurezza di .NET Framework  
 Esiste sempre un rischio potenziale quando si consente che una routine modifichi il valore sottostante un argomento nel codice chiamante.  Accertarsi che la modifica del valore sia prevista e verificare la validità del valore prima di utilizzarlo.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Differences Between Modifiable and Nonmodifiable Arguments](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [Differences Between Passing an Argument By Value and By Reference](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [How to: Protect a Procedure Argument Against Value Changes](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [How to: Force an Argument to Be Passed by Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)