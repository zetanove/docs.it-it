---
title: "Nothing (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Nothing"
  - "vb.Nothing"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Nothing keyword"
  - "Nothing keyword, syntax"
ms.assetid: 06176e2d-bbf7-4a37-afaa-a86ad21ee99f
caps.latest.revision: 31
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 31
---
# Nothing (Visual Basic)
[!INCLUDE[vs2017banner](../../visual-basic/developing-apps/includes/vs2017banner.md)]

Rappresenta il valore predefinito di qualsiasi tipo di dati.  Per i tipi di riferimento, il valore predefinito è `null` riferimento.  Per i tipi di valore, il valore predefinito varia a seconda che il tipo di valore è nullable.  
  
> [!NOTE]
>  Per i tipi di valore non nullable, `Nothing` in Visual Basic differisce da  `null` in c\#.  In Visual Basic, se si imposta una variabile di un tipo di valore non nullable a `Nothing`, la variabile è impostata sul valore predefinito per il suo tipo dichiarato.  In c\#, se si assegna una variabile di un tipo di valore non nullable a `null`, un errore in fase di compilazione si verifica.  
  
## Note  
 `Nothing` rappresenta il valore predefinito di un tipo di dati.  Il valore predefinito varia a seconda che la variabile è di un tipo di valore o di un tipo di riferimento.  
  
 Una variabile di un oggetto *tipo di valore* contiene direttamente il valore.  I tipi di valore sono inclusi tutti i tipi di dati numerici, `Boolean`,  `Char`,  `Date`, tutte le strutture e le enumerazioni.  Una variabile di un oggetto *tipo di riferimento* archivia un riferimento a un'istanza di oggetto in memoria.  I tipi di riferimento sono incluse le classi, le matrici, delegati e stringhe.  Per ulteriori informazioni, vedere [Value Types and Reference Types](../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md).  
  
 Se una variabile è di tipo valore, il comportamento di `Nothing` varia a seconda che la variabile è di un tipo di dati nullable.  Per rappresentare un tipo di valore nullable, aggiungere un oggetto `?` modificatore al nome del tipo.  assegnare `Nothing` le nullable una variabile imposta il valore su  `null`.  Per ulteriori informazioni ed esempi, vedere [Nullable Value Types](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md).  
  
 se una variabile è di un tipo di valore che non è nullable, assegnare `Nothing` lo impostato il valore predefinito per il tipo dichiarato.  Se nel tipo si trovano membri variabili, questi vengono tutti impostati ai valori predefiniti corrispondenti.  Questo comportamento viene illustrato nell'esempio seguente per i tipi scalari.  
  
 [!code-vb[VbVbalrKeywords#7](../../visual-basic/language-reference/codesnippet/visualbasic/nothing_1.vb)]  
  
 Se una variabile è di tipo riferimento, assegnare `Nothing` per impostare variabili a un oggetto  `null` riferimento del tipo della variabile.  Una variabile che è impostata su `null` il riferimento non associato ad alcun oggetto.  Nell'esempio che segue viene illustrato quanto descritto.  
  
 [!code-vb[VbVbalrKeywords#8](../../visual-basic/language-reference/codesnippet/visualbasic/nothing_2.vb)]  
  
 Nel controllare se tipo di valore NULL o di riferimento\) una variabile sia `null`, non utilizzare  `= Nothing` o  `<> Nothing`.  Utilizzare sempre `Is Nothing` o  `IsNot Nothing`.  
  
 Per le stringhe in Visual Basic, equals di stringa vuota `Nothing`.  di conseguenza, `"" = Nothing` è true.  
  
 Nell'esempio seguente vengono illustrati confronti in cui vengono utilizzati gli operatori `Is` e `IsNot`.  
  
 [!code-vb[VbVbalrKeywords#9](../../visual-basic/language-reference/codesnippet/visualbasic/nothing_3.vb)]  
  
 Se si dichiara una variabile senza utilizzare una clausola `As` e la si imposta su `Nothing`, la variabile dispone di un tipo di `Object`.  Un esempio è `Dim something = Nothing`.  Un errore in fase di compilazione si verifica in questo caso `Option Strict` è attivato e  `Option Infer` è disattivato.  
  
 Quando si assegna la parola chiave `Nothing` a una variabile oggetto, tale variabile non farà più riferimento all'istanza di un oggetto.  Se in precedenza la variabile ha fatto riferimento a un'istanza, l'istanza non viene automaticamente terminata quando si imposta la variabile su `Nothing`.  L'istanza viene terminata e le risorse di memoria e di sistema associate a essa vengono rilasciate solo quando il Garbage Collector non rileva più riferimenti attivi.  
  
 `Nothing` è diverso da  <xref:System.DBNull> oggetto, che rappresenta una variante non inizializzate o una colonna inesistente del database.  
  
## Vedere anche  
 [Dim Statement](../../visual-basic/language-reference/statements/dim-statement.md)   
 [Object Lifetime: How Objects Are Created and Destroyed](../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)   
 [Lifetime in Visual Basic](../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Is Operator](../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot Operator](../../visual-basic/language-reference/operators/isnot-operator.md)   
 [Nullable Value Types](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)