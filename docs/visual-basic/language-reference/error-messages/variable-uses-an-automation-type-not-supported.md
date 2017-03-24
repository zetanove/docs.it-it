---
title: La variabile utilizza un tipo di automazione non supportato in Visual Basic | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID458
dev_langs:
- VB
ms.assetid: bde4f4da-493b-452c-b6e4-1d370edba4cd
caps.latest.revision: 12
author: stevehoag
ms.author: shoag
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 58403a9aacc00e659807aff83031fe2ac80bbb40
ms.lasthandoff: 03/13/2017

---
# <a name="variable-uses-an-automation-type-not-supported-in-visual-basic"></a>La variabile utilizza un tipo di automazione non supportato in Visual Basic
Si è tentato di utilizzare una variabile definita in una libreria dei tipi o oggetti con un tipo di dati non supportato da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Utilizzare una variabile di tipo riconosciuto da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
     -oppure-  
  
-   Se questo errore si verifica durante l'utilizzo di `FileGet` o `FileGetOBject`, assicurarsi che il file si sta tentando di utilizzare è stato scritto con `FilePut` o `FilePutObject`.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../visual-basic/language-reference/data-types/data-type-summary.md)
