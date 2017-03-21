---
title: /highentropyva (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- highentropyva compiler option (Visual Basic)
- /highentropyva compiler option (Visual Basic)
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
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
ms.openlocfilehash: 34987930b3afd6d95d12190172a5a5e512106f8a
ms.lasthandoff: 03/13/2017

---
# <a name="highentropyva-visual-basic"></a>/highentropyva (Visual Basic)
Indica se un eseguibile a 64 bit o che è contrassegnato per la [/platform: anycpu](../../../visual-basic/reference/command-line-compiler/platform.md) l'opzione del compilatore supporta un'entropia elevata Address Space Layout Randomization (ASLR).  
  
## <a name="syntax"></a>Sintassi  
  
```  
/highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>Argomenti  
 `+` &#124; `-`  
 Facoltativo. L'opzione è disattivata per impostazione predefinita o se si specifica `/highentropyva-`. L'opzione è abilitata se si specifica `/highentropyva` o `/highentropyva+`.  
  
## <a name="remarks"></a>Note  
 Se si specifica questa opzione, versioni compatibili del kernel di Windows possono utilizzare livelli più elevati di entropia quando il kernel genera casualmente del layout dello spazio di indirizzi di un processo come parte di ASLR. Se il kernel utilizza livelli più elevati di entropia, un numero maggiore di indirizzi da allocare aree della memoria quali stack e heap. Di conseguenza, è più difficile indovinare la posizione di una determinata area di memoria.  
  
 Quando l'opzione è on, l'eseguibile di destinazione e tutti i moduli in cui esso dipende deve essere in grado di gestire i valori di puntatore sono maggiori di 4 gigabyte (GB) quando questi moduli vengono eseguiti come processi a 64 bit.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
