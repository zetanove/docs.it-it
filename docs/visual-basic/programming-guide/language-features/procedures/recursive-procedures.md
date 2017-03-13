---
title: "Recursive Procedures (Visual Basic) | Microsoft Docs"
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
  - "Visual Basic code, procedures"
  - "procedures, that call themselves"
  - "procedures, recursive"
  - "procedures, calling"
  - "recursive procedures"
  - "functions [Visual Basic], calling recursively"
  - "recursion"
ms.assetid: ba1d3962-b4c3-48d3-875e-96fdb4198327
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Recursive Procedures (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine *ricorsiva* è una routine che chiama se stessa.  In genere non si tratta del metodo più efficace per la scrittura di codice [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 Nella routine riportata di seguito viene utilizzata la ricorsione per calcolare il fattoriale del relativo argomento originale.  
  
 [!code-vb[VbVbcnProcedures#51](./codesnippet/VisualBasic/recursive-procedures_1.vb)]  
  
## Considerazioni sulle routine ricorsive  
 **Condizioni limitanti**.  È necessario progettare una routine ricorsiva per verificare almeno una condizione in grado di terminare la ricorsione e gestire inoltre il caso in cui nessuna condizione del genere venga soddisfatta nell'ambito di un numero ragionevole di chiamate ricorsive.  In assenza di almeno una condizione che possa essere soddisfatta senza errori, il rischio di eseguire una routine in un ciclo infinito è piuttosto elevato.  
  
 **Utilizzo della memoria**.  L'applicazione dispone di uno spazio limitato per le variabili locali.  Ogni volta che una routine chiama se stessa, utilizza una quantità di spazio superiore per le copie aggiuntive delle variabili locali.  Se questo processo continua in modo indefinito, provoca un errore <xref:System.StackOverflowException>.  
  
 **Efficienza**.  È quasi sempre possibile sostituire un ciclo per la ricorsione.  Un ciclo non è caratterizzato dal sovraccarico del passaggio degli argomenti, dell'inizializzazione della memoria aggiuntiva e della restituzione dei valori.  Le prestazioni migliorano in modo significativo senza chiamate ricorsive.  
  
 **Ricorsione reciproca**.  Se due routine si chiamano tra loro, è possibile che le prestazioni subiscano un notevole peggioramento o addirittura che si verifichi un ciclo infinito.  Questo tipo di progettazione presenta gli stessi problemi di una singola routine ricorsiva, ma può risultare più difficile rilevarla ed eseguirne il debug.  
  
 **Chiamate con parentesi**.  Quando una routine `Function` chiama se stessa in modo ricorsivo, è necessario aggiungere le parentesi dopo il nome, anche se non è disponibile un elenco di argomenti.  In caso contrario, il nome della funzione viene considerato come se rappresentasse il valore restituito dalla funzione.  
  
 **Verifica**.  Se si scrive una routine ricorsiva, è necessario verificarla con grande attenzione per accettarsi che soddisfi sempre alcune condizioni limitanti.  Accertarsi inoltre che a causa del numero eccessivo di chiamate ricorsive non si verifichino problemi di memoria insufficiente.  
  
## Vedere anche  
 <xref:System.StackOverflowException>   
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Troubleshooting Procedures](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [Loop Structures](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Risoluzione dei problemi relativi alle eccezioni: System.StackOverflowException](../Topic/Troubleshooting%20Exceptions:%20System.StackOverflowException.md)