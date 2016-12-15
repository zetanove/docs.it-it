---
title: "Procedures in Visual Basic | Microsoft Docs"
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
  - "procedures, structured code"
  - "Visual Basic code, procedures"
  - "procedures, types of"
  - "structured code, procedures"
  - "procedures"
ms.assetid: 9effbcf0-80a0-4d1a-98f4-2c6920592766
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedures in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Una *routine* è un blocco di istruzioni di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] racchiuse da un'istruzione di dichiarazione \(`Function`, `Sub`, `Operator`, `Get`, `Set`\) e una dichiarazione `End` corrispondente.  Tutte le istruzioni eseguibili di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] devono trovarsi nella stessa routine.  
  
## Chiamare una routine  
 Una routine viene richiamata da un punto diverso nel codice.  Si tratta di una *chiamata di routine*.  Quando la routine ha terminato l'esecuzione, restituisce il controllo al codice che l'ha richiamata. Tale codice è noto come *codice chiamante*.  Il codice chiamante è un'istruzione, o un'espressione all'interno di un'istruzione, che specifica la routine per nome e le trasferisce il controllo.  
  
## Chiusura di una routine  
 Al termine dell'esecuzione, la routine restituisce il controllo al codice che effettua la chiamata.  A questo scopo, potrebbe essere utilizzata un'[Return Statement](../../../../visual-basic/language-reference/statements/return-statement.md), l'istruzione [Exit Statement](../../../../visual-basic/language-reference/statements/exit-statement.md) appropriata per la routine o l'istruzione [End \<keyword\> Statement](../../../../visual-basic/language-reference/statements/end-keyword-statement.md) della routine.  Il controllo passa quindi al codice che effettua la chiamata a seconda del punto della chiamata della routine.  
  
-   Con un'istruzione `Return`, il controllo ritorna immediatamente al codice che effettua la chiamata.  Le istruzioni che seguono l'istruzione `Return` non vengono eseguite.  Nella stessa routine possono essere presenti più istruzioni `Return`.  
  
-   Con un'istruzione `Exit Sub` o `Exit Function`, il controllo ritorna immediatamente al codice chiamante.  Le istruzioni che seguono l'istruzione `Exit` non vengono eseguite.  Nella stessa routine possono essere presenti più istruzioni `Exit` ed è possibile combinare le istruzioni `Return` e `Exit`.  
  
-   Se una routine non ha istruzioni `Return` o `Exit` conclude con un'istruzione `End Sub` o `End Function`, `End Get` oppure `End Set` che segue l'ultima istruzione del corpo di una routine.  L'istruzione `End` restituisce immediatamente il controllo al codice chiamante.  In una routine, invece, può essere presente una sola istruzione `End`.  
  
## Parametri e argomenti  
 Nella maggior parte dei casi, è necessario che una routine venga utilizzata su dati diversi ogni volta che la si chiama.  È possibile passare questa informazione alla routine come parte della chiamata di routine.  La routine definisce zero o più *parametri*, ognuno dei quali rappresenta un valore che si prevede venga passato a questa.  A ogni parametro nella definizione della routine corrisponde un *argomento* nella chiamata di routine.  Un argomento rappresenta il valore che viene passato al parametro corrispondente in una determinata chiamata di routine.  
  
## Tipi di routine  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] vengono utilizzati diversi tipi di routine:  
  
-   Le [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) eseguono operazioni ma non restituiscono alcun valore al codice chiamante.  
  
-   Le routine di gestione degli eventi sono routine `Sub` eseguite in risposta a un evento generato dall'azione utente o da un'occorrenza in un programma.  
  
-   Le [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md) restituiscono un valore al codice chiamante.  Possono eseguire altre operazioni prima di essere chiuse.  
  
-   Le [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md) restituiscono e assegnano valori delle proprietà su oggetti o moduli.  
  
-   Le [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md) consentono di definire il comportamento di un operatore standard quando uno o entrambi gli operandi sono una classe o una struttura appena definiti.  
  
-   Le [Generic Procedures in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md) consentono di definire uno o più *parametri di tipo* oltre ai loro normali parametri, in modo che il codice chiamante riesca a passare tipi di dati specifici ogni volta che effettua una chiamata.  
  
## Routine e codice strutturato  
 È necessario che ogni riga di codice eseguibile nell'applicazione si trovi all'interno di una routine, come `Main`, `calculate` o `Button1_Click`.  Per rendere l'applicazione più leggibile, suddividere le routine più grandi in routine più piccole.  
  
 Le routine sono utili per l'esecuzione di attività ripetute o condivise, come calcoli utilizzati di frequente, gestione di testo e controlli e operazioni di database.  È possibile chiamare una routine da molti punti diversi del codice per utilizzare le routine come blocchi predefiniti dell'applicazione.  
  
 La strutturazione del codice tramite routine presenta i seguenti vantaggi:  
  
-   Le routine consentono di dividere i programmi in unità logiche discrete.  È possibile eseguire più facilmente il debug di unità separate rispetto al debug eseguito su un intero programma privo di routine.  
  
-   Dopo aver sviluppato le routine da utilizzare in un programma, è possibile utilizzarle in altri programmi, spesso con modifiche minime o nulle.  In questo modo si evita la duplicazione del codice.  
  
## Vedere anche  
 [How to: Create a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Recursive Procedures](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Generic Procedures in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)   
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)