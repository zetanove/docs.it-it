---
title: "Ereditariet&#224; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "classi astratte (C#)"
  - "metodi astratti [C#]"
  - "linguaggio C#, ereditarietà"
  - "classi derivate [C#]"
  - "ereditarietà [C#]"
  - "metodi virtuali [C#]"
ms.assetid: 81d64ee4-50f9-4d6c-a8dc-257c348d2eea
caps.latest.revision: 38
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 38
---
# Ereditariet&#224; (Guida per programmatori C#)
L’ereditarietà, insieme all'incapsulamento e al polimorfismo, rappresenta una delle tre principali caratteristiche \(o *pilastri*\) della programmazione orientata a oggetti.  L'ereditarietà permette di creare nuove classi che riutilizzano, estendono e modificano il comportamento definito in altre classi.  La classe i cui membri vengono ereditati è denominata *classe base*, mentre la classe che eredita tali membri è denominata *classe derivata*.  Classe derivata può disporre al massimo di una classe di base diretta.  Tuttavia, l'ereditarietà è transitiva.  Se ClassC viene derivata da ClassB e ClassB viene derivata da ClassA, ClassC eredita i membri dichiarati in ClassB e in ClassA.  
  
> [!NOTE]
>  Le strutture non supportano l'ereditarietà, mentre possono implementare interfacce.  Per ulteriori informazioni, vedere [Interfacce](../../../csharp/programming-guide/interfaces/index.md).  
  
 Concettualmente, una classe derivata rappresenta una specializzazione della classe base.  Ad esempio, avendo una classe base `Animal`, è possibile definire una classe derivata denominata `Mammal` e un’altra classe derivata denominata `Reptile`.  Un oggetto `Mammal` è anche un oggetto`Animal` e un oggetto `Reptile` è anche un `Animal`, ma ciascuna classe derivata rappresenta una diversa specializzazione della classe base.  
  
 Quando si definisce una classe derivandola da un'altra classe, la classe derivata acquista implicitamente tutti i membri della classe base, con l’eccezione dei costruttori e dei distruttori.  Di conseguenza, la classe derivata può riutilizzare il codice definito nella classe base senza doverlo implementare nuovamente.  Nella classe derivata è possibile aggiungere altri membri .  In questo modo, la classe derivata estende la funzionalità della classe base.  
  
 Nella figura riportata di seguito viene mostrata una classe `WorkItem` che rappresenta un elemento di lavoro in un qualche processo aziendale.  Come per tutte le classi, è derivata da <xref:System.Object?displayProperty=fullName> ed eredita tutti i metodi di tale classe.  `WorkItem` aggiunge cinque suoi membri.  Includono un costruttore, perché non vengono ereditati costruttori.  La classe `ChangeRequest` eredita da `WorkItem` e rappresenta un particolare tipo di elemento di lavoro.  `ChangeRequest` aggiunge altri due membri ai membri che eredita da `WorkItem` e da <xref:System.Object>.  Deve aggiungere il proprio costruttore e aggiunge anche `originalItemID`.  La proprietà `originalItemID` consente all'istanza `ChangeRequest` di essere associata a `WorkItem` originale a cui la richiesta modifiche è applicata.  
  
 ![Ereditarietà di classe](../../../csharp/programming-guide/classes-and-structs/media/class-inheritance.png "Class\_Inheritance")  
Ereditarietà delle classi  
  
 Nell'esempio seguente viene illustrato come le relazioni tra le classi mostrate nella precedente illustrazione vengono espresse in C\#.  Nell'esempio viene inoltre descritto come la classe `WorkItem` implementa l’override del metodo virtuale <xref:System.Object.ToString%2A?displayProperty=fullName> e come la classe `ChangeRequest` eredita l’implementazione del metodo definito dalla classe `WorkItem`.  
  
 [!code-cs[csProgGuideInheritance#49](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/inheritance_1.cs)]  
  
## Metodi virtuali e astratti  
 Quando una classe base dichiara un metodo come [virtuale](../../../csharp/language-reference/keywords/virtual.md), una classe derivata può [eseguire l'override](../../../csharp/language-reference/keywords/override.md) del metodo definendo una propria implementazione.  Quando una classe di base dichiara un membro come [astratto](../../../csharp/language-reference/keywords/abstract.md), è necessario effettuare l'override di tale metodo in ogni classe non astratta che eredita direttamente da tale classe.  Quando una classe derivata è dichiarata a sua volta astratta, eredita i membri astratti senza implementarli.  I membri astratti e virtuali costituiscono la base del polimorfismo, che rappresenta la seconda principale caratteristica della programmazione orientata a oggetti.  Per ulteriori informazioni, vedere [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
## Classi base astratte  
 Quando si desidera prevenire la generazione di istanze dirette di una classe, è possibile dichiararla come [astratta](../../../csharp/language-reference/keywords/abstract.md) utilizzando la parola chiave [new](../../../csharp/language-reference/keywords/new.md).  In questo modo, la classe è utilizzabile soltanto quando una nuova classe viene derivata da essa.  Una classe astratta può contenere una o più firme di metodi a loro volta dichiarati come astratti.  Tali firme specificano i parametri e il valore restituito, ma non definiscono alcuna implementazione \(corpo del metodo\).  Una classe astratta non deve necessariamente contenere membri astratti. Tuttavia, quando una classe contiene un membro astratto, deve essere dichiarata come astratta.  Le classi derivate non definite come astratte devono fornire l'implementazione per qualsiasi metodo astratto ereditato da una classe base astratta.  Per ulteriori informazioni, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
## Interfacce  
 Un'*interfaccia* rappresenta un tipo di riferimento ed è per vari aspetti simile a una classe base astratta costituita solo da membri astratti.  Quando una classe implementa un'interfaccia, deve fornire un'implementazione per tutti i membri definiti nell’interfaccia.  Una classe può implementare più interfacce, anche se può essere derivata solo da una singola classe base diretta.  
  
 Le interfacce sono utilizzate per definire specifiche funzionalità per le classi che non sono necessariamente caratterizzate da una relazione di tipo "è un".  Ad esempio, l’interfaccia <xref:System.IEquatable%601?displayProperty=fullName>può essere implementata da qualunque classe o struct che deve abilitare il codice client per determinare se due oggetti di un dato tipo sono equivalenti \(comunque il tipo definisce l’equivalenza\).  <xref:System.IEquatable%601> non implica lo stesso tipo di relazione "è" esistente tra una classe di base e una classe derivata \(ad esempio, un `Mammal` è un `Animal`\).  Per ulteriori informazioni, vedere [Interfacce](../../../csharp/programming-guide/interfaces/index.md).  
  
## Accesso ai membri di una classe base da parte di una classe derivata  
 Una classe derivata ha accesso ai membri di una classe di base dichiarati come public, protected, internal e protected internal.  Sebbene una classe derivata erediti i membri privati di una classe base, non può avere accesso a tali membri.  Tuttavia, tutti i membri privati continuano a esistere nella classe derivata e possono operare esattamente come farebbero nella classe base stessa.  Ad esempio, si supponga che un metodo protetto della classe base acceda a un campo privato.  Quel campo deve essere presente nella classe derivata per permettere il corretto funzionamento del metodo ereditato dalla classe base.  
  
## Prevenzione di un’ulteriore derivazione  
 È possibile impedire che altre classi ereditino da una data classe o da uno qualsiasi dei suoi membri, dichiarando tale classe o tale membro come [sealed](../../../csharp/language-reference/keywords/sealed.md).  Per ulteriori informazioni, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
## Nascondere un membro di una classe base in una classe derivata  
 Una classe derivata può nascondere i membri di una classe base dichiarando dei membri con lo stesso nome e la stessa firma.  Il modificatore [new](../../../csharp/language-reference/keywords/new.md) può essere utilizzato per indicare in modo esplicito che un membro non costituisce un override del membro della classe base.  L'utilizzo del modificatore [new](../../../csharp/language-reference/keywords/new.md) non è necessario, tuttavia, quando il modificatore[new](../../../csharp/language-reference/keywords/new.md) non viene utilizzato, il compilatore genererà un avviso.  Per ulteriori informazioni, vedere [Controllo delle versioni con le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md) e [Sapere quando utilizzare le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [classe](../../../csharp/language-reference/keywords/class.md)   
 [struct](../../../csharp/language-reference/keywords/struct.md)