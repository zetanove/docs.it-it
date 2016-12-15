---
title: "TryCast Operator (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.trycast"
  - "trycast"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "TryCast keyword"
ms.assetid: d1ef5d47-fef4-491e-b014-1d910628f65c
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# TryCast Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Introduce un'operazione di conversione dei tipi che non genera un'eccezione.  
  
## Note  
 Se non riesce un tentativo di conversione, `CType` e `DirectCast` generano entrambi un errore <xref:System.InvalidCastException> Ciò può influire negativamente sulle prestazioni dell'applicazione.  `TryCast` restituisce [Nothing](../../../visual-basic/language-reference/nothing.md). Pertanto, anziché gestire una possibile eccezione, sarà sufficiente testare il risultato restituito rispetto a `Nothing`.  
  
 L'uso della parola chiave `TryCast` è analogo a quello della funzione [Funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md) e della parola chiave [DirectCast Operator](../../../visual-basic/language-reference/operators/directcast-operator.md).  Viene specificata un'espressione come primo argomento e un tipo per la relativa conversione come secondo argomento.  `TryCast` opera solo sui tipi di riferimento, quali classi e interfacce.  e richiede una relazione di ereditarietà o di implementazione tra i due tipi.  Ciò significa che un tipo deve ereditare dall'altro tipo o implementarlo.  
  
## Condizioni di errore  
 Se non viene rilevata alcuna relazione di ereditarietà o implementazione, `TryCast` genera un errore del compilatore.  L'assenza di errori del compilatore non garantisce tuttavia la riuscita della conversione.  Se la conversione desiderata è verso un tipo di dati più piccolo, è possibile che l'operazione non riesca in fase di esecuzione.  In tal caso, `TryCast` restituisce [Nothing](../../../visual-basic/language-reference/nothing.md).  
  
## Parole chiave di conversione  
 Di seguito è riportato un confronto tra le parole chiave di conversione dei tipi.  
  
|||||  
|-|-|-|-|  
|Parola chiave|Tipi di dati|Relazione degli argomenti|Errore di runtime|  
|[Funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md)|Qualsiasi tipo di dati|La conversione verso un tipo di dati più grande o più piccolo deve essere definita tra i due tipi di dati|Genera <xref:System.InvalidCastException>|  
|[DirectCast Operator](../../../visual-basic/language-reference/operators/directcast-operator.md)|Qualsiasi tipo di dati|Uno dei tipi deve ereditare dall'altro o implementarlo|Genera <xref:System.InvalidCastException>|  
|`TryCast`|Solo tipi di riferimento|Uno dei tipi deve ereditare dall'altro o implementarlo|Restituisce [Nothing](../../../visual-basic/language-reference/nothing.md)|  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo di `TryCast`.  
  
 [!code-vb[VbVbalrKeywords#6](../../../visual-basic/language-reference/codesnippet/VisualBasic/trycast-operator_1.vb)]  
  
## Vedere anche  
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)