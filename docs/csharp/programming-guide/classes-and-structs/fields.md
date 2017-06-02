---
title: Campi (Guida per programmatori C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- fields [C#]
ms.assetid: 3cbb2f61-75f8-4cce-b4ef-f5d1b3de0db7
caps.latest.revision: 29
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
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1e5b1880e6821b2fd4595baad31f7a1bd5599ac4
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="fields-c-programming-guide"></a>Campi (Guida per programmatori C#)
Un *campo* è una variabile di qualsiasi tipo che viene dichiarata direttamente in una [classe](../../../csharp/language-reference/keywords/class.md) o [struct](../../../csharp/language-reference/keywords/struct.md). I campi sono *membri* del rispettivo tipo contenitore.  
  
 Una classe o struct può includere campi di istanza, campi statici o entrambi. I campi di istanza sono specifici di un'istanza di tipo. Se si ha una classe T con un campo di istanza F, è possibile creare due oggetti di tipo T e modificare il valore di F in ciascun oggetto senza modificare il valore nell'altro oggetto. Al contrario, un campo statico appartiene alla classe stessa ed è condiviso tra tutte le istanze della classe. Le modifiche apportate dall'istanza A saranno visibili immediatamente alle istanze B e C se accedono al campo.  
  
 In genere è necessario usare i campi solo per le variabili che hanno accesso privato o protetto. I dati che la classe espone al codice client devono essere forniti tramite [metodi](../../../csharp/programming-guide/classes-and-structs/methods.md), [proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md) e [indicizzatori](../../../csharp/programming-guide/indexers/index.md). Usando questi costrutti per l'accesso indiretto ai campi interni, è possibile evitare valori di input non validi. Un campo privato che archivia i dati esposti da una proprietà pubblica è chiamato *archivio di backup* o *campo sottostante*.  
  
 Di solito i campi archiviano dati che devono essere accessibili a più metodi della classe e devono essere archiviati per un tempo maggiore rispetto alla durata di ogni singolo metodo. Ad esempio, una classe che rappresenta una data di calendario potrebbe contenere tre campi interi: uno per il mese, uno per il giorno e uno per l'anno. Le variabili che vengono usate solo all'interno dell'ambito di un singolo metodo devono essere dichiarate come *variabili locali* all'interno del corpo del metodo stesso.  
  
 I campi vengono dichiarati nel blocco della classe, specificando il livello di accesso del campo, seguito dal tipo di campo e poi dal nome del campo. Ad esempio:  
  
 [!code-cs[csProgGuideObjects#61](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/fields_1.cs)]  
  
 Per accedere a un campo in un oggetto, aggiungere un punto dopo il nome dell'oggetto, seguito dal nome del campo, come in `objectname.fieldname`. Ad esempio:  
  
 [!code-cs[csProgGuideObjects#62](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/fields_2.cs)]  
  
 È possibile assegnare a un campo un valore iniziale usando l'operatore di assegnazione quando il campo viene dichiarato. Per assegnare automaticamente il campo `day` a `"Monday"`, ad esempio, è necessario dichiarare `day` come nell'esempio seguente:  
  
 [!code-cs[csProgGuideObjects#63](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/fields_3.cs)]  
  
 I campi vengono inizializzati immediatamente prima della chiamata del costruttore per l'istanza dell'oggetto. Se il costruttore assegna il valore di un campo, sovrascriverà qualsiasi valore assegnato nella dichiarazione del campo. Per altre informazioni, vedere [Uso dei costruttori](../../../csharp/programming-guide/classes-and-structs/using-constructors.md).  
  
> [!NOTE]
>  Un inizializzatore di campo non può fare riferimento ad altri campi di istanza.  
  
 I campi possono essere contrassegnati come [public](../../../csharp/language-reference/keywords/public.md), [private](../../../csharp/language-reference/keywords/private.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o `protected internal`. Questi modificatori di accesso definiscono in che modo gli utenti della classe possono accedere ai campi. Per altre informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 È possibile facoltativamente dichiarare un campo come [static](../../../csharp/language-reference/keywords/static.md). Questo rende il campo disponibile per i chiamanti in qualsiasi momento, anche se non esiste alcuna istanza della classe. Per altre informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 È possibile dichiarare un campo come [readonly](../../../csharp/language-reference/keywords/readonly.md). A un campo di sola lettura può essere assegnato un valore solo durante l'inizializzazione o in un costruttore. Un campo `static``readonly` è molto simile a una costante, a parte il fatto che il compilatore C# non ha accesso al valore di un campo statico di sola lettura in fase di compilazione, ma solo in fase di esecuzione. Per altre informazioni, vedere [Costanti](../../../csharp/programming-guide/classes-and-structs/constants.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Uso dei costruttori](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)
