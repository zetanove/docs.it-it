---
title: "How to: Create a Procedure (Visual Basic) | Microsoft Docs"
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
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "Visual Basic code, reusing"
  - "procedure declarations"
  - "procedures, about procedures"
ms.assetid: 4f779247-0b50-47e8-9e5c-ab5cf39ac0d2
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# How to: Create a Procedure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine deve essere racchiusa tra un'istruzione di dichiarazione di inizio \(`Sub` o `Function`\) e una di fine \(`End Sub` o `End Function`\).  Tra le due istruzioni è racchiuso tutto il codice della routine.  
  
 Una routine non può contenere un'altra routine, pertanto le istruzioni di inizio e di fine devono essere esterne a qualsiasi altra routine.  
  
 Se si dispone di codice che esegue la stessa attività in posizioni diverse, è possibile scrivere l'attività una sola volta come routine, quindi chiamarla dalle diverse posizioni del codice.  
  
### Per creare una routine che non restituisce alcun valore  
  
1.  Utilizzare un'istruzione `Sub` all'esterno di qualsiasi altra routine, seguita da un'istruzione `End Sub`.  
  
2.  Nell'istruzione `Sub` far seguire la parola chiave `Sub` dal nome della routine, quindi dall'elenco dei parametri racchiuso tra parentesi.  
  
3.  Inserire le istruzioni del codice della routine tra le istruzioni `Sub` e `End Sub`.  
  
### Per creare una routine che restituisce un valore  
  
1.  Al di fuori di qualsiasi altra routine, utilizzare un'istruzione `Function` seguita da un'istruzione `End Function`.  
  
2.  Nell'istruzione `Function` far seguire la parola chiave `Function` dal nome della routine, quindi dall'elenco dei parametri tra parentesi, infine da una clausola `As` che specifica il tipo di dati del valore restituito.  
  
3.  Inserire le istruzioni del codice della routine tra le istruzioni `Function` e `End Function`.  
  
4.  Utilizzare un'istruzione `Return` per restituire il valore al codice chiamante.  
  
### Per collegare la nuova routine ai vecchi blocchi di codice ripetitivi  
  
1.  Accertarsi di aver definito la nuova routine in una posizione che ne consenta l'accesso da parte del vecchio codice.  
  
2.  Nel vecchio blocco di codice ripetitivo sostituire le istruzioni che eseguono l'attività ripetitiva con un'istruzione singola che chiama la routine `Sub` o `Function`.  
  
3.  Se la routine è una `Function` che restituisce un valore, verificare che l'istruzione di chiamata esegua un'azione con il valore restituito, ad esempio lo memorizzi in una variabile, onde evitare che il valore venga perduto.  
  
## Esempio  
 La routine `Function` che segue consente di calcolare il lato più lungo, o ipotenusa, di un triangolo retto, dati i valori degli altri due lati.  
  
 [!code-vb[VbVbcnProcedures#1](./codesnippet/VisualBasic/how-to-create-a-procedure_1.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Recursive Procedures](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Programmazione orientata ad oggetti](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)