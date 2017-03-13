---
title: "How to: Call a Procedure That Returns a Value (Visual Basic) | Microsoft Docs"
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
  - "procedures, returning a value"
ms.assetid: a445127b-0f5f-465a-98fb-3e514b93d115
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# How to: Call a Procedure That Returns a Value (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine `Function` restituisce un valore al codice chiamante.  Per chiamarla, includerne il nome e gli argomenti nella parte destra di un'istruzione di assegnazione o in un'espressione.  
  
### Per chiamare una routine Function all'interno di un'espressione  
  
1.  Utilizzare il nome della routine `Function` come se fosse una variabile.  È possibile utilizzare una chiamata di routine `Function` dovunque sia consentito l'utilizzo di una variabile o di una costante in un'espressione.  
  
2.  Aggiungere le parentesi dopo il nome della routine per racchiudere l'elenco di argomenti.  Se non sono presenti argomenti, è possibile omettere le parentesi.  L'utilizzo delle parentesi, tuttavia, semplifica la lettura del codice.  
  
3.  Racchiudere gli argomenti dell'elenco tra parentesi, separati da virgole.  È importante indicarli nello stesso ordine in cui i parametri corrispondenti vengono definiti dalla routine `Function`.  
  
     In alternativa, è possibile passare uno o più argomenti in base al nome.  Per ulteriori informazioni, vedere [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md).  
  
4.  Il valore restituito dalla routine fa parte dell'espressione proprio come il valore di una variabile o di una costante.  
  
### Per chiamare una routine Function in un'istruzione di assegnazione  
  
1.  Utilizzare il nome della routine `Function` che segue il segno di uguale \(`=`\) nell'istruzione di assegnazione.  
  
2.  Aggiungere le parentesi dopo il nome della routine per racchiudere l'elenco di argomenti.  Se non sono presenti argomenti, è possibile omettere le parentesi.  L'utilizzo delle parentesi, tuttavia, semplifica la lettura del codice.  
  
3.  Racchiudere gli argomenti dell'elenco tra parentesi, separati da virgole.  È importante indicarli nello stesso ordine in cui i parametri corrispondenti vengono definiti dalla routine `Function`, a meno che non vengano passati in base al nome.  
  
4.  Il valore restituito dalla routine viene memorizzato nella variabile o nella proprietà a sinistra dell'istruzione di assegnazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene chiamata la <xref:Microsoft.VisualBasic.Interaction.Environ%2A> di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] per recuperare il valore di una variabile di ambiente del sistema operativo.  Nella prima riga `Environ` viene chiamato all'interno di un'espressione e nella seconda viene chiamato in un'istruzione di assegnazione.  `Environ` accetta il nome della variabile come unico argomento.  Il valore della variabile viene restituito al codice chiamante.  
  
 [!code-vb[VbVbcnProcedures#7](./codesnippet/VisualBasic/how-to-call-a-procedure-that-returns-a-value_1.vb)]  
  
## Vedere anche  
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [How to: Create a Procedure that Returns a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure-that-returns-a-value.md)   
 [How to: Return a Value from a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-return-a-value-from-a-procedure.md)   
 [How to: Call a Procedure that Does Not Return a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-does-not-return-a-value.md)