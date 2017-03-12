---
title: "MustInherit (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "MustInherit"
  - "vb.MustInherit"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "classes [Visual Basic], abstract"
  - "MustInherit classes, MustInherit keyword"
  - "abstract classes, MustInherit class"
  - "MustInherit keyword"
ms.assetid: b8f05185-90e3-4dd7-adc2-90d852fab5b4
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# MustInherit (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che una classe può essere utilizzata solo come classe base da cui non è possibile creare direttamente un oggetto.  
  
## Note  
 Lo scopo di una *classe base*, nota anche come *classe astratta*, è di definire la funzionalità comune a tutte le classi da essa derivate,  con il vantaggio per le classi derivate di non dover ridefinire gli elementi comuni.  In alcuni casi la funzionalità condivisa non è sufficientemente completa da creare un oggetto utilizzabile e ogni classe derivata definisce la funzionalità mancante.  In una situazione del genere il codice utilizzato deve creare oggetti solo dalle classi derivate.  Utilizzare `MustInherit` sulla classe base per attivare la procedura.  
  
 Un altro impiego di una classe `MustInherit` consiste nel limitare una variabile a un insieme di classi correlate.  È possibile definire una classe base da cui derivare tutte le classi correlate.  La classe base non deve fornire alcuna funzionalità comune a tutte le classi derivate, ma può essere utilizzata come filtro per l'assegnazione di valori alle variabili.  Se il codice utilizzato dichiara una variabile come classe base, in Visual Basic sarà possibile assegnare alla variabile solo un oggetto di una delle classi derivate.  
  
 In .NET Framework vengono definite diverse classi `MustInherit`, tra cui <xref:System.Array>, <xref:System.Enum> e <xref:System.ValueType>.  <xref:System.ValueType> è un esempio di classe di base che limita una variabile.  Tutti i tipi di valore derivano da <xref:System.ValueType>.  Se si dichiara una variabile come <xref:System.ValueType>, è possibile assegnare solo tipi di valore a quella variabile.  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile utilizzare `MustInherit` solo in un'istruzione `Class`.  
  
-   **Modificatori combinati.** Non è possibile specificare `MustInherit` insieme a `NotInheritable` nella stessa dichiarazione.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrati l'ereditarietà forzata e l'override forzato.  La classe base `shape` definisce una variabile `acrossLine`.  Le classi `circle` e `square` derivano da `shape`.  Ereditano la definizione di `acrossLine`, ma devono definire la funzione `area` in quanto il calcolo varia in base al tipo di forma.  
  
 [!code-vb[VbVbalrKeywords#2](../../../visual-basic/language-reference/codesnippet/visualbasic/mustinherit_1.vb)]  
  
 È possibile dichiarare le variabili `shape1` e `shape2` di tipo `shape`.  Non è tuttavia possibile creare un oggetto da `shape` in quanto non dispone della funzionalità della funzione `area` ed è contrassegnato con `MustInherit`.  
  
 Dal momento che sono dichiarate come `shape`, le variabili `shape1` e `shape2` sono limitate a oggetti delle classi derivate `circle` e `square`.  In Visual Basic non è consentita l'assegnazione di qualsiasi altro oggetto a tali variabili, con evidenti vantaggi in termini di indipendenza dai tipi.  
  
## Utilizzo  
 Il modificatore `MustInherit` può essere utilizzato in questo contesto:  
  
 [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
## Vedere anche  
 [Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)