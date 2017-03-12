---
title: "How to: Combine Data with LINQ by Using Joins (Visual Basic) | Microsoft Docs"
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
  - "queries [LINQ in Visual Basic], joins"
  - "joins [LINQ in Visual Basic]"
  - "Join clause [LINQ in Visual Basic]"
  - "Group Join clause [Visual Basic]"
  - "joining [LINQ in Visual Basic]"
  - "queries [LINQ in Visual Basic], how-to topics"
ms.assetid: 5b00a478-035b-41c6-8918-be1a97728396
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# How to: Combine Data with LINQ by Using Joins (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Visual Basic fornisce le clausole query `Join` e `Group Join` per consentire di combinare i contenuti di più raccolte in base ai valori comuni tra le raccolte.  I valori sono noti come valori *chiave*.  Gli sviluppatori che hanno familiarità con concetti di database relazionale riconosceranno la clausola `Join` come un INNER JOIN e la clausola `Group Join` come un LEFT OUTER JOIN, in effetti.  
  
 Negli esempi di questo argomento vengono illustrate alcune modalità per combinare dati utilizzando le clausole query `Join` e `Group Join`.  
  
## Creare un progetto e aggiungere dati di esempio  
  
#### Per creare un progetto che contiene dati e tipi di esempio  
  
1.  Per eseguire gli esempi in questo argomento, aprire Visual Studio e aggiungere un nuovo progetto Applicazione console di Visual Basic.  Fare doppio clic sul file Module1.vb creato da Visual Basic.  
  
2.  Negli esempi di questo utilizzo dell'argomento vengono utilizzati i tipi e i dati `Person` e `Pet` dal seguente esempio di codice.  Copiare questo codice nel modulo `Module1` predefinito creato da Visual Basic.  
  
     [!code-vb[VbLINQHowTos#1](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/visualbasic/VbLINQHowTos/Module1.vb#1)]  
    [!code-vb[VbLINQHowTos#2](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/visualbasic/VbLINQHowTos/Module1.vb#2)]  
  
## Eseguire un Inner join utilizzando la clausola Join  
 Un INNER JOIN combina i dati da due raccolte.  Vengono inclusi gli elementi per i quali esiste la corrispondenza dei valori della chiave specificata .  Qualsiasi elemento da una qualsiasi raccolta che non ha un elemento corrispondente nell'altra raccolta viene escluso.  
  
 In Visual Basic, LINQ fornisce due opzioni per l'esecuzione di un INNER JOIN: un join implicito e un join esplicito.  
  
 Un join implicito specifica le raccolte da combinare in una clausola `From` e identifica i campi chiave di corrispondenza in una clausola `Where`.  Visual Basic implicitamente associa le due raccolte in base ai campi chiave specificati.  
  
 È possibile specificare un join esplicito utilizzando la clausola `Join` quando si vuole specificare quali campi chiave utilizzare nel join.  In questo caso, viene comunque utilizzata una clausola `Where` per filtrare i risultati della query.  
  
#### Per eseguire un Inner join utilizzando la clausola Join  
  
1.  Aggiungere il codice seguente al modulo `Module1` del progetto per vedere esempi di inner join sia implicito che esplicito.  
  
     [!code-vb[VbLINQHowTos#4](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/visualbasic/VbLINQHowTos/Module1.vb#4)]  
  
## Eseguire un Left outer join utilizzando la clausola Group join  
 Un LEFT OUTER JOIN include tutti gli elementi dalla raccolta di sinistra del join e solo i valori corrispondenti dalla raccolta di destra del join.  Qualsiasi elemento della raccolta di destra del join che non abbia un elemento corrispondente nella raccolta di sinistra viene escluso dal risultato della query.  
  
 La clausola `Group Join` esegue, in effetto, un LEFT OUTER JOIN.  La differenza tra quello che è in genere noto come LEFT OUTER JOIN e quello che restituisce la clausola `Group Join` è che la clausola `Group Join` raggruppa i risultati dalla raccolta di destra per ogni elemento della raccolta di sinistra.  In un database relazionale, un LEFT OUTER JOIN restituisce risultati non raggruppati in cui ogni elemento nel risultato della query contiene elementi corrispondenti da entrambe le raccolte del join.  In questo caso, gli elementi dalla raccolta di sinistra vengono ripetuti per ogni elemento corrispondente della raccolta di destra.  Completando la prossima procedura sarà possibile vedere un risultato di questo tipo.  
  
 È possibile recuperare i risultati di una query `Group Join` come risultato non raggruppato, estendendo la query in modo che restituisca un elemento per ogni risultato raggruppato della query.  Per effettuare questa operazione è necessario assicurarsi di eseguire la query sul metodo `DefaultIfEmpty` della raccolta raggruppata.  In tal modo si è certi che gli elementi della raccolta di sinistra del join vengano comunque inseriti nel risultato della query, anche se non hanno risultati corrispondenti nella raccolta di destra  È possibile aggiungere codice alla query per fornire un valore predefinito quando non esiste un valore corrispondente nella raccolta di destra del join.  
  
#### Per eseguire un Left outer join utilizzando la clausola Group join  
  
1.  Aggiungere il codice seguente al modulo `Module1` del progetto per vedere esempi di left outer join raggruppato e non raggruppato.  
  
     [!code-vb[VbLINQHowTos#3](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/visualbasic/VbLINQHowTos/Module1.vb#3)]  
  
## Eseguire un join utilizzando una chiave composta  
 È possibile utilizzare la parola chiave `And` in una clausola `Join` o `Group Join` per identificare più campi chiave da utilizzare quando si cercano le corrispondenze tra i valori delle raccolte da unire.  La parola chiave `And` specifica che tutti i campi chiave specificati devono corrispondere per gli elementi da unire.  
  
#### Per eseguire un join utilizzando una chiave composta  
  
1.  Aggiungere il codice seguente al modulo `Module1` nel progetto per visualizzare un esempio di join che utilizza una chiave composta.  
  
     [!code-vb[VbLINQHowTos#5](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/visualbasic/VbLINQHowTos/Module1.vb#5)]  
  
## Eseguire il codice.  
  
#### Aggiungere codice per eseguire gli esempi  
  
1.  Sostituire `Sub Main` nel modulo `Module1` nel progetto con il codice seguente per eseguire gli esempi descritti in questo argomento.  
  
     [!code-vb[VbLINQHowTos#6](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/visualbasic/VbLINQHowTos/Module1.vb#6)]  
  
2.  Premere F5 per eseguire gli esempi.  
  
## Vedere anche  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Join Clause](../../../../visual-basic/language-reference/queries/join-clause.md)   
 [Group Join Clause](../../../../visual-basic/language-reference/queries/group-join-clause.md)   
 [From Clause](../../../../visual-basic/language-reference/queries/from-clause.md)   
 [Where Clause](../../../../visual-basic/language-reference/queries/where-clause.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)   
 [Trasformazioni dati con LINQ \(C\#\)](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md)