---
title: "Classi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "classi [C#]"
  - "C# (linguaggio), classi"
ms.assetid: e8848524-7273-429f-8aba-c658d5eff5ad
caps.latest.revision: 40
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 40
---
# Classi (Guida per programmatori C#)
Una *classe* è un costrutto che consente di creare tipi personalizzati raggruppando insieme variabili di altri tipi, metodi ed eventi.  Una classe è simile a un progetto iniziale.  Definisce i dati e il comportamento di un tipo.  Se la classe non è dichiarata come statica, il codice client può utilizzarla creando *oggetti* o *istanze* assegnati a una variabile.  La variabile rimane in memoria finché tutti i riferimenti ad essa non escono dall'ambito.  In quel momento, CLR la contrassegna come idonea per la procedura di Garbage Collection.  Se la classe è dichiarata come [statica](../../../csharp/language-reference/keywords/static.md), in memoria ne esiste una sola copia accessibile dal codice client solo tramite la classe stessa, non una *variabile dell'istanza*.  Per ulteriori informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 A differenza delle strutture, le classi supportano l'*ereditarietà*, una caratteristica fondamentale della programmazione orientata a oggetti.  Per ulteriori informazioni, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
## Dichiarazioni di classi  
 Le classi vengono dichiarate utilizzando la parola chiave [class](../../../csharp/language-reference/keywords/class.md), come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideObjects#79](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_1.cs)]  
  
 La parola chiave `class` è preceduta dal livello di accesso.  Poiché in questo caso viene utilizzato [public](../../../csharp/language-reference/keywords/public.md), qualsiasi utente può creare oggetti da questa classe.  Il nome della classe segue la parola chiave `class`.  Il resto della definizione è costituito dal corpo della classe, in cui vengono definiti il comportamento e i dati.  I campi, le proprietà, i metodi e gli eventi di una classe vengono collettivamente definiti *membri della classe*.  
  
## Creazione di oggetti  
 Anche se a volte vengono utilizzati in modo interscambiabile, classi e oggetti sono differenti.  Una classe definisce un tipo di oggetto, ma non l'oggetto stesso.  Un oggetto è un'entità concreta basata su una classe e viene a volte definito istanza di una classe.  
  
 Gli oggetti possono essere creati utilizzando la parola chiave [new](../../../csharp/language-reference/keywords/new.md) seguita dal nome della classe su cui sarà basato l'oggetto, come illustrato di seguito:  
  
 [!code-cs[csProgGuideObjects#80](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_2.cs)]  
  
 Quando viene creata un'istanza di una classe, al programmatore viene restituito un riferimento all'oggetto.  Nell'esempio precedente `object1` è un riferimento a un oggetto basato su `Customer`.  Fa riferimento al nuovo oggetto, ma non contiene i dati dell'oggetto stesso.  In realtà è possibile creare un riferimento a un oggetto anche senza creare l'oggetto:  
  
 [!code-cs[csProgGuideObjects#81](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_3.cs)]  
  
 Non è consigliabile creare riferimenti a oggetti come questo che non fa riferimento a un oggetto, perché il tentativo di accedere a un oggetto tramite tale riferimento genererà un errore in fase di esecuzione.  È tuttavia possibile creare un riferimento a un oggetto, creando un nuovo oggetto oppure assegnandolo a un oggetto esistente, come illustrato di seguito:  
  
 [!code-cs[csProgGuideObjects#82](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_4.cs)]  
  
 Con questo codice vengono creati due riferimenti allo stesso oggetto.  Pertanto le modifiche effettuate all'oggetto tramite `object3` si rifletteranno nei successivi utilizzi di `object4`,  perché agli oggetti basati su classi viene fatto riferimento mediante riferimento, in quanto le classi sono note come tipi riferimento.  
  
## Ereditarietà delle classi  
 L'ereditarietà si ottiene tramite l'utilizzo di una *derivazione*, ossia una classe viene dichiarata mediante una *classe di base* da cui eredita dati e comportamenti.  Una classe base viene specificata aggiungendo un segno di due punti e il nome della classe base dopo il nome della classe derivata, come illustrato di seguito:  
  
 [!code-cs[csProgGuideObjects#83](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_5.cs)]  
  
 Quando una classe dichiara una classe di base, eredita tutti i membri di quest'ultima, tranne i costruttori.  
  
 A differenza del C\+\+, in C\# una classe può ereditare direttamente da una sola classe base.  Tuttavia, dato che una classe base può ereditare a sua volta da un'altra classe, una classe può ereditare indirettamente da più classi base.  Inoltre, una classe può implementare direttamente più di un'interfaccia.  Per ulteriori informazioni, vedere [Interfacce](../../../csharp/programming-guide/interfaces/index.md).  
  
 Una classe può essere dichiarata [astratta](../../../csharp/language-reference/keywords/abstract.md).  Una classe astratta contiene metodi astratti che dispongono di una definizione della firma, ma non dispongono di implementazione.  Non è possibile creare istanze di una classe astratta.  È possibile utilizzarla solo tramite classi derivate che implementano i metodi astratti.  Al contrario, una classe [sealed](../../../csharp/language-reference/keywords/sealed.md) non consente alle altre classi di derivare da sé stessa.  Per ulteriori informazioni, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
 Le definizioni di classe possono essere suddivise tra file di origine differenti.  Per ulteriori informazioni, vedere [Classi e metodi parziali](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md).  
  
## Descrizione  
 Nell'esempio seguente viene definita una classe pubblica, contenente un unico campo, un metodo e un metodo speciale denominato costruttore.  Per ulteriori informazioni, vedere [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md).  Viene quindi creata un'istanza di questa classe con la parola chiave `new`.  
  
## Esempio  
 [!code-cs[csProgGuideObjects#84](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/classes_6.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Programmazione orientata ad oggetti](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)   
 [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)   
 [Membri](../../../csharp/programming-guide/classes-and-structs/members.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [Oggetti](../../../csharp/programming-guide/classes-and-structs/objects.md)