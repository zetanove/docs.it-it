---
title: "Passaggio di parametri di tipi di riferimento (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "parametri di metodo [C#], tipi di riferimento"
  - "parametri [C#], riferimento"
ms.assetid: 9e6eb65c-942e-48ab-920a-b7ba9df4ea20
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Passaggio di parametri di tipi di riferimento (Guida per programmatori C#)
Una variabile di un [tipo che rappresenta un riferimento](../../../csharp/language-reference/keywords/reference-types.md) non contiene direttamente dati, ma solo un riferimento a essi.  Quando si passa un parametro associato a un tipo che rappresenta un riferimento per valore, è possibile modificare i dati associati al riferimento, ad esempio il valore del membro di una classe.  Non è tuttavia possibile modificare il valore del riferimento stesso, ovvero non è possibile utilizzare tale riferimento per allocare memoria per una nuova classe e fare in modo che sia persistente anche all'esterno del blocco.  In questo caso, è necessario passare il parametro utilizzando la parola chiave [ref](../../../csharp/language-reference/keywords/ref.md) o [out](../../../csharp/language-reference/keywords/out.md).  Per semplicità, negli esempi che seguono viene utilizzata solo la parola chiave `ref`.  
  
## Passaggio di tipi riferimento per valore  
 Nell'esempio che segue viene illustrato il passaggio per valore del parametro associato a un tipo che rappresenta un riferimento `arr` al metodo `Change`.  Poiché il parametro è un riferimento a `arr`, è possibile modificare il valore degli elementi della matrice.  Il tentativo di riassegnare il parametro a una diversa posizione in memoria, tuttavia, è efficace solo all'interno del metodo e non ha alcun effetto sulla variabile originale `arr`.  
  
 [!code-cs[csProgGuideParameters#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-reference-type-p_1.cs)]  
  
 Nell'esempio precedente la matrice `arr`, la quale rappresenta un tipo di riferimento, viene passata al metodo senza il parametro `ref`.  In questo caso al metodo viene passata una copia del riferimento che punta a `arr`.  L'output indica che il metodo ha la possibilità di modificare il contenuto di un elemento della matrice \(da `1` a `888`\).  L'allocazione di una nuova porzione di memoria utilizzando l'operatore [new](../../../csharp/language-reference/keywords/new.md) nel metodo `Change`, tuttavia, fa sì che la variabile `pArray` faccia riferimento a una nuova matrice.  In questo modo eventuali modifiche successive non avranno effetto sulla matrice originale, `arr`, creata in `Main`.  In effetti, in questo esempio vengono create due matrici: una in `Main` e una nel metodo `Change`.  
  
## Passaggio di tipi riferimento per riferimento  
 L'esempio seguente è lo stesso dell'esempio precedente, tranne per il fatto che `ref` la parola chiave viene aggiunto all'intestazione e alla chiamata di metodo.  Tutte le modifiche che hanno luogo presenti in riportate metodo della variabile originale nel programma chiamante.  
  
 [!code-cs[csProgGuideParameters#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-reference-type-p_2.cs)]  
  
 Tutte le modifiche apportate all'interno del metodo hanno effetto sulla matrice originale in `Main`.  In effetti, la matrice originale viene riallocata mediante l'operatore `new`.  Dopo la chiamata al metodo `Change`, pertanto, i riferimenti a `arr` puntano alla matrice a cinque elementi creata nel metodo `Change`.  
  
## Scambio di due stringhe  
 Lo scambio di stringhe è un buon esempio di passaggio di parametri associati a tipi che rappresentano un riferimento per riferimento.  In questo esempio due stringhe, `str1` e `str2`, vengono inizializzate in `Main` e passate al metodo `SwapStrings` come parametri modificati dalla parola chiave `ref`.  Le due stringhe vengono scambiate all'interno del metodo e all'interno di `Main`.  
  
 [!code-cs[csProgGuideParameters#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-reference-type-p_3.cs)]  
  
 In questo esempio è necessario passare i parametri per riferimento perché abbiano effetto sulle variabili del programma chiamante.  Se si rimuove la parola chiave `ref` sia dall'intestazione del metodo che dalla chiamata al metodo, nel programma chiamante non avrà luogo alcuna modifica.  
  
 Per ulteriori informazioni sulle stringhe, vedere [stringa](../../../csharp/language-reference/keywords/string.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Passaggio di parametri](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [Passaggio di matrici mediante ref e out](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)   
 [ref](../../../csharp/language-reference/keywords/ref.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)