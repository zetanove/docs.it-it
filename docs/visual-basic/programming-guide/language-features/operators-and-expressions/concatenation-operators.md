---
title: "Concatenation Operators in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "& operator [Visual Basic], concatenation"
  - "concatenation operators"
  - "operators [Visual Basic], concatenation"
  - "Visual Basic code, operators"
  - "+ operator [Visual Basic], concatenation"
  - "concatenation operators, Visual Basic strings"
ms.assetid: e59908c3-89e0-41ae-933d-3e8826c16a04
caps.latest.revision: 18
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Concatenation Operators in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Gli operatori di concatenazione consentono di unire più stringhe in un'unica stringa.  Sono disponibili due operatori di concatenazione: `+` e `&`.  Entrambi eseguono operazioni di concatenazione di base, come illustrato nell'esempio seguente.  
  
 [!CODE [Dim x As String = "Mic" & "ro" & "soft" Dim y As String = "Mic" + "ro" + "soft" ' The preceding statements set both x and y to "Microsoft".](Dim x As String = "Mic" & "ro" & "soft" Dim y As String = "Mic" + "ro" + "soft" ' The preceding statements set both x and y to "Microsoft".)]  
  
 Questi operatori possono concatenare anche variabili di tipo `String`, come nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators#76](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/concatenation-operators_1.vb)]  
  
## Differenze tra i due operatori di concatenazione  
 Lo scopo primario dell'[\+ Operator](../../../../visual-basic/language-reference/operators/addition-operator.md) consiste nell'aggiungere due numeri.  Questo operatore consente però anche di concatenare operandi numerici con operandi stringa.  L'operatore `+` include un insieme complesso di regole che determinano se aggiungere, concatenare, segnalare un errore del compilatore oppure generare un'eccezione <xref:System.InvalidCastException> in fase di esecuzione.  
  
 L'[& Operator](../../../../visual-basic/language-reference/operators/concatenation-operator.md) viene definito solo per gli operandi `String` e amplia sempre i propri operandi in `String`, indipendentemente dall'impostazione di `Option Strict`.  L'operatore `&` rappresenta la scelta consigliata per la concatenazione delle stringhe poiché viene definito solo per le stringhe e riduce la possibilità di generare conversioni non intenzionali.  
  
## Prestazioni: String e StringBuilder  
 Se una stringa subisce numerose manipolazioni, ad esempio concatenazioni, eliminazioni e sostituzioni, l'uso della classe <xref:System.Text.StringBuilder> nello spazio dei nomi <xref:System.Text> può migliorare le prestazioni.  Questa classe richiede un'istruzione aggiuntiva per la creazione e l'inizializzazione di un oggetto <xref:System.Text.StringBuilder> e un'altra istruzione per la conversione del relativo valore finale in `String`, ma in questo caso è possibile eseguire il ripristino perché l'esecuzione di <xref:System.Text.StringBuilder> è più veloce.  
  
## Vedere anche  
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Types of String Manipulation Methods in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/types-of-string-manipulation-methods.md)   
 [Arithmetic Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Comparison Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)