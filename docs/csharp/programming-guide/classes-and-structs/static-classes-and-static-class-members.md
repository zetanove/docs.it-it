---
title: Classi statiche e membri di classi statiche (Guida per programmatori C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, static members
- static members [C#]
- static classes [C#]
- C# language, static classes
- static class members [C#]
ms.assetid: 235614b5-1371-4dbd-9abd-b406a8b0298b
caps.latest.revision: 49
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f93706bb5df41e46c860ca70d131d94015a6348f
ms.lasthandoff: 03/13/2017

---
# <a name="static-classes-and-static-class-members-c-programming-guide"></a>Classi statiche e membri di classi statiche (Guida per programmatori C#)
Una classe [statica](../../../csharp/language-reference/keywords/static.md) corrisponde fondamentalmente a una classe non statica, ma c'è una differenza: di una classe statica non è possibile creare un'istanza. In altre parole, non è possibile usare la parola chiave [new](../../../csharp/language-reference/keywords/new.md) per creare una variabile del tipo di classe. Poiché non esiste una variabile dell'istanza, si accede ai membri di una classe statica tramite il nome stesso della classe. Ad esempio, se si dispone di una classe statica denominata `UtilityClass` che dispone di un metodo pubblico denominato `MethodA`, si chiama il metodo come mostrato nell'esempio seguente:  
  
```csharp  
UtilityClass.MethodA();  
```  
  
 Una classe statica può essere usata come un contenitore adatto per insiemi di metodi che funzionano solo sui parametri di input e non devono ottenere o impostare campi di istanza interni. Ad esempio, nella libreria di classi .NET Framework, la classe statica <xref:System.Math?displayProperty=fullName> contiene diversi metodi che eseguono operazioni matematiche, senza alcun requisito per archiviare o recuperare dati univoci per una particolare istanza della classe <xref:System.Math>. In altre parole, si applicano i membri della classe specificando il nome della classe e il nome del metodo, come illustrato nell'esempio seguente.  
  
```csharp  
double dub = -3.14;  
Console.WriteLine(Math.Abs(dub));  
Console.WriteLine(Math.Floor(dub));  
Console.WriteLine(Math.Round(Math.Abs(dub)));  
  
// Output:  
// 3.14  
// -4  
// 3  
```  
  
 Come per tutti i tipi di classi, le informazioni sul tipo di una classe statica vengono caricate da [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] Common Language Runtime (CLR) durante il caricamento del programma che fa riferimento alle classi. Il programma non può specificare esattamente quando la classe verrà caricata. Tuttavia, è garantito che la classe sarà caricata, che i suoi campi saranno inizializzati e che il costruttore statico sarà chiamato prima che il programma faccia riferimento per la prima volta alla classe stessa. Un costruttore statico viene chiamato solo un volta e una classe statica rimane in memoria per la durata del dominio dell'applicazione in cui risiede il programma.  
  
> [!NOTE]
>  Per creare una classe non statica che consente la creazione di un'unica istanza di se stessa, vedere [Implementing Singleton in C#](http://go.microsoft.com/fwlink/?LinkID=100567) (Implementare Singleton in C#).  
  
 Nell'esempio riportato di seguito sono indicate le principali funzionalità delle classi statiche:  
  
-   Contiene solo membri statici.  
  
-   Non è possibile crearne istanze.  
  
-   È sealed.  
  
-   Non può contenere [costruttori di istanze](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md).  
  
 La creazione di una classe statica è pertanto analoga alla creazione di una classe che contiene solo membri statici e un costruttore privato, che impedisce la creazione di istanze della classe. Una classe statica presenta un indubbio vantaggio. Consente infatti al compilatore di verificare che non vengano aggiunti accidentalmente membri di istanze e quindi di garantire che non vengano create istanze di questa classe.  
  
 Le classi statiche sono sealed e pertanto non possono essere ereditate. Possono ereditare solo dalla classe <xref:System.Object>. Le classi statiche non possono contenere un costruttore di istanza; possono però contenere un costruttore statico. Le classi non statiche devono definire anche un costruttore statico se la classe contiene membri statici che richiedono un'inizializzazione più complessa. Per altre informazioni, vedere [Costruttori statici](../../../csharp/programming-guide/classes-and-structs/static-constructors.md).  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un esempio di una classe statica contenente due metodi che consentono di convertire i valori relativi alla temperatura da gradi Celsius a gradi Fahrenheit e viceversa:  
  
 [!code-cs[csProgGuideObjects#31](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-classes-and-static-class-members_1.cs)]  
  
## <a name="static-members"></a>Membri static  
 Una classe non statica può contenere metodi, campi, proprietà o eventi statici. È possibile chiamare il membro statico di una classe anche quando non sono state create istanze della classe. Al membro statico si accede sempre tramite il nome della classe, non tramite il nome dell'istanza. Di un membro statico esiste una sola copia, indipendentemente dal numero di istanze della classe create. Proprietà e metodi statici non possono accedere a campi non statici ed eventi nel tipo che li contiene e non possono accedere a una variabile dell'istanza di qualsiasi oggetto a meno che non venga esplicitamente passata in un parametro del metodo.  
  
 È più frequente dichiarare una classe non statica con alcuni membri statici, che dichiarare un'intera classe come statica. Due utilizzi comuni di campi statici sono: tenere un conteggio del numero di oggetti di cui è stata creata un'istanza o archiviare un valore che deve essere condiviso fra tutte le istanze.  
  
 I metodi statici possono essere sottoposti a overload ma non a override, perché appartengono alla classe e non a qualsiasi istanza della classe.  
  
 Sebbene non sia possibile dichiarare un campo come `static const`, il campo [const](../../../csharp/language-reference/keywords/const.md) è essenzialmente statico nel comportamento. Appartiene al tipo, non a istanze del tipo. Pertanto, non è possibile accedere ai campi const tramite la stessa notazione `ClassName.MemberName` usata per i campi statici. Non è richiesta alcuna istanza dell'oggetto.  
  
 C# non supporta variabili locali statiche (variabili dichiarate nell'ambito del metodo).  
  
 I membri delle classi statiche vengono dichiarati tramite la parola chiave `static` prima del tipo restituito, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideObjects#29](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-classes-and-static-class-members_2.cs)]  
  
 I membri statici vengono inizializzati prima dell'accesso iniziale e prima dell'eventuale chiamata al costruttore statico, se presente. Per accedere a un membro di una classe statica, usare il nome della classe anziché il nome di una variabile per specificare la posizione del membro, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideObjects#30](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-classes-and-static-class-members_3.cs)]  
  
 Se la classe contiene campi statici, fornire un costruttore statico che li inizializzi al caricamento della classe.  
  
 Una chiamata a un metodo statico genera un'istruzione call in Microsoft Intermediate Language (MSIL), mentre una chiamata a un metodo di istanza genera un'istruzione `callvirt` che verifica anche la presenza di riferimenti a un oggetto null. Tuttavia, nella maggior parte dei casi, la differenza di prestazioni tra i due non è significativa.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Static](../../../csharp/language-reference/keywords/static.md)   
 [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)   
 [class](../../../csharp/language-reference/keywords/class.md)   
 [Costruttori statici](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)   
 [Costruttori di istanza](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)
