---
title: "Oggetti (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "oggetti [C#], informazioni sugli oggetti"
  - "variabili [C#]"
ms.assetid: af4a5230-fbf3-4eea-95e1-8b883c2f845c
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# Oggetti (Guida per programmatori C#)
Una definizione di classe o struttura è simile a un progetto iniziale in cui vengono specificate le funzionalità del tipo.  Un oggetto è essenzialmente un blocco di memoria che è stato allocato e configurato in base al progetto iniziale.  Un programma può creare molti oggetti della stessa classe.  Gli oggetti, definiti anche istanze, possono essere archiviati in una variabile denominata o in una matrice o raccolta.  Il codice client è il codice che utilizza queste variabili per chiamare i metodi e accedere alle proprietà pubbliche dell'oggetto.  In un linguaggio orientato a oggetti quale C\#, un tipico programma è costituito da più oggetti che interagiscono dinamicamente.  
  
> [!NOTE]
>  I tipi statici si comportano in modo diverso da quanto viene descritto in questo punto.  Per ulteriori informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
## Istanze della struttura VS. istanze della classe  
 Poiché le classi sono tipi di riferimento, una variabile di un oggetto classe contiene un riferimento all'indirizzo dell'oggetto sull'heap gestito.  Se al primo oggetto viene assegnato un secondo oggetto dello stesso tipo, entrambe le variabili fanno riferimento all'oggetto in corrispondenza di tale indirizzo.  Questo punto viene illustrato più dettagliatamente in seguito in questo argomento.  
  
 Le istanze di classi vengono create utilizzando l'[operatore new](../../../csharp/language-reference/keywords/new-operator.md).  Nel seguente esempio, `Person` è il tipo e `person1` e `person 2` sono istanze, o oggetti, di tale tipo.  
  
 [!code-cs[csProgGuideStatements#30](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/objects_1.cs)]  
  
 Poiché le strutture sono tipi di valore, una variabile di un oggetto struttura contiene una copia dell'intero oggetto.  Anche le istanze di strutture possono essere create tramite l'operatore `new`, ma non è obbligatorio, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#31](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/objects_2.cs)]  
  
 La memoria per entrambi gli oggetti `p1` sia `p2` viene allocata sullo stack di thread.  Tale memoria viene recuperata insieme al tipo o al metodo in cui è stata dichiarata.  Questo è il motivo per cui le strutture vengono copiate per assegnazione.  Per contrasto, la memoria allocata per l'istanza di una classe viene recuperata automaticamente \(tramite Garbage Collection\) da Common Language Runtime quando tutti i riferimenti all'oggetto sono usciti dall'ambito.  Non è possibile eliminare in modo deterministico un oggetto di classe come invece avviene in C\+\+.  Per ulteriori informazioni sul sistema di Garbage Collection in [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)], vedere [Garbage Collection](../Topic/Garbage%20Collection.md).  
  
> [!NOTE]
>  L'allocazione e la deallocazione di memoria sull'heap gestito sono estremamente ottimizzate in Common Language Runtime.  Nella maggior parte dei casi non esistono differenze significative in termini di impatto sulle prestazioni tra l'allocazione di un'istanza di classe sull'heap e l'allocazione di un'istanza di struttura sullo stack.  
  
## Identità dell'oggetto VS. uguaglianza di valori  
 Quando si confrontano due oggetti per verificarne l'uguaglianza, è necessario innanzitutto distinguere se si desidera determinare se le due variabili rappresentano lo stesso oggetto in memoria oppure se i valori di uno o più campi sono equivalenti.  Se si intende confrontare valori, è necessario considerare se gli oggetti sono istanze di tipi di valore \(strutture\) o di tipi di riferimento \(classi, delegati, matrici\).  
  
-   Per determinare se due istanze di classe fanno riferimento alla stessa posizione in memoria \(ovvero hanno la stessa *identità*\), utilizzare il metodo statico <xref:System.Object.Equals%2A>.  <xref:System.Object?displayProperty=fullName> è la classe di base implicita per tutti i tipi valore e i tipi riferimento, incluse strutture e classi definite dall'utente.  
  
-   Per determinare se i campi di istanza in due istanze di strutture hanno gli stessi valori, utilizzare il metodo <xref:System.ValueType.Equals%2A?displayProperty=fullName>.  Poiché tutte le strutture ereditano implicitamente da <xref:System.ValueType?displayProperty=fullName>, il metodo viene chiamato direttamente sull'oggetto, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#32](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/objects_3.cs)]  
  
 L'implementazione <xref:System.ValueType?displayProperty=fullName> di `Equals` utilizza la reflection perché deve essere in grado di determinare i tipi di campi presenti in tutte le strutture.  Quando si creano strutture, eseguire l'override del metodo `Equals` per fornire un algoritmo di uguaglianza efficiente specifico del tipo.  
  
-   Per determinare se i valori dei campi in due istanze della classe sono uguali, è possibile utilizzare il metodo <xref:System.Object.Equals%2A> o l'[operatore \=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md).  Tuttavia, utilizzarli solo se la classe ha eseguito il loro override o overload per fornire una definizione personalizzata di cosa significa "uguaglianza" per gli oggetti di quel tipo.  È possibile anche che la classe implementi l'interfaccia <xref:System.IEquatable%601> dell'interfaccia <xref:System.Collections.Generic.IEqualityComparer%601>.  Entrambe le interfacce forniscono metodi che possono essere utilizzati per verificare l'uguaglianza dei valori.  Durante la progettazione di classi personalizzate che eseguono l'override di `Equals`, assicurarsi di seguire le linee guida stabilite in [Procedura: definire l'uguaglianza di valori per un tipo](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md) e in <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName>.  
  
## Sezioni correlate  
 Per ulteriori informazioni:  
  
-   [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)  
  
-   [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md)  
  
-   [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
  
-   [Eventi](../../../csharp/programming-guide/events/index.md)  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [oggetto](../../../csharp/language-reference/keywords/object.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [classe](../../../csharp/language-reference/keywords/class.md)   
 [struct](../../../csharp/language-reference/keywords/struct.md)   
 [Operatore new](../../../csharp/language-reference/keywords/new-operator.md)   
 [Common Type System](../../../standard/base-types/common-type-system.md)