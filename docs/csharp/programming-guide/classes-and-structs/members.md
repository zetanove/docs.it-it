---
title: Membri (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- types [C#], nested types
- C# language, type members
ms.assetid: 4a30a4ab-d690-4936-9124-92ce9448665a
caps.latest.revision: 20
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
ms.openlocfilehash: 229955400c0c16cdc0069d6e45148d91d6253f9d
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="members-c-programming-guide"></a>Membri (Guida per programmatori C#)
Le classi e gli struct contengono membri che ne rappresentano i dati e il comportamento. I membri di una classe includono tutti i membri dichiarati nella classe, oltre a tutti i membri (ad eccezione di costruttori e finalizzatori) dichiarati in tutte le classi nella relativa gerarchia di ereditarietà. I membri privati nelle classi base vengono ereditati ma non sono accessibili dalle classi derivate.  
  
 Nella tabella seguente sono elencati i tipi di membri che possono essere contenuti in una classe o in uno struct:  
  
|Membro|Descrizione|  
|------------|-----------------|  
|[Campi](../../../csharp/programming-guide/classes-and-structs/fields.md)|I campi sono variabili dichiarate nell'ambito della classe. Un campo può essere un tipo numerico incorporato o un'istanza di un'altra classe. Una classe calendario può ad esempio avere un campo che contiene la data corrente.|  
|[Costanti](../../../csharp/programming-guide/classes-and-structs/constants.md)|Le costanti sono campi o proprietà il cui valore è impostato in fase di compilazione e non può essere modificato.|  
|[Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)|Le proprietà sono metodi di una classe ai quali si accede come se si trattasse di campi della classe. Possono garantire la sicurezza di un campo di una classe in modo da impedire che venga modificato all'insaputa dell'oggetto.|  
|[Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)|I metodi definiscono le azioni che una classe è in grado di eseguire. Possono accettare parametri che forniscono dati di input e restituire dati di output tramite i parametri. Possono anche restituire un valore direttamente, senza l'uso di parametri.|  
|[Eventi](../../../csharp/programming-guide/events/index.md)|Gli eventi forniscono notifiche ad altri oggetti su ciò che si verifica, ad esempio le operazioni di clic su pulsanti o il completamento corretto di un metodo. Vengono definiti e generati tramite i delegati.|  
|[Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)|Gli operatori di overload sono considerati membri della classe. Quando si esegue l'overload di un operatore, lo si definisce come metodo statico pubblico in una classe. Gli operatori predefiniti (`+`, `*`, `<` e così via) non sono considerati membri. Per altre informazioni, vedere [Operatori che supportano l'overload](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md).|  
|[Indicizzatori](../../../csharp/programming-guide/indexers/index.md)|Gli indicizzatori consentono di eseguire l'indicizzazione di un oggetto in modo simile a quanto avviene per le matrici.|  
|[Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)|I costruttori sono metodi che vengono chiamati la prima volta che viene creato l'oggetto. Vengono spesso usati per inizializzare i dati di un oggetto.|  
|[Finalizzatori](../../../csharp/programming-guide/classes-and-structs/destructors.md)|I finalizzatori vengono usati molto raramente in C#. Questi sono metodi che vengono chiamati dal motore di esecuzione di runtime quando l'oggetto sta per essere rimosso dalla memoria. Vengono in genere usati per assicurarsi che le eventuali risorse da rilasciare vengano gestite nel modo appropriato.|  
|[Tipi annidati](../../../csharp/programming-guide/classes-and-structs/nested-types.md)|I tipi nidificati sono tipi dichiarati all'interno di un altro tipo. Vengono spesso usati per descrivere gli oggetti usati solo dai tipi che li contengono.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Finalizzatori](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Campi](../../../csharp/programming-guide/classes-and-structs/fields.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Tipi nidificati](../../../csharp/programming-guide/classes-and-structs/nested-types.md)   
 [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)   
 [Operatori che supportano l'overload](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)
