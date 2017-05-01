---
title: Generics in .NET Framework | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- generic methods, type inference
- generics [.NET Framework], collections
- generic interfaces [.NET Framework]
- constructed generic types
- nested generic types
- generic type definitions
- generic classes [.NET Framework]
- generics [.NET Framework], interfaces
- generics [.NET Framework], about
- generics [.NET Framework]
- generic collections [.NET Framework]
- generic delegates [.NET Framework]
- generic type arguments
- generics [.NET Framework], delegates
- generics [.NET Framework], features
- constraints [.NET Framework]
- generic types
- generic type parameters
ms.assetid: 2994d786-c5c7-4666-ab23-4c83129fe39c
caps.latest.revision: 23
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: 83ab82e7ef31b26321f513da668de25ed9690e04
ms.lasthandoff: 04/08/2017

---
# <a name="generics-in-the-net-framework"></a>Generics in .NET Framework
<a name="top"></a> I generics consentono di personalizzare un metodo, una classe o una struttura in base ai dati precisi su cui interviene. Ad esempio, invece di usare la classe <xref:System.Collections.Hashtable>, che consente di avere chiavi e valori di ogni tipo, è possibile usare la classe generica <xref:System.Collections.Generic.Dictionary%602> e specificare il tipo concesso per la chiave e quello concesso per il valore. Tra i vantaggi dei generics ci sono una maggiore riutilizzabilità del codice e l'indipendenza dai tipi.  
  
 In questo argomento vengono forniti una panoramica dei generics nel.NET Framework e un riepilogo dei tipi o metodi generici. Include le sezioni seguenti:  
  
-   [Definizione e uso dei generics](#defining_and_using_generics)  
  
-   [Terminologia dei generics](#generics_terminology)  
  
-   [Libreria di classi e supporto del linguaggio](#class_library_and_language_support)  
  
-   [Generics e tipi annidati](#nested_types_and_generics)  
  
-   [Argomenti correlati](#related_topics)  
  
-   [Riferimento](#reference)  
  
<a name="defining_and_using_generics"></a>   
## <a name="defining-and-using-generics"></a>Definizione e utilizzo dei generics  
 I generics sono classi, strutture, interfacce e metodi dotati di segnaposto (parametri di tipo) per uno o più dei tipi archiviati o usati. Una classe di raccolte generiche può usare un parametro di tipo come segnaposto per il tipo di oggetti in essa contenuti. I parametri di tipo vengono visualizzati come i tipi dei relativi campi e i tipi di parametri dei relativi metodi. Un metodo generico potrebbe usare il parametro di tipo come il tipo di valore restituito o come il tipo di uno dei parametri formali. Nel codice seguente viene illustrata una definizione di classe generica semplice.  
  
 [!code-cpp[Conceptual.Generics.Overview#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#2)]
 [!code-csharp[Conceptual.Generics.Overview#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#2)]
 [!code-vb[Conceptual.Generics.Overview#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#2)]  
  
 Quando si crea un'istanza di una classe generica, è possibile specificare i tipi effettivi da sostituire per i parametri di tipo. Ciò consente di stabilire una nuova classe generica, definita come una classe generica costruita, con tipi prescelti sostituiti a ogni occorrenza dei parametri di tipo. Il risultato è una classe indipendente dai tipi personalizzata in base alla scelta di tipi, come illustrato nel codice seguente.  
  
 [!code-cpp[Conceptual.Generics.Overview#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#3)]
 [!code-csharp[Conceptual.Generics.Overview#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#3)]
 [!code-vb[Conceptual.Generics.Overview#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#3)]  
  
<a name="generics_terminology"></a>   
### <a name="generics-terminology"></a>Terminologia dei generics  
 I termini seguenti vengono usati per discutere dei generics in .NET Framework:  
  
-   Una *definizione di tipo generico* è una classe, una struttura o una dichiarazione di interfaccia che funge da modello, con segnaposto per i tipi che può contenere o usare. Ad esempio, la classe <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> può contenere due tipi: chiavi e valori. Poiché una definizione di tipo generico è solo un modello, non è possibile creare istanze di una classe, una struttura o un'interfaccia che sia una definizione di tipo generico.  
  
-   I*parametri di tipo generico*, o *parametri di tipo*, sono i segnaposto in una definizione di tipo o metodo generico. Il tipo generico <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> ha due parametri di tipo, `TKey` e `TValue`, che rappresentano i tipi delle chiavi e dei valori relativi.  
  
-   Un *tipo generico costruito*, o *tipo costruito*, è il risultato della specifica di tipi per i parametri di tipo generico di una definizione di tipo generico.  
  
-   Un *argomento di tipo generico* è qualsiasi tipo che verrà sostituito con un parametro di tipo generico.  
  
-   Il termine generale *tipo generico* include sia tipi costruiti sia definizioni di tipo generico.  
  
-   La*covarianza* e la *controvarianza* of generic type parameters enable you to use constructed generic types whose type arguments are more derived (covariance) or less derived (controvarianza) than a target constructed type. La covarianza e la controvarianza sono definite collettivamente *varianza*. Per altre informazioni, vedere [Covarianza e controvarianza](../../../docs/standard/generics/covariance-and-contravariance.md).  
  
-   I*vincoli* sono limiti imposti su parametri di tipo generico. Ad esempio, è possibile limitare un parametro di tipo a tipi che implementano l'interfaccia generica <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName>, per garantire la possibilità di ordinare le istanze del tipo. È anche possibile vincolare i parametri di tipo a tipi che dispongono di una determinata classe di base, con un costruttore predefinito, o che siano tipi riferimento o tipi di valore. Gli utenti di tipo generico non possono sostituire gli argomenti di tipo che non soddisfano i vincoli.  
  
-   Una *definizione di metodo generico* è un metodo con due elenchi di parametri: un elenco di parametri di tipo generico e un elenco di parametri formali. I parametri di tipo possono apparire come tipo restituito o come tipi dei parametri formali, come illustrato nel codice seguente.  
  
 [!code-cpp[Conceptual.Generics.Overview#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#4)]
 [!code-csharp[Conceptual.Generics.Overview#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#4)]
 [!code-vb[Conceptual.Generics.Overview#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#4)]  
  
 I metodi generici possono apparire su tipi generici o non generici. È importante tenere presente che un metodo si definisce non generico solo perché appartiene a un tipo generico o perché ha parametri formali i cui tipi sono i parametri generici del tipo contenitore. Un metodo è generico solo se ha un proprio elenco di parametri di tipo. Nel codice seguente, solo il metodo `G` è generico.  
  
 [!code-cpp[Conceptual.Generics.Overview#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#5)]
 [!code-csharp[Conceptual.Generics.Overview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#5)]
 [!code-vb[Conceptual.Generics.Overview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#5)]  
  
 [Torna all'inizio](#top)  
  
<a name="advantages_limitations"></a>   
## <a name="advantages-and-disadvantages-of-generics"></a>Vantaggi e svantaggi dei generics  
 Esistono numerosi vantaggi nell'utilizzo di delegati e raccolte di tipi generici:  
  
-   Indipendenza dai tipi. I generics spostano il carico dell'indipendenza dai tipi al compilatore. Non è necessario scrivere codice per verificare il tipo di dati corretto perché viene applicato in fase di compilazione. La necessità del cast di tipo e la possibilità di errori di run-time sono ridotte.  
  
-   Meno codice e il codice è più facilmente riutilizzato. Non è necessario ereditare da un tipo di base ed eseguire l'override di membri. Ad esempio, la classe <xref:System.Collections.Generic.LinkedList%601> è pronta per l'uso immediato. Ad esempio, è possibile creare un elenco collegato di stringhe con la seguente dichiarazione di variabile:  
  
     [!code-cpp[HowToGeneric#24](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/source2.cpp#24)]
     [!code-csharp[HowToGeneric#24](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/source2.cs#24)]
     [!code-vb[HowToGeneric#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/source2.vb#24)]  
  
-   Prestazioni migliori. I tipi di raccolte generiche offrono in genere prestazioni migliori per l'archiviazione e la modifica dei tipi di valore, perché non è necessario eseguirne il boxing.  
  
-   I delegati generici consentono di eseguire il callback indipendente dai tipi senza la necessità di creare più classi delegate. Ad esempio, il delegato generico <xref:System.Predicate%601> consente di creare un metodo per implementare i propri criteri di ricerca di un tipo particolare e di usare il proprio metodo con metodi di tipo <xref:System.Array>, ad esempio <xref:System.Array.Find%2A>, <xref:System.Array.FindLast%2A> e <xref:System.Array.FindAll%2A>.  
  
-   I generics ottimizzano il codice generato dinamicamente. Quando si usano i generics con il codice generato in modo dinamico non è necessario generare il tipo. In questo modo aumenta il numero di scenari in cui è possibile usare i metodi dinamici leggeri invece di generare interi assembly. Per altre informazioni, vedere Procedura: definire ed eseguire metodi dinamici e DynamicMethod.  
  
 Di seguito sono elencate alcune limitazioni di generics:  
  
-   I tipi generici possono derivare dalla maggior parte delle classi base, ad esempio <xref:System.MarshalByRefObject> (e i vincoli possono essere usati per richiedere che i parametri di tipo generico derivino da classi base quali <xref:System.MarshalByRefObject>). Tuttavia, il [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] non supporta tipi generici associati al contesto. Un tipo generico può derivare da <xref:System.ContextBoundObject>, ma provare a creare un'istanza di quel tipo causa un <xref:System.TypeLoadException>.  
  
-   L'enumerazione non può avere parametri di tipo generico. Un'enumerazione può essere generica solo incidentalmente (ad esempio, perché è annidata in un tipo generico che viene definito con Visual Basic, C# o C++). Per altre informazioni, vedere "Enumerazioni" in [Common Type System](../../../docs/standard/base-types/common-type-system.md).  
  
-   I metodi dinamici leggeri non possono essere generici.  
  
-   In Visual Basic, C# e C++ non è possibile creare un'istanza di un tipo annidato in un tipo generico a meno che non siano stati assegnati i tipi ai parametri di tipo di tutti i tipi di inclusione. In altre parole, in una reflection un tipo annidato che viene definito con questi linguaggi contiene i parametri di tutti i relativi tipi di inclusione. Ciò consente di usare i parametri di tipo dei tipi in inclusione nelle definizioni di membro di un tipo annidato. Per altre informazioni, vedere la sezione "Tipi annidati" in <xref:System.Type.MakeGenericType%2A>.  
  
    > [!NOTE]
    >  Un tipo annidato definito con la creazione di codice in un assembly dinamico o usando [Ilasm.exe (Assembler IL)](../../../docs/framework/tools/ilasm-exe-il-assembler.md) non deve includere i parametri di tipo dei relativi tipi di inclusione. Tuttavia, se non li include, i parametri di tipo non saranno nell'ambito della classe annidata.  
  
     Per altre informazioni, vedere la sezione "Tipi annidati" in <xref:System.Type.MakeGenericType%2A>.  
  
 [Torna all'inizio](#top)  
  
<a name="class_library_and_language_support"></a>   
## <a name="class-library-and-language-support"></a>Libreria di classi e supporto del linguaggio  
 .NET Framework fornisce una serie di classi di raccolte generiche negli spazi dei nomi seguenti:  
  
-   Lo spazio dei nomi <xref:System.Collections.Generic> cataloga gran parte dei tipi di raccolte generiche forniti da .NET Framework, come le classi generiche <xref:System.Collections.Generic.List%601> e <xref:System.Collections.Generic.Dictionary%602>.  
  
-   Lo spazio dei nomi <xref:System.Collections.ObjectModel> cataloga tipi di raccolte generiche aggiuntive, come la classe generica <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>, utili per esporre i modelli di oggetto agli utenti delle classi.  
  
 Nello spazio dei nomi <xref:System> sono disponibili interfacce generiche per l'implementazione di confronti di uguaglianza e ordinamento, oltre ai tipi delegati generici per gestori eventi, conversioni e predicati di ricerca.  
  
 Il supporto dei generics è stato aggiunto allo spazio dei nomi <xref:System.Reflection> per l'esame di tipi e metodi generici, a <xref:System.Reflection.Emit> per la creazione di assembly dinamici che contengono tipi e metodi generici e a <xref:System.CodeDom> per la generazione di grafici di origine che includono generics.  
  
 Il Common Language Runtime fornisce nuovi codici operativi e prefissi per supportare i tipi generici nel linguaggio MSIL (Microsoft Intermediate Language), inclusi <xref:System.Reflection.Emit.OpCodes.Stelem>, <xref:System.Reflection.Emit.OpCodes.Ldelem>, <xref:System.Reflection.Emit.OpCodes.Unbox_Any>, <xref:System.Reflection.Emit.OpCodes.Constrained> e <xref:System.Reflection.Emit.OpCodes.Readonly>.  
  
 Visual C++, C# e Visual Basic forniscono il supporto completo per la definizione e l'utilizzo dei generics. Per altre informazioni sul supporto dei linguaggi, vedere [Tipi generici in Visual Basic](~/docs/visual-basic/programming-guide/language-features/data-types/generic-types.md), [Introduzione ai generics](~/docs/csharp/programming-guide/generics/introduction-to-generics.md) e [Panoramica dei generics in C++](http://msdn.microsoft.com/library/21f10637-0fce-4916-b925-6c86a126d3aa).  
  
 [Torna all'inizio](#top)  
  
<a name="nested_types_and_generics"></a>   
## <a name="nested-types-and-generics"></a>Generics e tipi annidati  
 Un tipo annidato all'interno di un tipo generico può dipendere dai parametri di tipo del tipo generico che lo contiene. Common Language Runtime considera i tipi annidati come generici, anche se non dispongono di propri parametri di tipo generico. Quando si crea un'istanza di un tipo annidato, è necessario specificare gli argomenti di tipo per tutti i tipi generici.  
  
 [Torna all'inizio](#top)  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Raccolte generiche in .NET Framework](../../../docs/standard/generics/collections.md)|Vengono descritte le classi di raccolte generiche e altri tipi generici in .NET Framework.|  
|[Delegati generici per la modifica di matrici ed elenchi](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)|Vengono descritti i delegati generici per conversioni, predicati di ricerca e azioni da eseguire sugli elementi di una matrice o raccolta.|  
|[Interfacce generiche](../../../docs/standard/generics/interfaces.md)|Vengono descritte le interfacce generiche che forniscono funzionalità comuni a famiglie di tipi generici.|  
|[Covarianza e controvarianza](../../../docs/standard/generics/covariance-and-contravariance.md)|Vengono descritte la covarianza e controvarianza nei parametri di tipo generico.|  
|[Tipi di raccolte comunemente utilizzate](../../../docs/standard/collections/commonly-used-collection-types.md)|Fornisce informazioni di riepilogo sulle caratteristiche e gli scenari di utilizzo dei tipi di raccolta in .NET Framework, inclusi i tipi generici.|  
|[Quando utilizzare raccolte generiche](../../../docs/standard/collections/when-to-use-generic-collections.md)|Vengono descritte le regole generali per determinare quando usare i tipi di raccolte generiche.|  
|[Procedura: Definire un tipo generico tramite reflection emit](../../../docs/framework/reflection-and-codedom/how-to-define-a-generic-type-with-reflection-emit.md)|Viene illustrato come generare assembly dinamici che includono tipi e metodi generici.|  
|[Tipi generici in Visual Basic](~/docs/visual-basic/programming-guide/language-features/data-types/generic-types.md)|Viene descritta la funzionalità generics per gli utenti di Visual Basic, tra cui procedure relative all'utilizzo e alla definizione di tipi generici.|  
|[Introduzione ai generics](~/docs/csharp/programming-guide/generics/introduction-to-generics.md)|Viene fornita una panoramica di definizione e utilizzo di tipi generici per gli utenti di C#.|  
|[Panoramica di Generics in Visual C++](http://msdn.microsoft.com/library/21f10637-0fce-4916-b925-6c86a126d3aa)|Viene descritta la funzionalità generics per gli utenti di C++, incluse le differenze tra generics e modelli.|  
  
<a name="reference"></a>   
## <a name="reference"></a>Riferimento  
 <xref:System.Collections.Generic>  
  
 <xref:System.Collections.ObjectModel>  
  
 <xref:System.Reflection.Emit.OpCodes?displayProperty=fullName>  
  
 [Torna all'inizio](#top)
