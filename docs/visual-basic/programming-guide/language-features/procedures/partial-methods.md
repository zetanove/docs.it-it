---
title: "Partial Methods (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.PartialMethod"
  - "PartialMethod"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "custom logic into code [Visual Basic]"
  - "partial methods [Visual Basic]"
  - "partial, methods [Visual Basic]"
  - "methods [Visual Basic], partial methods"
  - "inserting custom logic into code"
ms.assetid: 74b3368b-b348-44a0-a326-7d7dc646f4e9
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Partial Methods (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

I metodi parziali consentono agli sviluppatori di inserire una logica personalizzata nel codice.  In genere, il codice è parte di una classe generata nella finestra di progettazione.  I metodi parziali vengono definiti in una classe parziale creata da un generatore di codice e si utilizzano comunemente per notificare che si è verificata qualche modifica.  Consentono allo sviluppatore di specificare un comportamento personalizzato in funzione della modifica.  
  
 La finestra di progettazione del generatore di codice definisce solo la firma del metodo e una o più chiamate al metodo.  Gli sviluppatori possono fornire le implementazioni per il metodo se desiderano personalizzare il comportamento del codice generato.  Quando non viene fornita alcuna implementazione, le chiamate al metodo vengono rimosse dal compilatore, per evitare un ulteriore sovraccarico nelle prestazioni.  
  
## Dichiarazione  
 Il codice generato contrassegna la definizione di un metodo parziale posizionando la parola chiave `Partial` all'inizio della riga della firma.  
  
```vb#  
Partial Private Sub QuantityChanged()  
End Sub  
```  
  
 La definizione deve soddisfare le seguenti condizioni:  
  
-   Il metodo deve essere un `Sub`, non una `Function`.  
  
-   Il corpo del metodo deve essere lasciato vuoto.  
  
-   Il modificatore di accesso deve essere `Private`.  
  
## Implementazione  
 L'implementazione consiste principalmente nell'inserire il corpo del metodo parziale.  L'implementazione è in genere in una classe parziale separata dalla definizione e è scritta da un sviluppatore che desidera estendere il codice generato.  
  
```vb#  
Private Sub QuantityChanged()  
'    Code for executing the desired action.  
End Sub  
```  
  
 Nell'esempio precedente viene esattamente duplicata la firma nella dichiarazione, ma sono possibili variazioni.  In particolare, è possibile aggiungere altri modificatori, ad esempio `Overloads` o `Overrides`.  È consentito un solo modificatore `Overrides`.  Per ulteriori informazioni sui modificatori di metodo, vedere [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md).  
  
## Utilizzare  
 Si chiama un metodo parziale come si chiamerebbe qualsiasi altra procedura `Sub`.  Se il metodo è stato implementato, gli argomenti vengono valutati e viene eseguito il corpo del metodo.  Tuttavia,occorre ricordare che l'implementazione di un metodo parziale è facoltativa.  Se il metodo non viene implementato, una chiamata non ha effetto e le espressioni passate come argomenti al metodo non vengono valutate.  
  
## Esempio  
 In un file denominato Product.Designer.vb, definire una classe `Product` che ha una proprietà `Quantity`.  
  
 [!code-vb[VbVbalrPartialMeths#4](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/partial-methods_1.vb)]  
  
 In un file denominato Product.vb, fornire un'implementazione per `QuantityChanged`.  
  
 [!code-vb[VbVbalrPartialMeths#5](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/partial-methods_2.vb)]  
  
 Infine, nel metodo Main di un progetto, dichiarare un'istanza `Product` e fornire un valore iniziale per la relativa proprietà `Quantity`.  
  
 [!code-vb[VbVbalrPartialMeths#6](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/partial-methods_3.vb)]  
  
 Comparirà una finestra che visualizza questo messaggio:  
  
 `Quantity was changed to 100`  
  
## Vedere anche  
 [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Partial](../../../../visual-basic/language-reference/modifiers/partial.md)   
 [Generazione di codice in LINQ to SQL](../Topic/Code%20Generation%20in%20LINQ%20to%20SQL.md)   
 [Aggiunta della logica di business utilizzando i metodi parziali](../Topic/Adding%20Business%20Logic%20By%20Using%20Partial%20Methods.md)