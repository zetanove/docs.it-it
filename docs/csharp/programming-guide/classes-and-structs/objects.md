---
title: Oggetti (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- objects [C#], about objects
- variables [C#]
ms.assetid: af4a5230-fbf3-4eea-95e1-8b883c2f845c
caps.latest.revision: 26
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: a5ed524a1b17f7be8903f998cbd732594faab831
ms.openlocfilehash: fe548eb5d520945e3f0d52750bbf89935947116e
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="objects-c-programming-guide"></a>Oggetti (Guida per programmatori C#)
Una definizione di classe o struct è simile a un progetto iniziale in cui vengono specificate le funzionalità del tipo. Un oggetto è essenzialmente un blocco di memoria che è stato allocato e configurato in base al progetto iniziale. Un programma può creare molti oggetti della stessa classe. Gli oggetti, definiti anche istanze, possono essere archiviati in una variabile denominata o in una matrice o raccolta. Il codice client è il codice che usa queste variabili per chiamare i metodi e accedere alle proprietà pubbliche dell'oggetto. In un linguaggio orientato a oggetti come C#, il programma tipico è costituito da più oggetti che interagiscono dinamicamente.  
  
> [!NOTE]
>  I tipi statici si comportano in modo diverso da quanto descritto qui. Per altre informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
## <a name="struct-instances-vs-class-instances"></a>Differenze tra istanze di strutture e Istanze di classe  
 Poiché le classi sono tipi di riferimento, una variabile di un oggetto classe contiene un riferimento all'indirizzo dell'oggetto sull'heap gestito. Se al primo oggetto viene assegnato un secondo oggetto dello stesso tipo, entrambe le variabili fanno riferimento all'oggetto in quell'indirizzo. Questo punto viene illustrato più dettagliatamente di seguito in questo argomento.  
  
 Le istanze delle classi vengono create usando l'[operatore new](../../../csharp/language-reference/keywords/new-operator.md). Nell'esempio seguente `Person` è il tipo e `person1` e `person 2` sono le istanze o gli oggetti di tale tipo.  
  
 [!code-cs[csProgGuideStatements#30](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/objects_1.cs)]  
  
 Poiché gli struct sono tipi di valore, una variabile di un oggetto struct contiene una copia dell'intero oggetto. Le istanze di struct possono essere create anche usando l'operatore `new`, sebbene non sia obbligatorio, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#31](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/objects_2.cs)]  
  
 La memoria per `p1` e `p2` viene allocata nello stack di thread. La memoria viene recuperata insieme al tipo o al metodo in cui è stata dichiarata. Questo è il motivo per cui gli struct vengono copiati per assegnazione. Al contrario, la memoria allocata per l'istanza di una classe viene recuperata automaticamente (tramite Garbage Collection) da Common Language Runtime quando tutti i riferimenti all'oggetto sono usciti dall'ambito. Non è possibile eliminare in modo deterministico un oggetto di classe come avviene in C++. Per altre informazioni su Garbage Collection in [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], vedere [Garbage Collection](../../../standard/garbage-collection/index.md).  
  
> [!NOTE]
>  L'allocazione e la deallocazione di memoria sull'heap gestito sono estremamente ottimizzate in Common Language Runtime. Nella maggior parte dei casi non esistono differenze significative in termini di impatto sulle prestazioni tra l'allocazione di un'istanza di classe sull'heap e l'allocazione di un'istanza di struttura sullo stack.  
  
## <a name="object-identity-vs-value-equality"></a>Differenze tra identità di oggetto e uguaglianza di valori  
 Quando si confrontano due oggetti per verificarne l'uguaglianza, è necessario innanzitutto distinguere se si vuole determinare se le due variabili rappresentano lo stesso oggetto in memoria oppure se i valori di uno o più campi sono equivalenti. Se si intende confrontare valori, è necessario considerare se gli oggetti sono istanze di tipi di valore (struct) o di tipi di riferimento (classi, delegati, matrici).  
  
-   Per determinare se due istanze di classe fanno riferimento alla stessa posizione in memoria (ovvero hanno la stessa *identità*), usare il metodo statico <xref:System.Object.Equals%2A>. <xref:System.Object?displayProperty=fullName> è la classe di base implicita per tutti i tipi valore e i tipi riferimento, inclusi struct e classi definiti dall'utente.  
  
-   Per determinare se i campi di istanza in due istanze di struct hanno gli stessi valori, usare il metodo <xref:System.ValueType.Equals%2A?displayProperty=fullName>. Poiché tutti gli struct ereditano implicitamente da <xref:System.ValueType?displayProperty=fullName>, il metodo viene chiamato direttamente nell'oggetto, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#32](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/objects_3.cs)]  
  
 L'implementazione <xref:System.ValueType?displayProperty=fullName> di `Equals` usa la reflection perché deve essere in grado di determinare i campi presenti in tutti gli struct. Quando si creano struct, eseguire l'override del metodo `Equals` per specificare un algoritmo di uguaglianza efficiente specifico del tipo.  
  
-   Per determinare se i valori dei campi in due istanze di classe sono uguali, è possibile usare il metodo <xref:System.Object.Equals%2A> o l'operatore [==](../../../csharp/language-reference/operators/equality-comparison-operator.md). Tuttavia, usarli solo se la classe ha eseguito il loro override o overload per offrire una definizione personalizzata di cosa significa "uguaglianza" per gli oggetti di quel tipo. La classe può anche implementare l'interfaccia <xref:System.IEquatable%601> o <xref:System.Collections.Generic.IEqualityComparer%601>. Entrambe le interfacce offrono metodi che possono essere usati per verificare l'uguaglianza dei valori. Durante la progettazione di classi che eseguono l'override di `Equals`, assicurarsi di seguire le linee guida definite in [Procedura: Definire l'uguaglianza di valori per un tipo](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md) e <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName>.  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per ulteriori informazioni:  
  
-   [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)  
  
-   [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md)  
  
-   [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [Finalizzatori](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
  
-   [Eventi](../../../csharp/programming-guide/events/index.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [object](../../../csharp/language-reference/keywords/object.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [class](../../../csharp/language-reference/keywords/class.md)   
 [struct](../../../csharp/language-reference/keywords/struct.md)   
 [Operatore new](../../../csharp/language-reference/keywords/new-operator.md)   
 [Common Type System](../../../standard/base-types/common-type-system.md)
