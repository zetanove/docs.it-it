---
title: "Classi e struct (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, classi"
  - "linguaggio C#, oggetti"
  - "linguaggio C#, struct"
  - "classi [C#], panoramica"
  - "oggetti [C#]"
  - "struct [C#], informazioni sulle struct"
ms.assetid: cc39dbda-8754-423e-b5b1-16a1db0734c0
caps.latest.revision: 48
caps.handback.revision: 48
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Classi e struct (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Classi e strutture sono due dei costrutti di base del Common Type System in .NET Framework.  Ognuno di essi è essenzialmente una struttura di dati che incapsula un insieme di dati e comportamenti strettamente correlati a costituire un'unità logica.  I dati e i comportamenti sono i *membri* della classe o della struttura e includono i metodi, le proprietà, gli eventi, ecc., come elencato in seguito in questo argomento.  
  
 Una classe o una dichiarazione della struttura è come un progetto iniziale utilizzato per creare istanze o oggetti in fase di esecuzione .  Se si definisce una classe o una struttura chiamata `Person`, `Person` è il nome del tipo.  Se si dichiara e inizializza una variabile `p` di tipo `Person`, si dice che `p` sia un oggetto o un'istanza di `Person`.  È possibile creare istanze Multiple dello stesso tipo `Person` e ogni istanza può disporre di valori diversi nelle proprietà e nei campi.  
  
 Una classe è un tipo di riferimento.  Quando viene creato un oggetto della classe, la variabile alla quale è assegnato l'oggetto contiene solo un riferimento a quella memoria.  Quando il riferimento a un oggetto è assegnato a una nuova variabile, la nuova variabile si riferisce all'oggetto originale.  Le modifiche apportate tramite una variabile vengono riflesse nell'altra variabile perché entrambe si riferiscono agli stessi dati.  
  
 Una struttura è un tipo di valore.  Quando viene creata una struttura, la variabile alla quale è assegnata, contiene i dati effettivi della struttura.  Quando la struttura è assegnata a una nuova variabile, viene copiata.  La nuova variabile e la variabile originale contengono pertanto due copie separate degli stessi dati.  Eventuali modifiche apportate a una copia non influiscono sull'altra copia.  
  
 In generale, le classi sono utilizzate per modellare un comportamento più complesso o dati che devono essere modificati dopo la creazione di un oggetto di classe.  Le strutture sono più adatte per piccole strutture di dati contenenti principalmente dati che non devono essere modificati dopo la creazione della struttura.  
  
 Per ulteriori informazioni, vedere [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md), [Oggetti](../../../csharp/programming-guide/classes-and-structs/objects.md) e [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md).  
  
## Esempio  
 Nell'esempio seguente viene definita la classe `MyCustomClass` con tre membri in corrispondenza del livello superiore dello spazio dei nomi `ProgrammingGuide`.  Viene creata un'istanza \(oggetto\) di `MyCustomClass` nel metodo `Main` della classe `Program`. I metodi e le proprietà dell'oggetto sono accessibili tramite notazione del punto.  
  
 [!code-cs[csProgGuideObjects#88](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/index_1.cs)]  
  
## Incapsulamento  
 *L'incapsulamento* talvolta è definito come il primo pilastro o il principio della programmazione orientata a oggetti.  In base al principio di incapsulamento, una classe o una struttura possono specificare il modo in cui ognuno dei membri è accessibile al codice esterno alla classe o alla struttura.  Metodi e variabili che non devono essere utilizzati dall'esterno della classe o dell'assembly possono essere nascosti per limitare il rischio di errori di codifica o esiti dannosi.  
  
 Per ulteriori informazioni sulle classi, vedere [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md) e [Oggetti](../../../csharp/programming-guide/classes-and-structs/objects.md).  
  
### Membri  
 Tutti i metodi, i campi, le costanti, le proprietà e gli eventi devono essere dichiarati all'interno di un tipo; sono denominati i *membri* del tipo.  In C\#, non esistono variabili o metodi globali come in altri linguaggi.  Anche il punto di ingresso del programma, il metodo `Main` deve essere dichiarato all'interno di una classe o di una struttura.  Nell'elenco seguente sono inclusi tutti i vari tipi di membri che possono essere dichiarati in una classe o in una struttura.  
  
-   [Campi](../../../csharp/programming-guide/classes-and-structs/fields.md)  
  
-   [Costanti](../../../csharp/programming-guide/classes-and-structs/constants.md)  
  
-   [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)  
  
-   [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
  
-   [Eventi](../../../csharp/programming-guide/events/index.md)  
  
-   [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)  
  
-   [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
-   [Tipi annidati](../../../csharp/programming-guide/classes-and-structs/nested-types.md)  
  
### Accessibilità  
 Alcuni metodi e proprietà devono essere chiamati o resi accessibili a codice esterno alla classe o struttura, noto come *codice client*.  Altri metodi e proprietà possono essere riservati esclusivamente ad un utilizzo all'interno della stessa classe o struttura.  Ciò è importante per limitare l'accessibilità del codice in modo che solo il codice client desiderato possa raggiungerlo.  È possibile specificare il modo in cui è possibile accedere ai tipi e ai relativi membri dal codice client, utilizzando i modificatori di accesso [public](../../../csharp/language-reference/keywords/public.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md), `protected internal` e [private](../../../csharp/language-reference/keywords/private.md).  L'accessibilità predefinita è `private`.  Per ulteriori informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
### Ereditarietà  
 Le classi \(ma non le strutture\) supportano il concetto di ereditarietà.  Una classe che deriva da un'altra classe \(la *classe di base*\) contiene automaticamente tutti i membri pubblici, protetti e interni della classe di base, ad eccezione di costruttori e distruttori.  Per ulteriori informazioni, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md) e [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
 Le classi possono essere dichiarate come [astratte](../../../csharp/language-reference/keywords/abstract.md), ossia con uno o più metodi senza implementazione.  Anche se non è possibile crearne direttamente un'istanza, le classi astratte possono fungere da classi di base per altre classi che forniscono l'implementazione mancante.  Le classi possono essere dichiarate anche come [sealed](../../../csharp/language-reference/keywords/sealed.md) per impedire che altre classi ereditino da esse.  Per ulteriori informazioni, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
### Interfacce  
 Le classi e le strutture possono ereditare più interfacce.  Ereditare da un'interfaccia significa che il tipo implementa tutti i metodi definiti nell'interfaccia.  Per ulteriori informazioni, vedere [Interfacce](../../../csharp/programming-guide/interfaces/index.md).  
  
### Tipi generici  
 Le classi e le strutture possono essere definite con uno o più parametri di tipo.  Il codice client fornisce il tipo quando ne crea un'istanza.  Ad esempio, la classe <xref:System.Collections.Generic.List%601> nello spazio dei nomi <xref:System.Collections.Generic> è definita con un parametro di tipo.  Il codice client crea un'istanza di `List<string>` o `List<int>` per specificare il tipo che sarà contenuto nell'elenco.  Per ulteriori informazioni, vedere [Generics](../../../csharp/programming-guide/generics/index.md).  
  
### Tipi statici  
 Le classi \(ma non le strutture\) possono essere dichiarate come [statiche](../../../csharp/language-reference/keywords/static.md).  Una classe statica può contenere solo membri statici e non è possibile crearne un'istanza con la nuova parola chiave.  Una copia della classe viene caricata in memoria durante il caricamento del programma e i relativi membri sono accessibili tramite il nome della classe.  Sia le classi che le strutture possono contenere membri statici.  Per ulteriori informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
### Tipi annidati  
 Una classe o una struttura possono essere annidate all'interno di un'altra classe o struttura.  Per ulteriori informazioni, vedere [Tipi annidati](../../../csharp/programming-guide/classes-and-structs/nested-types.md).  
  
### Tipi parziali  
 È possibile definire una parte di una classe, struttura o metodo in un file di codice e un'altra parte in un file di codice distinto.  Per ulteriori informazioni, vedere [Classi e metodi parziali](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md).  
  
### Inizializzatori di oggetti  
 È possibile creare un'istanza e inizializzare oggetti di classi o strutture e raccolte di oggetti, senza chiamare in modo esplicito il relativo costruttore.  Per ulteriori informazioni, vedere [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
### Tipi anonimi  
 Nelle situazioni in cui non conviene o non è necessario creare una classe denominata, ad esempio quando si popola un elenco con strutture di dati che non devono necessariamente essere persistenti o passate a un altro metodo, è possibile utilizzare i tipi anonimi.  Per ulteriori informazioni, vedere [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
### Metodi di estensione  
 È possibile "estendere" una classe senza creare una classe derivata creando un tipo distinto i cui metodi possono essere chiamati come se appartenessero al tipo originale.  Per ulteriori informazioni, vedere [Metodi di estensione](../../../csharp/programming-guide/classes-and-structs/extension-methods.md).  
  
### Variabili locali tipizzate in modo implicito  
 All'interno di un metodo di classe o struttura è possibile utilizzare la tipizzazione implicita per indicare al compilatore di determinare il tipo corretto in fase di compilazione.  Per ulteriori informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)