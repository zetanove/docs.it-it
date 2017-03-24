---
title: "Matrici unidimensionali (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici [C#], unidimensionali"
  - "matrici unidimensionali [C#]"
ms.assetid: 2cec1196-1de0-49d2-baf2-c607c33310e8
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Matrici unidimensionali (Guida per programmatori C#)
È possibile dichiarare una matrice unidimensionale composta da cinque interi, come illustrato nell'esempio che segue:  
  
 [!code-cs[csProgGuideArrays#4](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_1.cs)]  
  
 Questa matrice contiene gli elementi da `array[0]` a `array[4]` compresi.  L'operatore [new](../../../csharp/language-reference/keywords/new.md) viene utilizzato per creare la matrice e inizializzarne gli elementi con i corrispondenti valori predefiniti.  In questo esempio tutti gli elementi della matrice sono inizializzati a zero.  
  
 Allo stesso modo è possibile dichiarare una matrice contenente elementi stringa.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideArrays#5](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_2.cs)]  
  
## Inizializzazione di una matrice  
 È possibile inizializzare una matrice al momento della dichiarazione, nel qual caso non è necessario specificarne il numero di dimensioni, in quanto è già fornito dal numero di elementi presente nell'elenco di inizializzazione.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideArrays#6](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_3.cs)]  
  
 Allo stesso modo, è possibile inizializzare una matrice di stringhe.  Di seguito è illustrata la dichiarazione di una matrice di stringhe in cui ciascun elemento della matrice è inizializzato con il nome di un giorno della settimana:  
  
 [!code-cs[csProgGuideArrays#7](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_4.cs)]  
  
 Quando si inizializza una matrice al momento della dichiarazione, è possibile utilizzare le seguenti abbreviazioni:  
  
 [!code-cs[csProgGuideArrays#8](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_5.cs)]  
  
 È possibile dichiarare una variabile di matrice senza inizializzazione, ma sarà necessario utilizzare l'operatore `new` quando si assegna una matrice a questa variabile.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideArrays#9](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_6.cs)]  
  
 In C\# 3.0 vengono introdotte le matrici tipizzate in modo implicito.  Per ulteriori informazioni, vedere [Matrici tipizzate in modo implicito](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md).  
  
## Matrici di tipo valore e di tipo riferimento  
 Si consideri la seguente dichiarazione di matrice:  
  
 [!code-cs[csProgGuideArrays#10](../../../csharp/programming-guide/arrays/codesnippet/CSharp/single-dimensional-arrays_7.cs)]  
  
 Il risultato di questa istruzione è diverso a seconda che `SomeType` sia un tipo di valore o un tipo di riferimento.  Se si tratta di un tipo valore, l'istruzione crea una matrice di 10 elementi, ciascuno del tipo `SomeType`.  Se `SomeType` è un tipo di riferimento, l'istruzione creerà una matrice di 10 elementi, ciascuno dei quali verrà inizializzato con un riferimento a null.  
  
 Per ulteriori informazioni sui tipi valore e sui tipi riferimento, vedere [Tipi](../../../csharp/language-reference/keywords/types.md).  
  
## Vedere anche  
 <xref:System.Array>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Matrici multidimensionali](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)   
 [Matrici irregolari](../../../csharp/programming-guide/arrays/jagged-arrays.md)