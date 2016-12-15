---
title: "/highentropyva (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "highentropyva compiler option (Visual Basic)"
  - "/highentropyva compiler option (Visual Basic)"
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /highentropyva (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Indica se un eseguibile a 64 bit o un eseguibile che è contrassegnato dall'opzione del compilatore di [\/platform: anycpu](../../../visual-basic/reference/command-line-compiler/platform.md) supporta l'ASLR \(ASLR\) elevato di entropia.  
  
## Sintassi  
  
```  
/highentropyva[+ | -]  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Parametro facoltativo.  L'opzione è disattivata per impostazione predefinita o se si specifica `/highentropyva-`.  L'opzione è attivata se si specifica `/highentropyva` o `/highentropyva+`.  
  
## Note  
 Se si specifica questa opzione, le versioni compatibili del kernel di windows possono utilizzare i livelli superiori di entropia quando il kernel randomizza il layout dello spazio degli indirizzi di un processo come parte di ASLR.  Se il kernel utilizza i livelli superiori di entropia, un numero maggiore degli indirizzi può essere allocata alle aree di memoria come gli stack e heap.  Di conseguenza, è più difficile indovinare la posizione di un'area di archiviazione specifico.  
  
 Quando l'opzione è attivata, l'eseguibile di destinazione e tutti i moduli da cui dipende siano in grado di gestire i valori di puntatore maggiori di 4 GB \(GB\) quando i moduli sono in esecuzione come processi a 64 bit.  
  
 Per ulteriori informazioni su ASLR, vedere [Vulnerabilità del software di attenuare](http://go.microsoft.com/fwlink/?LinkId=226234).  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)