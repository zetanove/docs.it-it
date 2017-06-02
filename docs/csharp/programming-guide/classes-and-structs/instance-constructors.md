---
title: Costruttori di istanze (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- constructors [C#], instance constructors
- instance constructors [C#]
ms.assetid: 24663779-c1e5-4af4-a942-ca554e4c542d
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
ms.openlocfilehash: 5c579c28c6b298cc0aefe0cb9eb41993b84a23d8
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="instance-constructors-c-programming-guide"></a>Costruttori di istanze (Guida per programmatori C#)
I costruttori di istanze vengono usati per creare e inizializzare qualsiasi variabile membro di istanza quando si usa l'espressione [new](../../../csharp/language-reference/keywords/new.md) per creare un oggetto di una [classe](../../../csharp/language-reference/keywords/class.md). Per inizializzare una classe [statica](../../../csharp/language-reference/keywords/static.md), o variabili statiche in una classe non statica, è necessario definire un costruttore statico. Per altre informazioni, vedere [Costruttori statici](../../../csharp/programming-guide/classes-and-structs/static-constructors.md).  
  
 Nell'esempio seguente viene illustrato un costruttore di istanze:  
  
 [!code-cs[csProgGuideObjects#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_1.cs)]  
  
> [!NOTE]
>  Per maggior chiarezza, questa classe contiene campi pubblici. L'uso di campi pubblici non è una procedura di programmazione consigliata, perché consente a qualsiasi metodo in qualsiasi punto di un programma di accedere senza restrizioni e senza verifiche ai componenti interni di un oggetto. I membri dati in genere devono essere privati e l'accesso ad essi deve essere consentito solo tramite metodi e proprietà della classe.  
  
 Questo costruttore di istanze viene chiamato ogni volta che viene creato un oggetto basato sulla classe `CoOrds`. Un costruttore come questo, che non accetta argomenti, viene chiamato *costruttore predefinito*. È spesso utile, tuttavia, per fornire costruttori aggiuntivi. È ad esempio possibile aggiungere un costruttore alla classe `CoOrds` che consente di specificare i valori iniziali dei membri dati:  
  
 [!code-cs[csProgGuideObjects#76](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_2.cs)]  
  
 Ciò consente di creare oggetti `CoOrd` con valori iniziali predefiniti o specifici, come illustrato di seguito:  
  
 [!code-cs[csProgGuideObjects#77](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_3.cs)]  
  
 Se una classe non ha un costruttore, viene generato automaticamente un costruttore predefinito e per inizializzare i campi dell'oggetto vengono usati i valori predefiniti. Ad esempio, un valore [int](../../../csharp/language-reference/keywords/int.md) viene inizializzato su 0. Per altre informazioni sui valori predefiniti, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md). Poiché il costruttore predefinito della classe `CoOrds` inizializza tutti i membri dati su zero, può pertanto essere rimosso completamente senza modificare il funzionamento della classe. Per un esempio completo sull'uso di più costruttori, vedere l'esempio 1 più avanti in questo argomento. Per un esempio di costruttore generato automaticamente, vedere l'esempio 2.  
  
 I costruttori di istanze possono anche essere usati per chiamare i costruttori di istanze delle classi di base. Il costruttore di classi può chiamare il costruttore della classe di base mediante l'inizializzatore, ad esempio:  
  
 [!code-cs[csProgGuideObjects#78](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_4.cs)]  
  
 In questo esempio la classe `Circle` passa i valori che rappresentano il raggio e l'altezza al costruttore fornito da `Shape` da cui deriva `Circle`. Per un esempio completo sull'uso di `Shape` e `Circle` vedere l'esempio 3 di questo argomento.  
  
## <a name="example-1"></a>Esempio 1  
 L'esempio riportato di seguito illustra una classe con due costruttori di classi, uno senza argomenti e uno con due argomenti.  
  
 [!code-cs[csProgGuideObjects#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_5.cs)]  
  
## <a name="example-2"></a>Esempio 2  
 Nell'esempio riportato di seguito la classe `Person` non ha alcun costruttore. In questo caso viene fornito automaticamente un costruttore predefinito e i campi vengono inizializzati sui valori predefiniti.  
  
 [!code-cs[csProgGuideObjects#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_6.cs)]  
  
 Si noti che il valore predefinito di `age` è `0` e il valore predefinito di `name` è `null`. Per altre informazioni sui valori predefiniti, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md).  
  
## <a name="example-3"></a>Esempio 3  
 Nell'esempio riportato di seguito viene illustrato l'uso dell'inizializzatore della classe di base. La classe `Circle` è derivata dalla classe generale `Shape`e la classe `Cylinder` è derivata dalla classe `Circle`. Il costruttore di ogni classe derivata usa il relativo inizializzatore della classe di base.  
  
 [!code-cs[csProgGuideObjects#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/instance-constructors_7.cs)]  
  
 Per altri esempi su come chiamare i costruttori della classe di base, vedere [virtual](../../../csharp/language-reference/keywords/virtual.md), [override](../../../csharp/language-reference/keywords/override.md) e [base](../../../csharp/language-reference/keywords/base.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Finalizzatori](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [static](../../../csharp/language-reference/keywords/static.md)
