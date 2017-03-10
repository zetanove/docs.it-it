---
title: "Relaxed Delegate Conversion (Visual Basic) | Microsoft Docs"
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
  - "relaxed delegate conversion [Visual Basic]"
  - "delegates [Visual Basic], relaxed conversion"
  - "conversions, relaxed delegate"
ms.assetid: 64f371d0-5416-4f65-b23b-adcbf556e81c
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Relaxed Delegate Conversion (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

La conversione di tipo relaxed del delegato consente di assegnare subroutine e funzioni a delegati o gestori anche quando le firme non sono identiche. Pertanto, l'associazione ai delegati diventa coerente con l'associazione già consentita nelle chiamate ai metodi.  
  
## Parametri e tipo restituito  
 Al posto della corrispondenza esatta delle firme, la conversione relaxed richiede il rispetto delle condizioni seguenti quando l'oggetto `Option Strict` è impostato su `On`:  
  
-   Una conversione verso un tipo di dati più grande è possibile dal tipo di dati di ogni parametro del delegato al tipo di dati del parametro corrispondente della funzione assegnata o `Sub`.  Nell'esempio seguente, il delegato `Del1` dispone di un parametro, ovvero di un oggetto `Integer`.  Il parametro `m` nelle espressioni lambda assegnate deve avere un tipo di dati per il quale vi sia una conversione verso un tipo di dati più grande da `Integer`, ad esempio `Long` o `Double`.  
  
     [!code-vb[VbVbalrRelaxedDelegates#1](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#1)]  
  
     [!code-vb[VbVbalrRelaxedDelegates#2](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#2)]  
  
     Le conversioni verso un tipo di dati più piccolo sono consentite solo quando `Option Strict` è impostato su `Off`.  
  
     [!code-vb[VbVbalrRelaxedDelegates#8](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module2.vb#8)]  
  
-   Una conversione verso un tipo di dati più grande è possibile nella direzione opposta dal tipo restituito della funzione assegnata o `Sub` al tipo restituito del delegato.  Negli esempi seguenti, il corpo di ogni espressione lambda assegnata deve restituire un tipo di dati che viene convertito verso il tipo più grande `Integer` poiché il tipo restituito dell'oggetto `del1` è `Integer`.  
  
     [!code-vb[VbVbalrRelaxedDelegates#3](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#3)]  
  
 Se `Option Strict` è impostato su `Off`, la restrizione per la conversione verso un tipo di dati più grande viene rimossa in entrambe le direzioni.  
  
 [!code-vb[VbVbalrRelaxedDelegates#4](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module2.vb#4)]  
  
## Omissione delle specifiche dei parametri  
 I delegati di tipo relaxed consentono inoltre di omettere completamente le specifiche dei parametri nel metodo assegnato:  
  
 [!code-vb[VbVbalrRelaxedDelegates#5](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#5)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#6](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#6)]  
  
 Tenere presente che non è possibile specificare alcuni parametri e ometterne altri.  
  
 [!code-vb[VbVbalrRelaxedDelegates#15](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#15)]  
  
 La possibilità di omettere i parametri è utile in una situazione quale la definizione di un gestore eventi, in cui sono implicati vari parametri complessi.  Gli argomenti per alcuni gestori eventi non sono utilizzati.  Invece, il gestore accede direttamente allo stato del controllo nel quale l'evento è registrato e ignora gli argomenti.  I delegati di tipo relaxed consentono di omettere gli argomenti in tali dichiarazioni quando non risultano ambiguità.  Nell'esempio seguente, il metodo `OnClick` pienamente specificato può essere riscritto come `RelaxedOnClick`.  
  
```vb#  
Sub OnClick(ByVal sender As Object, ByVal e As EventArgs) Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
  
Sub RelaxedOnClick() Handles b.Click  
    MessageBox.Show("Hello World from" + b.Text)  
End Sub  
```  
  
## Esempi di AddressOf  
 Le espressioni lambda vengono utilizzate negli esempi precedenti per rendere facilmente individuabili le relazioni dei tipi.  Tuttavia, le stesse conversioni di tipo relaxed sono consentite per le assegnazioni del delegato che utilizzano `AddressOf`, `Handles` o `AddHandler`.  
  
 Nell'esempio seguente le funzioni `f1`, `f2`, `f3` e `f4` possono essere tutte assegnate a `Del1`.  
  
 [!code-vb[VbVbalrRelaxedDelegates#1](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#1)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#7](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#7)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#9](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#9)]  
  
 L'esempio seguente è valido solo quando `Option Strict` è impostato su `Off`.  
  
 [!code-vb[VbVbalrRelaxedDelegates#14](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module2.vb#14)]  
  
## Eliminazione dei risultati delle funzioni  
 La conversione di tipo relaxed del delegato consente di assegnare una funzione a un delegato `Sub`, ignorando efficacemente il valore restituito della funzione.  Tuttavia, non è possibile assegnare una `Sub` a un delegato della funzione.  Nell'esempio seguente, l'indirizzo della funzione `doubler` viene assegnato al delegato `Sub` `Del3`.  
  
 [!code-vb[VbVbalrRelaxedDelegates#10](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#10)]  
  
 [!code-vb[VbVbalrRelaxedDelegates#11](../../../../visual-basic/programming-guide/language-features/delegates/codesnippet/visualbasic/VbVbalrRelaxedDelegates/Module1.vb#11)]  
  
## Vedere anche  
 [Lambda Expressions](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Delegates](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [How to: Pass Procedures to Another Procedure in Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)