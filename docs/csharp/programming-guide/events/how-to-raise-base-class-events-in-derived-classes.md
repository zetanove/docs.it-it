---
title: 'Procedura: Generare eventi della classe base in classi derivate (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- events [C#], in derived classes
ms.assetid: 2d20556a-0aad-46fc-845e-f85d86ea617a
caps.latest.revision: 24
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
ms.openlocfilehash: 4f3990959bb62676562dc21e1e5eabfb8ead20d5
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-raise-base-class-events-in-derived-classes-c-programming-guide"></a>Procedura: generare eventi della classe base in classi derivate (Guida per programmatori C#)
L'esempio seguente illustra il metodo standard di dichiarazione degli eventi in una classe base in modo che possano essere generati anche dalle classi derivate. Questo modello è usato spesso nelle classi Windows Forms nella libreria di classi [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
 Quando si crea una classe che può essere usata come classe base di altre classi, è necessario tenere presente che gli eventi sono un tipo speciale di delegati che possono essere richiamati solo dall'interno della classe che li ha dichiarati. Le classi derivate non possono richiamare direttamente gli eventi dichiarati all'interno della classe base. Nonostante sia necessario a volte un evento che possa essere generato solo dalla classe base, nella maggior parte dei casi è opportuno consentire alla classe derivata di richiamare eventi della classe base. A tale scopo, è possibile creare un metodo di chiamata protetto nella classe base che esegue il wrapping dell'evento. Le classi derivate possono richiamare indirettamente l'evento richiamando o eseguendo l'override di questo metodo di chiamata.  
  
> [!NOTE]
>  Non dichiarare eventi virtuali in una classe base ed eseguire l'override in una classe derivata. Il compilatore C# non è in grado di gestirli correttamente e non è possibile prevedere se un sottoscrittore dell'evento derivato sottoscriverà effettivamente l'evento della classe base.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuideEvents#1](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-raise-base-class-events-in-derived-classes_1.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Creazione di gestori eventi in Windows Form](https://msdn.microsoft.com/library/dacysss4.aspx)
