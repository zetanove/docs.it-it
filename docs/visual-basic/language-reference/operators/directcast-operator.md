---
title: "DirectCast Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.directCast"
  - "directCast"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DirectCast keyword"
ms.assetid: 63e5a1d0-4d9e-4732-bf8f-e90c0c8784b8
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# DirectCast Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Introduce un'operazione di conversione dei tipi basata sull'ereditarietà o sull'implementazione.  
  
## Note  
 Per la conversione `DirectCast` non utilizza le routine di supporto di runtime di Visual Basic, per poter garantire prestazioni migliori rispetto a `CType` durante la conversione da e verso il tipo di dati `Object`.  
  
 È possibile utilizzare la parola chiave `DirectCast` analogamente a [Funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md) e alla parola chiave [TryCast Operator](../../../visual-basic/language-reference/operators/trycast-operator.md).  Viene specificata un'espressione come primo argomento e un tipo per la relativa conversione come secondo argomento.  `DirectCast` richiede una relazione di ereditarietà o di implementazione tra tipi di dati di due argomenti.  Ciò significa che un tipo deve ereditare dall'altro tipo o implementarlo.  
  
## Condizioni di errore  
 Se non viene rilevata alcuna relazione di ereditarietà o implementazione, `DirectCast` genera un errore del compilatore.  L'assenza di errori del compilatore non garantisce tuttavia la riuscita della conversione.  Se la conversione desiderata è verso un tipo di dati più piccolo, è possibile che l'operazione non riesca in fase di esecuzione.  In questo caso, il runtime genera un errore <xref:System.InvalidCastException>.  
  
## Parole chiave di conversione  
 Di seguito è riportato un confronto tra le parole chiave di conversione dei tipi.  
  
|||||  
|-|-|-|-|  
|Parola chiave|Tipi di dati|Relazione degli argomenti|Errore di runtime|  
|[Funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md)|Qualsiasi tipo di dati|La conversione verso un tipo di dati più grande o più piccolo deve essere definita tra i due tipi di dati|Genera <xref:System.InvalidCastException>|  
|`DirectCast`|Qualsiasi tipo di dati|Uno dei tipi deve ereditare dall'altro o implementarlo|Genera <xref:System.InvalidCastException>|  
|[TryCast Operator](../../../visual-basic/language-reference/operators/trycast-operator.md)|Solo tipi di riferimento|Uno dei tipi deve ereditare dall'altro o implementarlo|Restituisce [Nothing](../../../visual-basic/language-reference/nothing.md)|  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrati due utilizzi di `DirectCast`, uno con esito negativo in fase di esecuzione e un altro con esito positivo.  
  
 [!code-vb[VbVbalrKeywords#1](../../../visual-basic/language-reference/codesnippet/visualbasic/directcast-operator_1.vb)]  
  
 Nell'esempio precedente il tipo di runtime `q` è `Double`.  `CType` ha esito positivo perché è possibile convertire `Double` in `Integer`.  Tuttavia, il primo `DirectCast` ha esito negativo in fase di esecuzione poiché il tipo di `Double` in fase di esecuzione non presenta alcuna relazione di ereditarietà con `Integer`, anche in presenza di una conversione.  Il secondo `DirectCast` ha esito positivo poiché esegue la conversione dal tipo <xref:System.Windows.Forms.Form> al tipo <xref:System.Windows.Forms.Control>, dal quale <xref:System.Windows.Forms.Form> eredita.  
  
## Vedere anche  
 <xref:System.Convert.ChangeType%2A?displayProperty=fullName>   
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)