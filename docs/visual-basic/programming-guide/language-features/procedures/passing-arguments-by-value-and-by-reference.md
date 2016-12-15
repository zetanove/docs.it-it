---
title: "Passing Arguments by Value and by Reference (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "ByRef keyword, passing arguments by reference"
  - "Visual Basic code, procedures"
  - "passing arguments, by value or by reference"
  - "ByVal keyword, passing arguments by value"
  - "arguments [Visual Basic], passing by value or by reference"
  - "argument passing, by value or by reference"
ms.assetid: fd8a9de6-7178-44d5-a9bf-458d4ad907c2
caps.latest.revision: 23
caps.handback.revision: 23
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Passing Arguments by Value and by Reference (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] è possibile passare un argomento a una routine *in base al valore* o *in base al riferimento*.  Tale funzionalità è nota come *meccanismo di passaggio* e determina se la routine può modificare l'elemento di programmazione sottostante all'argomento nel codice chiamante.  Il meccanismo di passaggio è definito nella dichiarazione della routine di ogni parametro mediante la specifica della parola chiave [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md).  
  
## Differenze  
 È importante tenere presenti i diversi fattori distintivi che interagiscono nel corso del passaggio di un argomento a una routine.  
  
-   La possibilità che l'elemento di programma sottostante sia modificabile o meno  
  
-   La possibilità che l'argomento stesso sia modificabile o meno  
  
-   La possibilità che l'argomento venga passato in base al valore o al riferimento  
  
-   La possibilità che il tipo di dati dell'argomento sia un tipo di valore o di riferimento  
  
 Per ulteriori informazioni, vedere [Differences Between Modifiable and Nonmodifiable Arguments](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md) e [Differences Between Passing an Argument By Value and By Reference](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md).  
  
## Scelta del meccanismo di passaggio  
 La scelta del meccanismo di passaggio deve essere valutata attentamente per ogni argomento.  
  
-   **Protezione**.  Nella scelta tra i due meccanismi di passaggio, il criterio più importante è l'esposizione delle variabili chiamanti da modificare.  Il vantaggio del passaggio di un argomento tramite `ByRef` è che la routine può restituire un valore al codice di chiamata tramite l'argomento.  Il vantaggio del passaggio di un argomento tramite valore `ByVal` è che esso impedisce che la variabile venga modificata dalla routine.  
  
-   **Prestazioni**.  Sebbene il meccanismo di passaggio possa avere effetto sulle prestazioni del codice, la differenza è in genere irrilevante.  Un'eccezione è rappresentata da un tipo di valore passato tramite valore \(`ByVal`\).  In questo caso, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente di copiare l'intero contenuto di dati dell'argomento.  Di conseguenza, per un tipo di valore di grandi dimensioni, come una struttura, il passaggio in base al riferimento \(`ByRef`\) risulta più efficiente.  
  
     Per i tipi di riferimento, viene copiato solo il puntatore ai dati \(quattro byte sulle piattaforme a 32 bit, otto byte su quelle a 64 bit\).  Pertanto, è possibile passare argomenti di tipo `String` o `Object` in base al valore senza compromettere le prestazioni.  
  
## Determinazione del meccanismo di passaggio  
 Nella dichiarazione della routine è specificato il meccanismo di passaggio di ogni parametro.  Il codice chiamante non può eseguire l'override di un meccanismo `ByVal`.  
  
 Se un parametro viene dichiarato con `ByRef`, il codice chiamante può imporre il meccanismo `ByVal` racchiudendo il nome dell'argomento tra parentesi nella chiamata.  Per ulteriori informazioni, vedere [How to: Force an Argument to Be Passed by Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md).  
  
 Per impostazione predefinita, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli argomenti vengono passati per valore.  
  
## Quando passare un argomento per valore  
  
-   Se l'elemento di codice chiamante sottostante all'argomento non è modificabile, dichiarare il parametro corrispondente [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md).  Nessun codice può modificare il valore di un elemento non modificabile.  
  
-   Se l'elemento sottostante è modificabile, ma non si desidera consentire alla routine di modificarne il valore, dichiarare il parametro `ByVal`.  Solo il codice chiamante può modificare il valore di un elemento modificabile passato in base al valore.  
  
## Quando passare un argomento per riferimento  
  
-   Se la routine richiede la modifica dell'elemento sottostante nel codice chiamante, dichiarare il parametro corrispondente [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md).  
  
-   Se l'esecuzione corretta del codice dipende dalla modifica dell'elemento nel codice chiamante da parte della routine, dichiarare il parametro `ByRef`.  Se il passaggio avviene in base al valore o il codice chiamante esegue l'override del meccanismo di passaggio `ByRef` racchiudendo l'argomento tra parentesi, la chiamata alla routine potrebbe produrre risultati imprevisti.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio seguente viene illustrato quando passare argomenti per valore e quando passarli per riferimento.  La routine `Calculate` dispone sia di un parametro `ByVal` che di un parametro `ByRef`.  Dati un tasso di interesse, `rate`, e una somma di denaro, `debt`, l'attività della routine consiste nel calcolare un nuovo valore per `debt` che sia il risultato dell'applicazione del tasso di interesse al valore originale di `debt`.  Poiché `debt` è un parametro `ByRef`, il nuovo totale viene riflesso nel valore dell'argomento nel codice chiamante che corrisponde a `debt`.  Il parametro `rate` è un parametro `ByVal` poiché `Calculate` non deve modificarne il valore.  
  
### Codice  
 [!code-vb[VbVbcnProcedures#74](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/passing-arguments-by-value-and-by-reference_1.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [How to: Change the Value of a Procedure Argument](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [How to: Protect a Procedure Argument Against Value Changes](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [How to: Force an Argument to Be Passed by Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)