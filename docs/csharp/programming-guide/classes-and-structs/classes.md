---
title: Classi (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- classes [C#]
- C# language, classes
ms.assetid: e8848524-7273-429f-8aba-c658d5eff5ad
caps.latest.revision: 40
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a5ed524a1b17f7be8903f998cbd732594faab831
ms.openlocfilehash: 1f327e7171df8b91d4c5a787c879069a4e44f562
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="classes-c-programming-guide"></a>Classi (Guida per programmatori C#)
Una *classe* è un costrutto che consente di creare tipi personalizzati raggruppando insieme variabili di altri tipi, metodi e eventi. Una classe è simile a un progetto. Definisce i dati e il comportamento di un tipo. Se la classe non è dichiarata come statica, il codice client può usarla creando *oggetti* o *istanze* che vengono assegnate a una variabile. La variabile rimane in memoria fino a quando tutti i riferimenti non escono dall'ambito. In questa fase, CLR la contrassegna come idonea per Garbage Collection. Se la classe viene dichiarata come [statica](../../../csharp/language-reference/keywords/static.md), viene mantenuta in memoria solo una copia e il codice client può accedervi solo tramite la classe stessa, non con una *variabile di istanza*. Per altre informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 Diversamente da struct, le classi supportano l'*ereditarietà*, una caratteristica fondamentale della programmazione orientata a oggetti. Per altre informazioni, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
## <a name="declaring-classes"></a>Dichiarazione di classi  
 Le classi vengono dichiarate usando la parola chiave [class](../../../csharp/language-reference/keywords/class.md), come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideObjects#79](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/classes_1.cs)]  
  
 La parola chiave `class` è preceduta dal livello di accesso. Poiché in questo caso viene usata la parola chiave [public](../../../csharp/language-reference/keywords/public.md), chiunque può creare oggetti da questa classe. Il nome della classe segue la parola chiave `class`. Il resto della definizione è il corpo della classe, in cui vengono definiti il comportamento e i dati. I campi, le proprietà, i metodi e gli eventi in una classe vengono collettivamente definiti *membri della classe*.  
  
## <a name="creating-objects"></a>Creazione di oggetti  
 Anche se vengono talvolta usati in modo intercambiabile, una classe e un oggetto sono elementi diversi. Una classe definisce un tipo di oggetto, ma non è un oggetto. Un oggetto è un'entità concreta ed è basato su una classe. Talvolta si fa riferimento all'oggetto come istanza di una classe.  
  
 Gli oggetti possono essere creati tramite la parola chiave [new](../../../csharp/language-reference/keywords/new.md) seguita dal nome della classe su cui si baserà l'oggetto, nel modo seguente:  
  
 [!code-cs[csProgGuideObjects#80](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/classes_2.cs)]  
  
 Quando viene creata un'istanza di una classe, viene passato al programmatore un riferimento all'oggetto. Nell'esempio precedente, `object1` è un riferimento a un oggetto basato su `Customer`. Questo riferimento indica il nuovo oggetto, ma non contiene i dati dell'oggetto. Infatti, è possibile creare un riferimento all'oggetto senza creare un oggetto:  
  
 [!code-cs[csProgGuideObjects#81](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/classes_3.cs)]  
  
 Non è consigliabile creare riferimenti a oggetti come questo che non fanno riferimento a un oggetto reale perché il tentativo di accedere a un oggetto tramite tale riferimento avrà esito negativo in fase di esecuzione. Tuttavia, tale riferimento può essere creato per fare riferimento a un oggetto, creando un nuovo oggetto oppure assegnandolo a un oggetto esistente, come illustrato di seguito:  
  
 [!code-cs[csProgGuideObjects#82](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/classes_4.cs)]  
  
 Questo codice crea due riferimenti a oggetti che fanno entrambi riferimento allo stesso oggetto. Tutte le modifiche effettuate all'oggetto tramite `object3` si rifletteranno tuttavia nei successivi usi di `object4`. Poiché gli oggetti che si basano su classi vengono indicati tramite riferimenti, le classi sono note come tipi di riferimento.  
  
## <a name="class-inheritance"></a>Ereditarietà di classe  
 L'ereditarietà si ottiene usando una *derivazione*, vale a dire che una classe viene dichiarata usando una *classe di base* da cui eredita dati e comportamento. Una classe di base viene specificata tramite l'aggiunta di due punti e il nome della classe di base dopo il nome della classe derivata, nel modo seguente:  
  
 [!code-cs[csProgGuideObjects#83](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/classes_5.cs)]  
  
 Quando una classe dichiara una classe di base, eredita tutti i membri della classe di base, a eccezione dei costruttori.  
  
 Diversamente da C++, una classe di C# può ereditare direttamente solo da una classe di base. Tuttavia, poiché una classe di base può ereditare da un'altra classe, una classe può ereditare indirettamente più classi di base. Una classe può anche implementare direttamente più di un'interfaccia. Per altre informazioni, vedere [Interfacce](../../../csharp/programming-guide/interfaces/index.md).  
  
 Una classe può essere dichiarata come [astratta](../../../csharp/language-reference/keywords/abstract.md). Una classe astratta contiene metodi astratti che hanno una definizione di firma, ma senza implementazione. Non è possibile creare un'istanza di classi astratte. Le classi astratte possono essere usate solo tramite classi derivate che implementano i metodi astratti. Al contrario, una classe [sealed](../../../csharp/language-reference/keywords/sealed.md) non consente ad altre classi di derivare da tale classe. Per altre informazioni, vedere [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
 Le definizioni di classe possono essere suddivise tra file di origine diversa. Per altre informazioni, vedere [Classi e metodi parziali](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md).  
  
## <a name="description"></a>Descrizione  
 Nell'esempio seguente vengono definiti una classe pubblica che contiene un singolo campo, un metodo e un metodo speciale denominato costruttore. Per altre informazioni, vedere [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md). Viene quindi creata un'istanza alla classe con la parola chiave `new`.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuideObjects#84](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/classes_6.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Programmazione orientata ad oggetti](../concepts/object-oriented-programming.md)   
 [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)   
 [Membri](../../../csharp/programming-guide/classes-and-structs/members.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Finalizzatori](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [Oggetti](../../../csharp/programming-guide/classes-and-structs/objects.md)
