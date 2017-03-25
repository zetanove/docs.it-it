---
title: Interfacce (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- interfaces [C#]
- C# language, interfaces
ms.assetid: 2feda177-ce11-432d-81b4-d50f5f35fd37
caps.latest.revision: 45
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
ms.openlocfilehash: 25c2bf8830d80f0f41855d0fa9e292b0edcbe052
ms.lasthandoff: 03/13/2017

---
# <a name="interfaces-c-programming-guide"></a>Interfacce (Guida per programmatori C#)
Un'interfaccia contiene le definizioni per un gruppo di funzionalità correlate che possono essere implementate da una [classe](../../../csharp/language-reference/keywords/class.md) o uno [struct](../../../csharp/language-reference/keywords/struct.md).  
  
 Usando le interfacce, è possibile, ad esempio, includere il comportamento di più origini in una classe. Tale funzionalità è importante in C# perché il linguaggio non supporta l'ereditarietà multipla delle classi. Inoltre è necessario usare un'interfaccia se si vuole simulare l'ereditarietà per le struct, perché non possono effettivamente ereditare da un'altra struct o classe.  
  
 Per definire un'interfaccia, si usa la parola chiave [interface](../../../csharp/language-reference/keywords/interface.md), come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideInheritance#47](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/interfaces_1.cs)]  
  
 Qualsiasi classe o struct che implementa l'interfaccia <xref:System.IEquatable%601> deve contenere una definizione per un metodo <xref:System.IEquatable%601.Equals%2A> che corrisponde alla firma specificata dall'interfaccia. Di conseguenza, è possibile affidarsi a una classe che implementa `IEquatable<T>` per contenere un metodo `Equals` con cui un'istanza della classe può determinare se sia uguale a un'altra istanza della stessa classe.  
  
 La definizione di `IEquatable<T>` non fornisce un'implementazione per `Equals`. L'interfaccia definisce solo la firma. In tal modo, un'interfaccia in C# è simile a una classe astratta in cui tutti i metodi sono astratti. Tuttavia, una classe o struct può implementare più interfacce, ma una classe può ereditare una sola classe, astratta o meno. Usando le interfacce, è quindi possibile includere il comportamento di più origini in una classe.  
  
 Per altre informazioni sulle classi astratte, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
 Le interfacce possono contenere metodi, proprietà, eventi, indicizzatori o qualsiasi combinazione di questi quattro membri. Per collegamenti a esempi, vedere [Sezioni correlate](../../../csharp/programming-guide/interfaces/index.md#BKMK_RelatedSections). Un'interfaccia non può contenere costanti, campi, operatori, costruttori di istanze, distruttori o tipi. I membri di interfaccia sono automaticamente pubblici e non possono includere modificatori di accesso. I membri non possono nemmeno essere [statici](../../../csharp/language-reference/keywords/static.md).  
  
 Per implementare un membro di interfaccia, il corrispondente membro della classe di implementazione deve essere pubblico e non statico e avere lo stesso nome e la stessa firma del membro di interfaccia.  
  
 Quando una classe o una struct implementa un'interfaccia, la classe o la struct deve fornire un'implementazione per tutti i membri definiti dall'interfaccia. L'interfaccia stessa non fornisce funzionalità che una classe o struct possa ereditare come può ereditare le funzionalità delle classi base. Tuttavia, se una classe base implementa un'interfaccia, qualsiasi classe derivata dalla classe base eredita tale implementazione.  
  
 Nell'esempio seguente viene illustrata un'implementazione dell'interfaccia IEquatable<T\>. La classe di implementazione, `Car`, deve fornire un'implementazione del metodo <xref:System.IEquatable%601.Equals%2A>.  
  
 [!code-cs[csProgGuideInheritance#48](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/interfaces_2.cs)]  
  
 Le proprietà e gli indicizzatori di una classe possono definire altre funzioni di accesso per una proprietà o un indicizzatore definito in un'interfaccia. Ad esempio, un'interfaccia può dichiarare una proprietà con una funzione di accesso [get](../../../csharp/language-reference/keywords/get.md). La classe che implementa l'interfaccia può dichiarare la stessa proprietà con una funzione di accesso `get` o [set](../../../csharp/language-reference/keywords/set.md). Tuttavia, se la proprietà o l'indicizzatore usa l'implementazione esplicita, le funzioni di accesso devono corrispondere. Per altre informazioni sull'implementazione esplicita, vedere [Implementazione esplicita dell'interfaccia](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md) e [Proprietà dell'interfaccia](../../../csharp/programming-guide/classes-and-structs/interface-properties.md).  
  
 Le Interfacce possono implementare altre interfacce. Una classe può includere un'interfaccia più volte tramite le classi base ereditate o tramite le interfacce implementate da altre interfacce. Tuttavia, la classe può fornire un'implementazione di un'interfaccia solo una volta e solo se la classe dichiara l'interfaccia durante la definizione della classe (`class ClassName : InterfaceName`). Se l'interfaccia viene ereditata perché è stata ereditata una classe base che implementa l'interfaccia, la classe base fornisce l'implementazione dei membri dell'interfaccia. Tuttavia, la classe derivata può reimplementare i membri dell'interfaccia invece di usare l'implementazione ereditata.  
  
 Una classe base può implementare anche i membri di interfaccia usando membri virtuali. In tal caso, una classe derivata può modificare il comportamento dell'interfaccia eseguendo l'override dei membri virtuali. Per altre informazioni su membri virtuali, vedere [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
## <a name="interfaces-summary"></a>Riepilogo delle interfacce  
 Un'interfaccia presenta le proprietà seguenti:  
  
-   Un'interfaccia è uguale a una classe base astratta. Qualsiasi classe o struct che implementa l'interfaccia deve implementarne tutti i membri.  
  
-   Non è possibile creare direttamente un'istanza di un'interfaccia. I membri vengono implementati da qualsiasi classe o struct che implementa l'interfaccia.  
  
-   Le interfacce possono contenere eventi, indicizzatori, metodi e proprietà.  
  
-   Le interfacce non contengono implementazioni di metodi.  
  
-   Una classe o struct può implementare più interfacce. Una classe può ereditare una classe base e anche implementare una o più interfacce.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Implementazione esplicita dell'interfaccia](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md)  
 Illustra come creare un membro di una classe specifico di un'interfaccia.  
  
 [Procedura: Implementare in modo esplicito i membri di interfaccia](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-interface-members.md)  
 Fornisce un esempio di come implementare in modo esplicito i membri delle interfacce.  
  
 [Procedura: Implementare in modo esplicito i membri di due interfacce](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md)  
 Fornisce un esempio di come implementare in modo esplicito i membri delle interfacce con l'ereditarietà.  
  
##  <a name="BKMK_RelatedSections"></a> Sezioni correlate  
  
-   [Proprietà dell'interfaccia](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)  
  
-   [Indicizzatori nelle interfacce](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)  
  
-   [Procedura: Implementare eventi di interfaccia](../../../csharp/programming-guide/events/how-to-implement-interface-events.md)  
  
-   [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)  
  
-   [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)  
  
-   [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)  
  
-   [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)  
  
-   [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)  
  
-   [Eventi](../../../csharp/programming-guide/events/index.md)  
  
-   [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)  
  
## <a name="featured-book-chapter"></a>Capitoli del libro rappresentati  
 [Interfaces](http://msdn.microsoft.com/library/orm-9780596521066-01-13.aspx) in [Learning C# 3.0: Master the Fundamentals of C# 3.0](http://msdn.microsoft.com/library/orm-9780596521066-01.aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)

