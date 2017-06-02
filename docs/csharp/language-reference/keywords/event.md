---
title: event (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- event
- remove
- event_CSharpKeyword
- add
dev_langs:
- CSharp
helpviewer_keywords:
- event keyword [C#]
ms.assetid: 7858fd85-153b-4259-85d0-6aa13c35f174
caps.latest.revision: 28
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
ms.openlocfilehash: 60a6322f8e120c6a443638b4f6e409acdfa0b235
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="event-c-reference"></a>event (Riferimenti per C#)
La parola chiave `event` viene usata per dichiarare un evento in una classe autore.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come dichiarare e generare un evento che usa <xref:System.EventHandler> come tipo delegate sottostante. Per l'esempio di codice completo in cui viene illustrato come usare il tipo delegate generico <xref:System.EventHandler%601> e come sottoscrivere un evento e creare un metodo per la gestione eventi, vedere [Procedura: Pubblicare eventi conformi alle linee guida di .NET Framework](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md).  
  
 [!code-cs[csrefKeywordsModifiers#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/event_1.cs)]  
  
 Gli eventi sono un tipo di delegati multicast speciali che possono essere chiamati solo dall'interno della classe o dello struct in cui sono dichiarati (la classe autore). Se altre classi o altri struct sottoscrivono l'evento, i metodi di gestione eventi corrispondenti verranno chiamati quando la classe publisher genera l'evento. Per altre informazioni e altri esempi di codice, vedere [Eventi](../../../csharp/programming-guide/events/index.md) e [Delegati](../../../csharp/programming-guide/delegates/index.md).  
  
 Gli eventi possono essere contrassegnati come [public](../../../csharp/language-reference/keywords/public.md), [private](../../../csharp/language-reference/keywords/private.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o `protected``internal`. Questi modificatori di accesso definiscono in che modo gli utenti della classe possono accedere all'evento. Per altre informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
## <a name="keywords-and-events"></a>Parole chiave ed eventi  
 Agli eventi si applicano le parole chiave seguenti.  
  
|Parola chiave|Descrizione|Per altre informazioni|  
|-------------|-----------------|--------------------------|  
|[static](../../../csharp/language-reference/keywords/static.md)|Rende l'evento disponibile per i chiamanti in qualsiasi momento, anche se non esiste alcuna istanza della classe.|[Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)|  
|[virtual](../../../csharp/language-reference/keywords/virtual.md)|Consente alle classi derivate di eseguire l'override del comportamento dell'evento tramite la parola chiave [override](../../../csharp/language-reference/keywords/override.md).|[Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)|  
|[sealed](../../../csharp/language-reference/keywords/sealed.md)|Specifica che per le classi derivate l'evento non è più virtuale.||  
|[abstract](../../../csharp/language-reference/keywords/abstract.md)|Il compilatore non genererà i blocchi di funzioni di accesso degli eventi `add` e `remove` e pertanto le classi derivate dovranno fornire la propria implementazione.||  
  
 Un evento può essere dichiarato statico mediante la parola chiave [static](../../../csharp/language-reference/keywords/static.md). Ciò rende l'evento disponibile per i chiamanti in qualsiasi momento, anche se non esiste alcuna istanza della classe. Per altre informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 Un evento può essere contrassegnato come virtuale mediante la parola chiave [virtual](../../../csharp/language-reference/keywords/virtual.md). Ciò consente alle classi derivate di eseguire l'override del comportamento dell'evento tramite la parola chiave [override](../../../csharp/language-reference/keywords/override.md). Per altre informazioni, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md). Un evento che esegue l'override di un evento virtuale può anche essere contrassegnato come [sealed](../../../csharp/language-reference/keywords/sealed.md), in modo che non risulti più virtuale per le classi derivate. Infine, un evento può essere dichiarato [abstract](../../../csharp/language-reference/keywords/abstract.md), in modo che il compilatore non generi blocchi di funzioni di accesso agli eventi `add` e `remove`. Le classi derivate devono pertanto fornire la propria implementazione.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [add](../../../csharp/language-reference/keywords/add.md)   
 [remove](../../../csharp/language-reference/keywords/remove.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [Procedura: Combinare delegati (delegati multicast)](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)
