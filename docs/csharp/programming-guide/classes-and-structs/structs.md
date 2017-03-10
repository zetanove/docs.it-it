---
title: "Struct (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, struct"
  - "struct [C#]"
ms.assetid: b7cf4ff2-0eb7-4e5c-93d5-b2196b4f5d89
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# Struct (Guida per programmatori C#)
Per la definizione delle strutture viene utilizzata la parola chiave [struct](../../../csharp/language-reference/keywords/struct.md), ad esempio:  
  
 [!code-cs[csProgGuideObjects#39](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/structs_1.cs)]  
  
 Le strutture condividono la maggior parte della sintassi delle classi, sebbene le prime siano più limitate rispetto alle seconde:  
  
-   All'interno di una dichiarazione di struttura, i campi non possono essere inizializzati se non sono stati dichiarati come const o static.  
  
-   Uno struct non può dichiarare un distruttore o un costruttore predefinito, ovvero un costruttore senza parametri.  
  
-   Le strutture vengono copiate su assegnazione.  Quando una struttura viene assegnata a una nuova variabile, vengono copiati tutti i dati e qualsiasi modifica alla nuova copia non causa la modifica dei dati nella copia originale.  Questo è importante da ricordare quando si utilizzano raccolte con tipi di valore come Dictionary\<string, myStruct\>.  
  
-   Le strutture sono tipi di valore, mentre le classi sono tipi di riferimento.  
  
-   A differenza delle classi, è possibile creare istanze di oggetti struttura senza utilizzare un operatore `new`.  
  
-   Le strutture possono dichiarare costruttori con parametri.  
  
-   Una struttura non può ereditare da un'altra struct o da un'altra classe né può costituire la base di una classe.  Tutte le strutture ereditano direttamente da `System.ValueType`, che eredita da `System.Object`.  
  
-   Una struttura può implementare interfacce.  
  
-   È possibile assegnare un valore null a una struttura che può essere utilizzata come tipo nullable.  
  
## Sezioni correlate  
 Per ulteriori informazioni:  
  
-   [Utilizzo di struct](../../../csharp/programming-guide/classes-and-structs/using-structs.md)  
  
-   [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)  
  
-   [Procedura: differenza tra il passaggio a un metodo di uno struct e di un riferimento a una classe](../../../csharp/programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md)  
  
-   [Procedura: implementare conversioni tra struct definite dall'utente](../../../csharp/programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)  
  
-   [Ulteriori informazioni sulle variabili](http://go.microsoft.com/fwlink/?LinkId=221230) in [Visual c\# 2010 iniziale](http://go.microsoft.com/fwlink/?LinkId=221214)  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)