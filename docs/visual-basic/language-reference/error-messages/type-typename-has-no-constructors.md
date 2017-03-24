---
title: Tipo &quot;&lt;typename&gt;&quot; non ha costruttori | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30251
- vbc30251
dev_langs:
- VB
helpviewer_keywords:
- BC30251
ms.assetid: aff3e1df-abe6-4bc0-9abc-a1e70514c561
caps.latest.revision: 9
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
ms.openlocfilehash: 505e3bbdfa830394efcea7226897ec0d3e6d2b02
ms.lasthandoff: 03/13/2017

---
# <a name="type-39lttypenamegt39-has-no-constructors"></a>Tipo '&lt;typename&gt;' non ha costruttori
Un tipo non supporta una chiamata a `Sub New()`. Causa possibile: compilatore o un file binario danneggiato.  
  
 **ID errore:** BC30251  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Se il tipo si trova in un progetto diverso o in un file di riferimento, reinstallare il progetto o il file.  
  
2.  Se il tipo si trova nello stesso progetto, ricompilare l'assembly in cui è contenuto.  
  
3.  Se l'errore si ripresenta, reinstallare il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
4.  Se l'errore persiste, raccogliere informazioni sulla situazione contingente e informare il Servizio Supporto Tecnico Clienti Microsoft.  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti e classi](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Comunicazioni con Microsoft](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
