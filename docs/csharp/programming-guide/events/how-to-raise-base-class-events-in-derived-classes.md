---
title: "Procedura: generare eventi della classe base in classi derivate (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "eventi [C#], in classi derivate"
ms.assetid: 2d20556a-0aad-46fc-845e-f85d86ea617a
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# Procedura: generare eventi della classe base in classi derivate (Guida per programmatori C#)
Nell'esempio seguente viene illustrato il metodo standard di dichiarare eventi in una classe base in modo che possano essere generati anche dalle classi derivate.  Questo modello è utilizzato spesso nelle classi Windows Forms nella libreria delle classi di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  
  
 Quando si crea una classe che può essere utilizzata come classe base per altre classi, è necessario tenere presente che gli eventi sono un tipo speciale di delegati che possono essere richiamati solo dall'interno della classe che li ha dichiarati.  Le classi derivate non possono richiamare direttamente gli eventi dichiarati all'interno della classe base.  Nonostante sia necessario a volte un evento che possa essere generato solo dalla classe base, nella maggior parte dei casi è opportuno consentire alla classe derivata di richiamare eventi della classe base.  A tale scopo, è possibile creare un metodo di chiamata protetto nella classe base che esegue il wrapping dell'evento.  Le classi derivate possono richiamare indirettamente l'evento richiamando o ignorando questo metodo di chiamata.  
  
> [!NOTE]
>  Non dichiarare eventi virtuali in una classe base ed eseguire l'override in una classe derivata.  Il compilatore c\# non è in grado di gestirli correttamente e non è possibile prevedere se un sottoscrittore dell' evento derivato sottoscriverà effettivamente l'evento della classe base.  
  
## Esempio  
 [!code-cs[csProgGuideEvents#1](../../../csharp/programming-guide/events/codesnippet/csharp/how-to-raise-base-class-_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Creating Event Handlers in Windows Forms](../Topic/Creating%20Event%20Handlers%20in%20Windows%20Forms.md)