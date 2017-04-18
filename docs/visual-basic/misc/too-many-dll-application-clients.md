---
title: Troppe applicazioni client DLL | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID47
ms.assetid: 4b87780b-67ad-4c96-9253-db954a751dad
caps.latest.revision: 8
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1abc9ce574de00db42a33cde478ca80be74e61ff
ms.lasthandoff: 03/13/2017

---
# <a name="too-many-dll-application-clients"></a>Troppe applicazioni client DLL
La libreria di collegamento dinamico (DLL) per [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] supporta solo l'accesso a un numero limitato di applicazioni host. L'applicazione e altre applicazioni che sono [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] host (alcuni dei quali è accessibile dall'applicazione) sta tentando di accedere il [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] DLL nello stesso momento.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Ridurre il numero di applicazioni aperte che accedono a [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di errore](../../visual-basic/programming-guide/language-features/error-types.md)
