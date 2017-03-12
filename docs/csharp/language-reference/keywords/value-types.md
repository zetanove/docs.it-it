---
title: "Tipi di valore (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.valuetypes"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, tipi di valori"
  - "tipi [C#], tipi di valori"
  - "tipi di valori [C#]"
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Tipi di valore (Riferimenti per C#)
I tipi di valore sono suddivisi in due categorie principali:  
  
-   [Strutture](../../../csharp/language-reference/keywords/struct.md)  
  
-   [Enumerazioni](../../../csharp/language-reference/keywords/enum.md)  
  
 Le strutture sono suddivise nelle seguenti categorie:  
  
-   Tipi numerici  
  
    -   [Tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)  
  
    -   [Tipi a virgola mobile](../../../csharp/language-reference/keywords/floating-point-types-table.md)  
  
    -   [decimal](../../../csharp/language-reference/keywords/decimal.md)  
  
-   [bool](../../../csharp/language-reference/keywords/bool.md)  
  
-   Strutture definite dall'utente.  
  
## Caratteristiche principali dei tipi di valore  
 Le variabili basate sui tipi di valore contengono direttamente i valori.  Se una variabile basata su un tipo di valore viene assegnata a un'altra variabile, il valore contenuto viene copiato,  a differenza di quanto avviene con l'assegnazione delle variabili basate su un tipo di riferimento, nel qual caso viene copiato un riferimento all'oggetto ma non l'oggetto stesso.  
  
 Tutti i tipi di valore sono derivati in modo implicito dall'oggetto <xref:System.ValueType?displayProperty=fullName>.  
  
 A differenza dei tipi di riferimento, non è possibile derivare un nuovo tipo da un tipo di valore.  Analogamente ai tipi di riferimento, tuttavia, le strutture consentono di implementare interfacce.  
  
 A differenza dei tipi di riferimento, un tipo di valore non può contenere il valore `null`.  Tuttavia, la funzionalità [tipi nullable](../../../csharp/programming-guide/nullable-types/index.md) consente l'invio dei tipi di valore venga assegnata a `null`.  
  
 Ciascun tipo di valore presenta un costruttore predefinito implicito che inizializza il valore predefinito di tale tipo.  Per informazioni sui valori predefiniti dei tipi di valore, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md).  
  
## Caratteristiche principali dei tipi semplici  
 Tutti i tipi semplici, ossia quelli interni al linguaggio C\#, sono alias dei tipi di sistema .NET Framework.  Ad esempio, [int](../../../csharp/language-reference/keywords/int.md) è un alias di <xref:System.Int32?displayProperty=fullName>.  Per un elenco completo di alias, vedere [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md).  
  
 Le espressioni costanti, i cui operandi sono tutti costanti di tipo semplice, vengono valutate in fase di compilazione.  
  
 È possibile inizializzare i tipi semplici mediante i valori letterali.  Ad esempio "A" è un valore effettivo di tipo `char` e 2001 è un valore effettivo di tipo `int`.  
  
## Inizializzazione dei tipi di valore  
 Non è possibile utilizzare variabili locali in C\# senza averle prima inizializzate.  Nell'esempio riportato di seguito viene dichiarata una variabile locale senza inizializzazione:  
  
```  
int myInt;  
```  
  
 Non è possibile utilizzare la variabile senza prima procedere all'inizializzazione.  È possibile effettuare l'inizializzazione mediante la seguente istruzione:  
  
```  
myInt = new int();  // Invoke default constructor for int type.  
```  
  
 Questa istruzione equivale all'istruzione seguente:  
  
```  
myInt = 0;         // Assign an initial value, 0 in this example.  
```  
  
 È possibile, naturalmente, inserire dichiarazione e inizializzazione nella stessa istruzione, come negli esempi riportati di seguito:  
  
```  
int myInt = new int();  
```  
  
 Oppure  
  
```  
int myInt = 0;  
```  
  
 Utilizzando l'operatore [new](../../../csharp/language-reference/keywords/new.md) viene chiamato il costruttore predefinito del tipo specifico e assegnato il valore predefinito alla variabile.  Nell'esempio precedente il costruttore predefinito assegna il valore `0` a `myInt`.  Per ulteriori informazioni sui valori assegnati chiamando i costruttori predefiniti, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md).  
  
 Con i tipi definiti dall'utente utilizzare [new](../../../csharp/language-reference/keywords/new.md) per richiamare il costruttore predefinito.  L'istruzione seguente, ad esempio, richiama il costruttore predefinito della struttura `Point`:  
  
```  
Point p = new Point(); // Invoke default constructor for the struct.  
```  
  
 Dopo questa chiamata la struttura è considerata definitivamente assegnata, ovvero tutti i membri di cui è composta sono inizializzati ai corrispondenti valori predefiniti.  
  
 Per ulteriori informazioni sul nuovo operatore, vedere [new](../../../csharp/language-reference/keywords/new.md).  
  
 Per informazioni sulla formattazione dell'output dei tipi numerici, vedere [Tabella della formattazione dei risultati numerici](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [Tabelle di riferimento per i tipi](../../../csharp/language-reference/keywords/reference-tables-for-types.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)