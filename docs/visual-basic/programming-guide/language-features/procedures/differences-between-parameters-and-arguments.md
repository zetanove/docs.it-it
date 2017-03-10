---
title: "Differences Between Parameters and Arguments (Visual Basic) | Microsoft Docs"
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
  - "parameters, and arguments"
  - "procedure arguments"
  - "Visual Basic code, procedures"
  - "arguments [Visual Basic], and parameters"
  - "procedure parameters"
  - "parameters, definition"
ms.assetid: c237c056-74f4-4749-9f2c-15864f139a31
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Differences Between Parameters and Arguments (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nella maggior parte dei casi una routine richiede alcune informazioni sulle circostanze in cui è stata chiamata.  Una routine che esegue attività ripetute o condivise utilizza informazioni diverse per ogni chiamata.  Tali informazioni sono costituite da variabili, costanti ed espressioni passate alla routine al momento della chiamata.  
  
 Per comunicare le informazioni alla routine, quest'ultima definisce un *parametro* a cui il codice chiamante passa un *argomento*.  Il parametro può essere paragonato a un'area di parcheggio e l'argomento a un'automobile.  Così come diverse automobili possono parcheggiare nella stessa area in momenti diversi, il codice chiamante può passare un argomento differente allo stesso parametro ogni volta che chiama la routine.  
  
## Parametri  
 Un *parametro* rappresenta un valore da passare alla routine al momento della chiamata.  La dichiarazione della routine ne definisce i parametri.  
  
 Quando si definisce una routine `Function` o `Sub`, è necessario specificare un *elenco di parametri* tra parentesi immediatamente dopo il nome della routine.  Per ciascun parametro è necessario indicare un nome, un tipo di dati e un meccanismo di passaggio \([ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)\).  È possibile anche indicare che un parametro è facoltativo.  Ciò significa che il codice che effettua la chiamata non deve passare un valore per il parametro.  
  
 Il nome di ciascun parametro funge da *variabile locale* all'interno della routine   e viene utilizzato come qualsiasi altra variabile.  
  
## Argomenti  
 Un *argomento* rappresenta il valore passato al parametro di una routine quando quest'ultima viene chiamata.  Gli argomenti vengono forniti dal codice chiamante al momento della chiamata.  
  
 Quando si chiama una routine `Function` o `Sub`, è necessario includere un *elenco di argomenti* tra parentesi immediatamente dopo il nome della routine.  Ciascun argomento corrisponde al parametro nella stessa posizione nell'elenco.  
  
 A differenza della definizione del parametro, gli argomenti non includono nomi.  Ogni argomento è un'espressione, che può contenere zero o più variabili, costanti e valori letterali.  Il tipo di dati dell'espressione valutata in genere corrisponde al tipo di dati definito per il parametro corrispondente. In ogni caso deve essere convertibile nel tipo del parametro.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [How to: Define a Parameter for a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-parameter-for-a-procedure.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Recursive Procedures](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)