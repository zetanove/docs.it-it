---
title: Tipi (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- value types [C#]
- reference types [C#]
- types [C#]
- C# language, data types
- common type system [C#]
- data types [C#]
- C# language, types
- strong typing [C#]
ms.assetid: f782d7cc-035e-4500-b1b1-36a9881130ad
caps.latest.revision: 53
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: 61f23020b8a5dd0136d54e0a2ceb925bebca88cc
ms.lasthandoff: 03/31/2017

---
# <a name="types-c-programming-guide"></a>Tipi (Guida per programmatori C#)
## <a name="types-variables-and-values"></a>Tipi, variabili e valori  
 C# è un linguaggio fortemente tipizzato. Ogni variabile e costante ha un tipo, così come ogni espressione che restituisce un valore. Ogni firma del metodo specifica un tipo per ogni parametro di input e per il valore restituito. La libreria di classi .NET Framework definisce un set di tipi numerici incorporati, oltre a tipi più complessi che rappresentano un'ampia gamma di costrutti logici, ad esempio il file system, le connessioni di rete, le raccolte e le matrici di oggetti e le date. Un tipico programma C# usa tipi dalla libreria di classi e tipi definiti dall'utente che modellano i concetti specifici del dominio relativo al problema del programma.  
  
 Le informazioni archiviate in un tipo possono includere quanto segue:  
  
-   Lo spazio di archiviazione richiesto da una variabile del tipo.  
  
-   I valori minimi e massimi che può rappresentare.  
  
-   I membri (metodi, campi, eventi e così via) in esso contenuti.  
  
-   Il tipo di base da cui eredita.  
  
-   Il percorso in cui viene allocata la memoria per le variabili in fase di esecuzione.  
  
-   I tipi di operazioni consentite.  
  
 Il compilatore usa le informazioni sul tipo per assicurarsi che tutte le operazioni eseguite nel codice siano *indipendenti dai tipi*. Se ad esempio si dichiara una variabile di tipo [int](../../../csharp/language-reference/keywords/int.md), il compilatore consente di usare la variabile anche in operazioni di addizione e sottrazione. Se si prova a eseguire le stesse operazioni su una variabile di tipo [bool](../../../csharp/language-reference/keywords/bool.md), il compilatore genera un errore, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideTypes#42](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_1.cs)]  
  
> [!NOTE]
>  Gli sviluppatori C e C++ devono tenere presente che, in C#, [bool](../../../csharp/language-reference/keywords/bool.md) non è convertibile in [int](../../../csharp/language-reference/keywords/int.md).  
  
 Il compilatore incorpora le informazioni sul tipo nel file eseguibile come metadati. Il Common Language Runtime (CLR) usa i metadati in fase di esecuzione per garantire una maggiore indipendenza dai tipi quando alloca e recupera la memoria.  
  
### <a name="specifying-types-in-variable-declarations"></a>Definizione dei tipi nelle dichiarazioni di variabile  
 Quando si dichiara una variabile o una costante in un programma, è necessario specificarne il tipo oppure usare la parola chiave [var](../../../csharp/language-reference/keywords/var.md) per consentire al compilatore di dedurre il tipo. L'esempio seguente illustra alcune dichiarazioni di variabili che usano sia tipi numerici incorporati sia tipi complessi definiti dall'utente:  
  
 [!code-cs[csProgGuideTypes#36](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_2.cs)]  
  
 I tipi di parametri e valori restituiti del metodo sono specificati nella firma del metodo. La firma seguente illustra un metodo che richiede un [int](../../../csharp/language-reference/keywords/int.md) come argomento di input e restituisce una stringa:  
  
 [!code-cs[csProgGuideTypes#35](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_3.cs)]  
  
 Una variabile dichiarata non può essere dichiarata una seconda volta con un tipo nuovo e non è possibile assegnare a tale variabile un valore non compatibile con il relativo tipo dichiarato. Non è possibile, ad esempio, dichiarare una variabile [int](../../../csharp/language-reference/keywords/int.md) e assegnare ad essa il valore booleano [true](../../../csharp/language-reference/keywords/true-literal.md). I valori possono tuttavia essere convertiti in altri tipi, ad esempio quando vengono assegnati a nuove variabili o passati come argomenti di metodo. Una *conversione del tipo* che non causa la perdita di dati viene eseguita automaticamente dal compilatore, mentre una conversione che può causare la perdita di dati richiede un *cast* nel codice sorgente.  
  
 Per altre informazioni, vedere [Cast e conversioni di tipi](../../../csharp/programming-guide/types/casting-and-type-conversions.md).  
  
## <a name="built-in-types"></a>Tipi incorporati  
 Il linguaggio C# offre un set standard di tipi numerici incorporati per rappresentare numeri interi, valori a virgola mobile, espressioni booleane, caratteri di testo, valori decimali e altri tipi di dati. Sono anche disponibili tipi `string` e `object` incorporati, che possono essere usati in qualsiasi programma C#. Per altre informazioni sui tipi incorporati, vedere [Tabelle di riferimento per i tipi](../../../csharp/language-reference/keywords/reference-tables-for-types.md).  
  
## <a name="custom-types"></a>Tipi personalizzati  
 Usare i costrutti [struct](../../../csharp/language-reference/keywords/struct.md), [class](../../../csharp/language-reference/keywords/class.md), [interface](../../../csharp/language-reference/keywords/interface.md) e [enum](../../../csharp/language-reference/keywords/enum.md) per creare tipi personalizzati. La libreria di classi .NET Framework è una raccolta di tipi personalizzati offerti da Microsoft che è possibile usare nelle nuove applicazioni. Per impostazione predefinita, i tipi più comunemente usati nella libreria di classi sono disponibili in qualsiasi programma C#, mentre altri diventano disponibili solo quando si aggiunge in modo esplicito un riferimento di progetto all'assembly in cui sono definiti. Nel momento in cui il compilatore ha un riferimento all'assembly, è possibile dichiarare variabili (e costanti) dei tipi dichiarati nell'assembly in codice sorgente. Per altre informazioni, vedere [Libreria di classi .NET Framework](http://go.microsoft.com/fwlink/?LinkID=217856).  
  
## <a name="the-common-type-system"></a>Common Type System  
 È importante tenere presente due aspetti fondamentali del sistema dei tipi in [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]:  
  
-   Supporta il principio di ereditarietà. I tipi possono derivare da altri tipi, denominati *tipi di base*. Il tipo derivato eredita (con alcune limitazioni) metodi, proprietà e altri membri del tipo di base, che a sua volta può derivare da un altro tipo. In questo caso, il tipo derivato eredita i membri di entrambi i tipi di base nella gerarchia di ereditarietà. Tutti i tipi, inclusi quelli numerici incorporati, ad esempio <xref:System.Int32?displayProperty=fullName> (parola chiave C#: [int](../../../csharp/language-reference/keywords/int.md)), derivano in ultima istanza da un unico tipo di base, ovvero <xref:System.Object?displayProperty=fullName> (parola chiave C#: [object](../../../csharp/language-reference/keywords/object.md)). Questa gerarchia di tipi unificata prende il nome di [Common Type System](http://msdn.microsoft.com/library/53c57c96-83e1-4ee3-9543-9ac832671a89) (CTS). Per altre informazioni sull'ereditarietà in C#, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
-   Nel CTS ogni tipo è definito come *tipo valore* o *tipo riferimento*. In queste due categorie sono inclusi anche tutti i tipi personalizzati nella libreria di classi .NET Framework e i tipi definiti dall'utente. I tipi definiti tramite la parola chiave [struct](../../../csharp/language-reference/keywords/struct.md) sono tipi valore e tutti i tipi numerici incorporati sono tipi `structs`. I tipi definiti tramite la parola chiave [class](../../../csharp/language-reference/keywords/class.md) sono tipi riferimento. I tipi riferimento e i tipi valore hanno regole diverse in fase di compilazione e un comportamento diverso in fase di esecuzione.  
  
 La figura seguente illustra la relazione tra tipi valore e tipi riferimento nel CTS.  
  
 ![Tipi valore e tipi riferimento](../../../csharp/programming-guide/types/media/valuetypescts.png "ValueTypesCTS")  
Tipi valore e tipi riferimento nel CTS  
  
> [!NOTE]
>  È possibile osservare come i tipi usati con maggiore frequenza siano tutti organizzati nello spazio dei nomi <xref:System>. L'inserimento di un tipo in uno spazio dei nomi, tuttavia, è indipendente dalla categoria a cui appartiene il tipo.  
  
### <a name="value-types"></a>Tipi valore  
 I tipi valore derivano da <xref:System.ValueType?displayProperty=fullName>, che deriva da <xref:System.Object?displayProperty=fullName>. I tipi che derivano da <xref:System.ValueType?displayProperty=fullName> hanno un comportamento speciale nel CLR. Le variabili dei tipi valore contengono direttamente i rispettivi valori, ovvero la memoria viene allocata inline nel contesto in cui è dichiarata la variabile. Non esiste un'allocazione heap o un overhead di Garbage Collection separato per le variabili dei tipi valore.  
  
 Esistono due categorie di tipi valore: [struct](../../../csharp/language-reference/keywords/struct.md) e [enum](../../../csharp/language-reference/keywords/enum.md).  
  
 I tipi numerici incorporati sono struct i cui metodi e le cui proprietà sono accessibili dall'utente:  
  
```csharp  
// Static method on type Byte.  
byte b = Byte.MaxValue;  
```  
  
 Ad essi, tuttavia, si dichiarano e si assegnano valori come se fossero tipi non aggregati semplici:  
  
```csharp  
byte num = 0xA;  
int i = 5;  
char c = 'Z';  
```  
  
 I tipi valore sono *sealed*, ovvero non è possibile, ad esempio, derivare un tipo da <xref:System.Int32?displayProperty=fullName> e non è possibile definire un tipo struct da ereditare da un tipo struct o da una classe definita dall'utente, poiché un tipo struct può ereditare solo da <xref:System.ValueType?displayProperty=fullName>. Un tipo struct può tuttavia implementare una o più interfacce. È possibile eseguire il cast di un tipo struct in un tipo di interfaccia. Questa operazione genera tuttavia una *conversione boxing* con cui si esegue il wrapping del tipo struct in un oggetto tipo riferimento sull'heap gestito. Le operazioni di conversione boxing si verificano anche quando si passa un tipo valore a un metodo che accetta <xref:System.Object?displayProperty=fullName> come parametro di input. Per altre informazioni, vedere [Boxing e unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md).  
  
 Usare la parola chiave [struct](../../../csharp/language-reference/keywords/struct.md) per creare tipi valore personalizzati. In genere, un tipo struct viene usato come contenitore per un piccolo set di variabili correlate, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideObjects#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/index_4.cs)]  
  
 Per altre informazioni sui tipi struct, vedere [Struct](../../../csharp/programming-guide/classes-and-structs/structs.md). Per altre informazioni sui tipi valore in [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], vedere [Common Type System](http://msdn.microsoft.com/library/53c57c96-83e1-4ee3-9543-9ac832671a89).  
  
 L'altra categoria di tipi valore è [enum](../../../csharp/language-reference/keywords/enum.md). Un tipo enum definisce un set di costanti integrali denominate. L'enumerazione <xref:System.IO.FileMode?displayProperty=fullName> nella libreria di classi .NET Framework, ad esempio, contiene un set di valori interi costanti e denominati che specificano come deve essere aperto un file. L'enumerazione deve essere definita come illustrato nell'esempio seguente:  
 
 [!code-cs[csProgGuideTypes#44](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_5.cs)]  
  
 Il valore della costante `System.IO.FileMode.Create` è 2. I nomi, tuttavia, sono molto più significativi per gli utenti che leggono il codice sorgente e, quindi, è preferibile usare enumerazioni anziché valori letterali numerici costanti. Per altre informazioni, vedere <xref:System.IO.FileMode?displayProperty=fullName>.  
  
 Tutte le enumerazioni ereditano da <xref:System.Enum?displayProperty=fullName>, che eredita da <xref:System.ValueType?displayProperty=fullName>. Tutte le regole valide per i tipi struct sono valide anche per le enumerazioni. Per altre informazioni sulle enumerazioni, vedere [Tipi di enumerazione](../../../csharp/programming-guide/enumeration-types.md).  
  
### <a name="reference-types"></a>Tipi riferimento  
 Un tipo definito come [classe](../../../csharp/language-reference/keywords/class.md), [delegato](../../../csharp/language-reference/keywords/delegate.md), matrice o [interfaccia](../../../csharp/language-reference/keywords/interface.md) è un *tipo riferimento*. In fase di esecuzione, quando si dichiara una variabile di un tipo riferimento, la variabile contiene il valore [null](../../../csharp/language-reference/keywords/null.md) fino a quando non si crea in modo esplicito un'istanza dell'oggetto usando l'operatore [new](../../../csharp/language-reference/keywords/new.md) o non la si assegna a un oggetto creato altrove tramite `new, as shown in the following example:`.  
  
```csharp  
MyClass mc = new MyClass();  
MyClass mc2 = mc;  
```  
   Un'interfaccia deve essere inizializzata insieme a un oggetto classe che la implementa. Se `MyClass` implementa `IMyInterface`, si crea un'istanza di `IMyInterface`, come illustrato nell'esempio seguente:  
  
```csharp  
IMyInterface iface = new MyClass();  
```  
  
 Quando viene creato l'oggetto, la memoria viene allocata nell'heap gestito e la variabile mantiene solo un riferimento al percorso dell'oggetto. I tipi nell'heap gestito richiedono un overhead quando vengono allocati e recuperati dalla funzionalità di gestione automatica della memoria del CLR, nota come *Garbage Collection*. La Garbage Collection, tuttavia, è anche altamente ottimizzata e, nella maggior parte degli scenari, non genera un problema di prestazioni. Per altre informazioni sulla Garbage Collection, vedere [Gestione automatica della memoria](http://msdn.microsoft.com/library/d4850de5-fa63-4936-a250-5678d118acba).  
  
 Tutte le matrici sono tipi riferimento, anche se i relativi elementi sono tipi valore. Le matrici derivano in modo implicito dalla classe <xref:System.Array?displayProperty=fullName>, ma vengono dichiarate e usate con la sintassi semplificata fornita da C#, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideTypes#45](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_6.cs)]  
  
 I tipi riferimento supportano completamente l'ereditarietà. Quando si crea una classe, è possibile ereditare da qualsiasi altra interfaccia o classe non definita come [sealed](../../../csharp/language-reference/keywords/sealed.md); altre classi, inoltre, possono ereditare dalla classe appena creata ed eseguire l'override dei metodi virtuali. Per altre informazioni su come creare classi personalizzate, vedere [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md). Per altre informazioni sull'ereditarietà e sui metodi virtuali, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
## <a name="types-of-literal-values"></a>Tipi di valori letterali  
 In C# i valori letterali ricevono un tipo dal compilatore. È possibile specificare come deve essere tipizzato un valore letterale numerico aggiungendo una lettera alla fine del numero. Per specificare, ad esempio, che il valore 4.56 deve essere considerato come un tipo float, aggiungere una "f" o una "F" dopo il numero: `4.56f`. Se non viene aggiunta alcuna lettera, il compilatore dedurrà un tipo per il valore letterale. Per altre informazioni sui tipi che possono essere specificati con suffissi letterali, vedere le pagine di riferimento relative ai singoli tipi in [Tipi valore](../../../csharp/language-reference/keywords/value-types.md).  
  
 Dal momento che i valori letterali sono tipizzati e tutti i tipi derivano in ultima istanza da <xref:System.Object?displayProperty=fullName>, è possibile scrivere e compilare codice come illustrato di seguito:  
  
 [!code-cs[csProgGuideTypes #37](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_7.cs)]  
  
## <a name="generic-types"></a>Tipi generici  
 Un tipo può essere dichiarato con uno o più *parametri di tipo* che agiscono da segnaposto per il tipo effettivo (*tipo concreto*) che il codice client specifica quando si crea un'istanza del tipo. Questi tipi sono definiti *tipi generici*. Il tipo .NET Framework <xref:System.Collections.Generic.List%601?displayProperty=fullName>, ad esempio, ha un parametro di tipo a cui per convenzione viene assegnato il nome *T*. Quando si crea un'istanza del tipo, si specifica il tipo degli oggetti che saranno contenuti nell'elenco, ad esempio, string:  
 
```csharp
List<string> stringList = new List<string>();
stringList.Add("String example");
// compile time error adding a type other than a string:
stringList.Add(4);
```
 L'uso del parametro di tipo consente di riutilizzare la stessa classe per contenere qualsiasi tipo di elemento senza dover convertire ogni elemento in [object](../../../csharp/language-reference/keywords/object.md). Le classi di raccolte generiche sono definite *raccolte fortemente tipizzate* perché il compilatore conosce il tipo specifico degli elementi della raccolta e può generare un errore in fase di compilazione se, ad esempio, si prova ad aggiungere un numero intero all'oggetto `strings` nell'esempio precedente. Per altre informazioni, vedere [Generics](../../../csharp/programming-guide/generics/index.md).  
  
## <a name="implicit-types-anonymous-types-and-nullable-types"></a>Tipi impliciti, tipi anonimi e tipi nullable  
 Come indicato in precedenza, è possibile tipizzare una variabile locale (ma non membri di classe) in modo implicito usando la parola chiave [var](../../../csharp/language-reference/keywords/var.md). Alla variabile viene comunque assegnato un tipo in fase di compilazione, specificato dal compilatore. Per altre informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
 In alcuni casi non è consigliabile creare un tipo denominato per set semplici di valori correlati che non si intende archiviare o passare fuori dai limiti del metodo. A questo scopo è possibile creare *tipi anonimi*. Per altre informazioni, vedere [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
 I tipi valore comuni non possono avere un valore [null](../../../csharp/language-reference/keywords/null.md). È tuttavia possibile creare tipi valore nullable aggiungendo `?` dopo il tipo. Ad esempio, `int?` è un tipo `int` che può avere anche il valore [null](../../../csharp/language-reference/keywords/null.md). In CTS i tipi nullable sono istanze del tipo di struct generico <xref:System.Nullable%601?displayProperty=fullName>. I tipi nullable sono particolarmente utili quando si passano dati da e verso database in cui possono essere presenti valori numerici null. Per altre informazioni, vedere [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md).  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per altre informazioni, vedere i seguenti argomenti:  
  
-   [Cast e conversioni di tipi](../../../csharp/programming-guide/types/casting-and-type-conversions.md)  
  
-   [Boxing e unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)  
  
-   [Uso del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)  
  
-   [Tipi valore](../../../csharp/language-reference/keywords/value-types.md)  
  
-   [Tipi riferimento](../../../csharp/language-reference/keywords/reference-types.md)  
  
-   [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)  
  
-   [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)  
  
-   [Generics](../../../csharp/programming-guide/generics/index.md)  

## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Conversione dei tipi di dati XML](http://msdn.microsoft.com/library/a2aa99ba-8239-4818-9281-f1d72ee40bde)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)

