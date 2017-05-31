---
title: -highentropyva (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /highentropyva
dev_langs:
- CSharp
helpviewer_keywords:
- /highentropyva compiler option [C#]
- -highentropyva compiler option [C#]
- highentropyva compiler option [C#]
ms.assetid: eaf409b3-384e-49dd-9417-62453658f421
caps.latest.revision: 8
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
ms.openlocfilehash: c1b49faa2fb388b330c24bdff28d00872828b110
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="highentropyva-c-compiler-options"></a>/highentropyva (opzioni del compilatore C#)
L'opzione del compilatore **/highentropyva** indica al kernel di Windows se un particolare eseguibile supporta la funzionalità ASLR (Address Space Layout Randomization) a entropia elevata.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>Argomenti  
 `+` &#124; `-`  
 Con questa opzione viene specificato che un eseguibile a 64 bit o un eseguibile contrassegnato dall'opzione del compilatore [/platform:anycpu](../../../csharp/language-reference/compiler-options/platform-compiler-option.md) supporta uno spazio degli indirizzi virtuali a entropia elevata. L'opzione è disabilitata per impostazione predefinita. Per abilitarla, usare **/highentropyva+** o **/highentropyva**.  
  
## <a name="remarks"></a>Note  
 Con l'opzione **/highentropyva**, nelle versioni compatibili del kernel di Windows è possibile usare livelli di entropia più elevati per la scelta casuale del layout dello spazio degli indirizzi di un processo in quanto parte di ASLR. L'utilizzo di livelli più elevati di entropia indica la possibilità di allocare un numero maggiore di indirizzi ad aree della memoria quali stack e heap. Di conseguenza, è più difficile indovinare la posizione di una determinata area di memoria.  
  
 Quando l'opzione del compilatore **/highentropyva** è specificata, l'eseguibile di destinazione e tutti i moduli da cui dipende devono essere in grado di gestire i valori di puntatore maggiori di 4 gigabyte (GB) quando sono in esecuzione come processi a 64 bit.
