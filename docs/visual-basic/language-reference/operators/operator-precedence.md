---
title: "Operator Precedence in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "arithmetic operators, precedence"
  - "operator precedence"
  - "logical operators, precedence"
  - "operators [Visual Basic], associativity"
  - "operators [Visual Basic], resolution"
  - "associativity of operators"
  - "operators [Visual Basic], precedence"
  - "precedence, of operators"
  - "comparison operators, precedence"
  - "math operators"
  - "order of precedence"
ms.assetid: cbbdb282-f572-458e-a520-008a675f8063
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Operator Precedence in Visual Basic
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando in un'espressione vengono eseguite varie operazioni, ciascuna di esse viene valutata e risolta in base a un ordine preciso definito *precedenza tra gli operatori*.  
  
## Regole di precedenza  
 Se le espressioni contengono operatori appartenenti a più categorie, la valutazione degli operatori seguirà le regole indicate più avanti:  
  
-   Gli operatori aritmetici e di concatenazione seguono l'ordine di precedenza descritto nella sezione seguente e vengono tutti elaborati prima degli operatori bit per bit, logici e di confronto.  
  
-   Tutti gli operatori di confronto hanno la stessa precedenza e vengono elaborati prima degli operatori logici e bit per bit ma dopo gli operatori aritmetici e di concatenazione.  
  
-   Gli operatori logici e bit per bit seguono l'ordine di precedenza descritto nella sezione seguente e vengono tutti elaborati dopo gli operatori aritmetici, di concatenazione e di confronto.  
  
-   Gli operatori con la stessa precedenza vengono valutati da sinistra a destra nell'ordine in cui appaiono nell'espressione.  
  
## Ordine di precedenza  
 Gli operatori seguono l'ordine di precedenza riportato di seguito:  
  
### Attendere l'operatore  
 Await  
  
### Operatori aritmetici e di concatenazione  
 Elevamento a potenza \(`^`\)  
  
 Identità e negazione unarie \(`+`, `–`\)  
  
 Moltiplicazione e divisione a virgola mobile \(`*`, `/`\)  
  
 Divisione di valori integer \(`\`\)  
  
 Modulo aritmetico \(`Mod`\)  
  
 Aggiunta e meno \(`+`, `–`\)  
  
 Concatenazione di stringhe \(`&`\)  
  
 Spostamento di bit aritmetico \(`<<`, `>>`\)  
  
### Operatori di confronto  
 Tutti gli operatori di confronto \(`=`, `<>`, `<`, `<=`, `>`, `>=`, `Is`, `IsNot`, `Like`, `TypeOf`...`Is`\)  
  
### Operatori logici e bit per bit  
 Negazione \(`Not`\)  
  
 Congiunzione \(`And`, `AndAlso`\)  
  
 Disgiunzione inclusiva \(`Or`, `OrElse`\)  
  
 Disgiunzione esclusiva \(`Xor`\)  
  
### Commenti  
 L'operatore di confronto `=` è solo un operatore di uguaglianza, non di assegnazione.  
  
 L'operatore di concatenazione di stringhe \(`&`\) non è un operatore aritmetico, ma per quanto riguarda l'ordine di precedenza viene raggruppato con gli operatori aritmetici.  
  
 Gli operatori `Is` e `IsNot` sono operatori di confronto per riferimenti a oggetti  con i quali non si eseguono confronti tra i valori di due oggetti, ma solo verifiche per stabilire se due variabili oggetto sono relative alla stessa istanza di oggetto.  
  
## Associazione  
 Se un'espressione contiene operatori con la stessa precedenza, ad esempio una moltiplicazione e una divisione, ciascuna operazione viene valutata dal compilatore da sinistra a destra nell'ordine in cui è rilevata.  Questa condizione è illustrata nell'esempio che segue.  
  
```  
Dim n1 As Integer = 96 / 8 / 4  
Dim n2 As Integer = (96 / 8) / 4  
Dim n3 As Integer = 96 / (8 / 4)  
```  
  
 La prima espressione valuta la divisione 96 \/ 8, che restituisce 12, e quindi la divisione 12 \/ 4, che restituisce 3.  Perché il compilatore valuta da sinistra verso destra le operazioni per `n1`, la valutazione è la stessa quando quell'ordine è indicato in modo esplicito per `n2`.  Sia `n1` che `n2` avranno come risultato 3.  Il risultato di `n3` sarà invece 48, in quanto le parentesi forzano il compilatore a valutare prima 8 \/ 4.  
  
 Tale comportamento fa sì che in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli operatori vengano definiti *associativi a sinistra*.  
  
## Modifica della precedenza e dell'associazione  
 Per fare in modo che alcune parti di un'espressione vengano calcolate prima di altre, è possibile racchiuderle tra parentesi.  In questo modo è possibile eseguire l'override sia dell'ordine di precedenza che dell'associazione a sinistra.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] esegue sempre le operazioni che sono racchiuse tra parentesi prima di quelle a. Tuttavia, all'interno delle parentesi, gestiscono la precedenza normale e l'associazione, a meno che non si utilizzi le parentesi tra parentesi.  Questa condizione è illustrata nell'esempio che segue.  
  
```  
Dim a, b, c, d, e, f, g As Double  
a = 8.0  
b = 3.0  
c = 4.0  
d = 2.0  
e = 1.0  
f = a - b + c / d * e  
' The preceding line sets f to 7.0. Because of natural operator   
' precedence and associativity, it is exactly equivalent to the   
' following line.  
f = (a - b) + ((c / d) * e)  
' The following line overrides the natural operator precedence   
' and left associativity.  
g = (a - (b + c)) / (d * e)  
' The preceding line sets g to 0.5.  
```  
  
## Vedere anche  
 [\= Operator](../../../visual-basic/language-reference/operators/assignment-operator.md)   
 [Is Operator](../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot Operator](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [Like Operator](../../../visual-basic/language-reference/operators/like-operator.md)   
 [TypeOf Operator](../../../visual-basic/language-reference/operators/typeof-operator.md)   
 [Await Operator](../../../visual-basic/language-reference/operators/await-operator.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)