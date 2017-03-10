---
title: "Expression is a value and therefore cannot be the target of an assignment | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30068"
  - "vbc30068"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30068"
ms.assetid: d65141e1-f31e-4ac5-a3b8-0b2e02a71ebf
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Expression is a value and therefore cannot be the target of an assignment
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un'istruzione tenta di assegnare un valore a un'espressione.  È possibile assegnare un valore solo a una variabile, a una proprietà o a un elemento di matrice modificabile in fase di esecuzione.  Nell'esempio riportato di seguito viene illustrato come può verificarsi questo errore.  
  
```  
Dim yesterday As Integer  
ReadOnly maximum As Integer = 45  
yesterday + 1 = DatePart(DateInterval.Day, Now)  
' The preceding line is an ERROR because of an expression on the left.  
maximum = 50  
' The preceding line is an ERROR because maximum is declared ReadOnly.  
```  
  
 Esempi simili possono essere validi per le proprietà e gli elementi di matrice.  
  
 **Accesso indiretto.** Questo errore può essere generato anche dall'accesso indiretto attraverso un tipo di valore.  Nell'esempio di codice riportato di seguito viene effettuato un tentativo di impostare il valore dell'oggetto <xref:System.Drawing.Point> accedendo indirettamente ad esso attraverso la proprietà <xref:System.Windows.Forms.Control.Location%2A>.  
  
```  
' Assume this code runs inside Form1.  
Dim exitButton As New System.Windows.Forms.Button()  
exitButton.Text = "Exit this form"  
exitButton.Location.X = 140  
' The preceding line is an ERROR because of no storage for Location.  
```  
  
 L'ultima istruzione dell'esempio precedente non viene eseguita correttamente poiché crea solo un'allocazione temporanea per la struttura dell'oggetto <xref:System.Drawing.Point> restituita dalla proprietà <xref:System.Windows.Forms.Control.Location%2A>.  Una struttura è un tipo di valore e la struttura temporanea non viene mantenuta dopo l'esecuzione dell'istruzione.  Per risolvere il problema, è necessario dichiarare e utilizzare una variabile per la proprietà <xref:System.Windows.Forms.Control.Location%2A> che crei un'allocazione più permanente per la struttura dell'oggetto <xref:System.Drawing.Point>.  Nell'esempio riportato di seguito viene illustrato il codice che può sostituire l'ultima istruzione dell'esempio precedente.  
  
```  
Dim exitLocation as New System.Drawing.Point(140, exitButton.Location.Y)  
exitButton.Location = exitLocation  
```  
  
 **ID errore:** BC30068  
  
### Per correggere l'errore  
  
-   Se l'istruzione assegna un valore a un'espressione, sostituire quest'ultima con una variabile, una proprietà o un elemento di matrice modificabile.  
  
-   Se l'istruzione effettua l'accesso indiretto attraverso un tipo di valore, in genere una struttura, creare una variabile che contenga il tipo di valore.  
  
-   Assegnare alla variabile la struttura o un altro tipo di valore appropriato.  
  
-   Utilizzare la variabile per accedere alla proprietà e assegnare a quest'ultima un valore.  
  
## Vedere anche  
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)   
 [Troubleshooting Procedures](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)