---
title: "event (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "event"
  - "remove"
  - "event_CSharpKeyword"
  - "add"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "event (parola chiave) [C#]"
ms.assetid: 7858fd85-153b-4259-85d0-6aa13c35f174
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# event (Riferimenti per C#)
La parola chiave `event` viene utilizzata per dichiarare un evento in una classe autore.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare e generare un evento che utilizza <xref:System.EventHandler> come tipo delegato sottostante.  Per l'esempio di codice completo in cui viene illustrato come utilizzare il tipo delegato generico <xref:System.EventHandler%601> e come sottoscrivere un evento e creare un metodo per la gestione eventi, vedere [Procedura: pubblicare eventi conformi alle linee guida di .NET Framework](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md).  
  
 [!code-cs[csrefKeywordsModifiers#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/event_1.cs)]  
  
 Gli eventi sono un tipo speciale di delegato multicast che possono essere richiamati solo dall'interno della classe o della struttura in cui sono dichiarati \(la classe autore\).  Se altre classi o strutture sottoscrivono l'evento, i metodi per la gestione eventi corrispondenti verranno chiamati quando la classe autore genera l'evento.  Per ulteriori informazioni ed esempi di codice, vedere [Eventi](../../../csharp/programming-guide/events/index.md) e [Delegati](../../../csharp/programming-guide/delegates/index.md).  
  
 Gli eventi possono essere contrassegnati come [public](../../../csharp/language-reference/keywords/public.md), [private](../../../csharp/language-reference/keywords/private.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o `protected` `internal`.  Questi modificatori definiscono le modalità di accesso all'evento per gli utenti della classe.  Per ulteriori informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
## Parole chiave ed eventi  
 Le parole chiave seguenti si riferiscono a eventi.  
  
|Parola chiave|Descrizione|Ulteriori informazioni|  
|-------------------|-----------------|----------------------------|  
|[static](../../../csharp/language-reference/keywords/static.md)|L'evento sarà sempre disponibile per i chiamanti, anche se non esistono istanze della classe.|[Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)|  
|[virtual](../../../csharp/language-reference/keywords/virtual.md)|Le classi derivate possono eseguire l'override del comportamento dell'evento utilizzando la parola chiave [override](../../../csharp/language-reference/keywords/override.md).|[Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)|  
|[sealed](../../../csharp/language-reference/keywords/sealed.md)|Specifica che per le classi derivate l'evento non è più virtuale.||  
|[abstract](../../../csharp/language-reference/keywords/abstract.md)|Il compilatore non genererà i blocchi di funzioni di accesso dell'evento `add` e `remove` e pertanto le classi derivate dovranno fornire la propria implementazione.||  
  
 Un evento può essere dichiarato statico mediante la parola chiave [static](../../../csharp/language-reference/keywords/static.md).  In questo modo l'evento risulterà sempre disponibile per i chiamanti, anche se non esistono istanze della classe.  Per ulteriori informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 Un evento può essere contrassegnato come virtuale mediante la parola chiave [virtual](../../../csharp/language-reference/keywords/virtual.md).  In questo modo le classi derivate possono eseguire l'override del comportamento dell'evento tramite la parola chiave [override](../../../csharp/language-reference/keywords/override.md).  Per ulteriori informazioni, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  Un evento che esegue l'override di un evento virtuale può anche essere contrassegnato come [sealed](../../../csharp/language-reference/keywords/sealed.md), in modo che non risulti più virtuale per le classi derivate.  Infine, un evento può essere dichiarato [abstract](../../../csharp/language-reference/keywords/abstract.md), in modo che il compilatore non generi blocchi di funzioni di accesso agli eventi `add` e `remove`.  Le classi derivate devono fornire pertanto le relative implementazioni.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [aggiunta](../../../csharp/language-reference/keywords/add.md)   
 [rimozione](../../../csharp/language-reference/keywords/remove.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [Procedura: combinare delegati multicast](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)