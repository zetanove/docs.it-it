---
title: Errore di automazione | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID440
dev_langs:
- VB
ms.assetid: 2c4be5c5-2f0d-4a2b-96fe-d1b24f08fc4c
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 0e48d5bde8b0fd3d31265d3d287623e32c0ea4cf
ms.lasthandoff: 03/13/2017

---
# <a name="automation-error"></a>Errore di automazione
Si è verificato un errore durante l'esecuzione di un metodo o durante il recupero o l'impostazione di una proprietà di una variabile oggetto. L'errore è stato segnalato dall'applicazione che ha creato l'oggetto.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Verificare le proprietà dell'oggetto `Err` per determinare l'origine e la natura dell'errore.  
  
2.  Usare l'istruzione `On Error Resume Next` immediatamente prima dell'istruzione di accesso e quindi controllare subito la presenza di errori dopo l'istruzione di accesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di errore](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [Comunicazioni con Microsoft](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
