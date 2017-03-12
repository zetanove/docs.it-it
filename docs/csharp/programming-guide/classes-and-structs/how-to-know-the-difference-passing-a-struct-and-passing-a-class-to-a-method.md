---
title: "Procedura: differenza tra il passaggio a un metodo di uno struct e di un riferimento a una classe (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "metodi [C#], passaggio di classi e struct"
  - "passaggio di parametri [C#], struct e classi"
  - "struct [C#], passaggio come parametro di metodo"
ms.assetid: 9c1313a6-32a8-4ea7-a59f-450f66af628b
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 25
---
# Procedura: differenza tra il passaggio a un metodo di uno struct e di un riferimento a una classe (Guida per programmatori C#)
In l ' esempio seguente viene illustrato come passare [struttura](../../../csharp/language-reference/keywords/struct.md) a un metodo differisce da passare un'istanza di [classe](../../../csharp/language-reference/keywords/class.md) a un metodo.  In l ' esempio, entrambi gli argomenti \(struct e istanza della classe\) vengono passati con valore ed entrambi i metodi modificano il valore di un campo dell' argomento.  Tuttavia, i risultati di due metodi non sono identici in quanto ciò che vengono passati quando si passa una struttura è diverso rispetto a quello passato quando si passa un'istanza di una classe.  
  
 Poiché una struttura è [tipo di valore](../../../csharp/language-reference/keywords/value-types.md), quando [passare una struttura per valore](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md) a un metodo, il metodo segnala e intervenire una copia dell' argomento della struttura.  Il metodo non dispone di accesso alla struttura originale nel metodo di chiamata e pertanto non può essere modificato in qualsiasi modo.  Il metodo può modificare solo la copia.  
  
 L'istanza della classe è [tipo di riferimento](../../../csharp/language-reference/keywords/reference-types.md), non un tipo di valore.  Quando [un tipo riferimento viene passato per valore](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md) a un metodo, il metodo riceve una copia del riferimento all' istanza della classe.  Ovvero il metodo riceve una copia dell' indirizzo dell' istanza, non una copia dell' istanza stessa.  L'istanza della classe nel metodo di chiamata a un indirizzo, il parametro nel metodo chiamato è una copia dell' indirizzo ed entrambi gli indirizzi si riferiscono allo stesso oggetto.  Poiché il parametro contiene solo una copia dell' indirizzo, il metodo chiamato non può modificare l'indirizzo dell' istanza della classe nel metodo di chiamata.  Tuttavia, il metodo chiamato possibile utilizzare l'indirizzo per accedere ai membri della classe che sia l'indirizzo originale e la copia fanno riferimento.  Se il metodo chiamato modifica un membro di classe, l'istanza della classe originale del metodo di chiamata delle modifiche anche.  
  
 L'output dell' esempio seguente viene illustrata la differenza.  Il valore del campo di `willIChange` dell' istanza della classe viene modificato dalla chiamata al metodo `ClassTaker` perché il metodo utilizza l'indirizzo nel parametro per trovare il campo specificato dall' istanza della classe.  Il campo di `willIChange` della struttura nel metodo di chiamata non viene modificato dalla chiamata al metodo `StructTaker` perché il valore dell' argomento è una copia della struttura stessa, non una copia del relativo indirizzo.  `StructTaker` modifica la copia e la copia viene persa durante la chiamata a `StructTaker` viene completata.  
  
## Esempio  
 [!code-cs[csProgGuideObjects#32](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-know-the-differen_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)   
 [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md)   
 [Passaggio di parametri](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)