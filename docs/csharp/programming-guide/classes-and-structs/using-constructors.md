---
title: Uso dei costruttori (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- constructors [C#], about constructors
ms.assetid: 464253b2-fd5d-469a-836d-df0fdf2a43f7
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
ms.openlocfilehash: 47103d13a68c5250c33dbca3e89de2f1f3e13449
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="using-constructors-c-programming-guide"></a>Utilizzo di costruttori (Guida per programmatori C#)
Quando si crea una [classe](../../../csharp/language-reference/keywords/class.md) o uno [struct](../../../csharp/language-reference/keywords/struct.md) viene chiamato il relativo costruttore. I costruttori hanno lo stesso nome della classe o dello struct e in genere inizializzano i membri dati del nuovo oggetto.  
  
 Nell'esempio seguente viene definita una classe denominata `Taxi` usando un costruttore semplice. Viene quindi creata un'istanza per la classe con l'operatore [new](../../../csharp/language-reference/keywords/new.md). Il costruttore `Taxi` viene richiamato dall'operatore `new` immediatamente dopo l'allocazione della memoria per il nuovo oggetto.  
  
 [!code-cs[csProgGuideObjects#53](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_1.cs)]  
  
 Un costruttore che non accetta parametri è detto *costruttore predefinito*. I costruttori predefiniti vengono richiamati ogni volta che si crea un'istanza per un oggetto usando l'operatore `new` e non sono specificati argomenti per `new`. Per altre informazioni, vedere [Costruttori di istanze](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md).  
  
 A meno che la classe sia [statica](../../../csharp/language-reference/keywords/static.md), le classi senza costruttori ricevono un costruttore predefinito pubblico dal compilatore C# per consentire la creazione di istanze di classi. Per altre informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 È possibile impedire che venga creata un'istanza per una classe rendendo il costruttore privato, come indicato di seguito:  
  
 [!code-cs[csProgGuideObjects#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_2.cs)]  
  
 Per altre informazioni, vedere [Costruttori privati](../../../csharp/programming-guide/classes-and-structs/private-constructors.md).  
  
 I costruttori per i tipi [struct](../../../csharp/language-reference/keywords/struct.md) sono simili ai costruttori di classi, ma gli `structs` non possono contenere un costruttore predefinito esplicito poiché ne viene specificato automaticamente uno dal compilatore. Questo costruttore inizializza ogni campo dello `struct` sui valori predefiniti. Per altre informazioni, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md). Il costruttore predefinito viene tuttavia richiamato solo se si crea un'istanza per lo `struct` con `new`. Ad esempio, questo codice usa il costruttore predefinito per <xref:System.Int32>, in modo da garantire che venga inizializzato l'Integer:  
  
```  
int i = new int();  
Console.WriteLine(i);  
```  
  
 Il codice seguente, tuttavia, provoca un errore del compilatore perché non usa `new` e poiché tenta di usare un oggetto che non è stato inizializzato:  
  
```  
int i;  
Console.WriteLine(i);  
```  
  
 In alternativa, gli oggetti basati su `structs`, inclusi tutti i tipi numerici incorporati, possono essere inizializzati o assegnati e quindi usati come nell'esempio seguente:  
  
```  
int a = 44;  // Initialize the value type...  
int b;  
b = 33;      // Or assign it before using it.  
Console.WriteLine("{0}, {1}", a, b);  
```  
  
 Quindi la chiamata al costruttore predefinito per un tipo di valore non è necessaria.  
  
 Sia le classi che gli `structs` possono definire costruttori che accettano parametri. I costruttori che accettano parametri devono essere chiamati con un'istruzione `new` o un'istruzione di [base](../../../csharp/language-reference/keywords/base.md). Le classi e gli `structs` possono inoltre definire più costruttori e non è necessario definire un costruttore predefinito. Ad esempio:  
  
 [!code-cs[csProgGuideObjects#54](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_3.cs)]  
  
 Questa classe può essere creata usando una delle istruzioni seguenti:  
  
 [!code-cs[csProgGuideObjects#55](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_4.cs)]  
  
 Un costruttore può usare la parola chiave `base` per chiamare il costruttore di una classe di base. Ad esempio:  
  
 [!code-cs[csProgGuideObjects#56](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_5.cs)]  
  
 In questo esempio il costruttore per la classe di base viene chiamato prima che venga eseguito il blocco per il costruttore. La parola chiave `base` può essere usata con o senza parametri. Tutti i parametri per il costruttore possono essere usati come parametri per `base` o come parte di un'espressione. Per altre informazioni, vedere [base](../../../csharp/language-reference/keywords/base.md).  
  
 In una classe derivata, se un costruttore di classe base non viene chiamato in modo esplicito usando la parola chiave `base`, il costruttore predefinito, se ne esiste uno, viene chiamato in modo implicito. Ciò significa quindi che le seguenti dichiarazioni del costruttore si equivalgono:  
  
 [!code-cs[csProgGuideObjects#58](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_6.cs)]  
  
 [!code-cs[csProgGuideObjects#57](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_7.cs)]  
  
 Se una classe di base non offre un costruttore predefinito, la classe derivata deve effettuare una chiamata esplicita a un costruttore di base usando `base`.  
  
 Un costruttore può richiamare un altro costruttore nello stesso oggetto usando la parola chiave [this](../../../csharp/language-reference/keywords/this.md). Come `base`, `this` può essere utilizzata con o senza parametri e gli eventuali parametri nel costruttore sono disponibili come parametri per `this` o come parte di un'espressione. Ad esempio, il secondo costruttore nell'esempio precedente può essere riscritto usando `this`:  
  
 [!code-cs[csProgGuideObjects#59](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_8.cs)]  
  
 L'uso della parola chiave `this` nell'esempio precedente causa la chiamata di questo costruttore:  
  
 [!code-cs[csProgGuideObjects#60](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_9.cs)]  
  
 I costruttori possono essere contrassegnati come [public](../../../csharp/language-reference/keywords/public.md), [private](../../../csharp/language-reference/keywords/private.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o `protected``internal`. Questi modificatori di accesso definiscono il modo in cui gli utenti della classe possono costruire la classe. Per altre informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 Un costruttore può essere dichiarato statico usando la parola chiave [static](../../../csharp/language-reference/keywords/static.md). I costruttori statici vengono chiamati automaticamente subito prima dell'accesso ai campi statici e in genere vengono usati per inizializzare i membri delle classi statiche. Per altre informazioni, vedere [Costruttori statici](../../../csharp/programming-guide/classes-and-structs/static-constructors.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Finalizzatori](../../../csharp/programming-guide/classes-and-structs/destructors.md)
