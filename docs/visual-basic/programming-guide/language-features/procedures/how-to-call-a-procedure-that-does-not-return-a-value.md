---
title: "How to: Call a Procedure that Does Not Return a Value (Visual Basic) | Microsoft Docs"
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
  - "procedure calls, returning values"
  - "Visual Basic code, procedures"
  - "procedures, calling"
ms.assetid: 259b49a3-a3c1-4254-ba8c-73cdc4127703
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# How to: Call a Procedure that Does Not Return a Value (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine `Sub` non restituisce un valore al codice chiamante.  Viene chiamata in modo esplicito tramite un'istruzione di chiamata autonoma.  Non è possibile effettuare la chiamata utilizzando solo il nome della routine all'interno di un'espressione.  
  
### Per chiamare una routine Sub  
  
1.  Specificare il nome della routine `Sub`.  
  
2.  Aggiungere le parentesi dopo il nome della routine per racchiudere l'elenco di argomenti.  Se non sono presenti argomenti, è possibile omettere le parentesi.  L'utilizzo delle parentesi, tuttavia, semplifica la lettura del codice.  
  
3.  Racchiudere gli argomenti dell'elenco tra parentesi, separati da virgole.  Verificare di inserire gli argomenti nello stesso ordine con cui la routine `Sub` definisce i parametri corrispondenti.  
  
     Nell'esempio seguente viene chiamata la funzione <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] per attivare una finestra dell'applicazione.  <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> utilizza il titolo della finestra come unico argomento  e non restituisce alcun valore al codice chiamante.  Se un processo Blocco note non è in esecuzione, nell'esempio verrà generata un'eccezione <xref:System.ArgumentException>.  Il presupposto per la routine `Shell` è che le applicazioni si trovino nei percorsi specificati.  
  
     [!code-vb[VbVbalrCatRef#11](./codesnippet/VisualBasic/how-to-call-a-procedure-that-does-not-return-a-value_1.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.Shell%2A>   
 <xref:System.ArgumentException>   
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [How to: Create a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure.md)   
 [How to: Call a Procedure That Returns a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-returns-a-value.md)   
 [How to: Call an Event Handler in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-event-handler.md)