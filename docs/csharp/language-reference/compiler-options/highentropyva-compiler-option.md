---
title: "/highentropyva (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/highentropyva"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/highentropyva compiler option [C#]"
  - "-highentropyva compiler option [C#]"
  - "highentropyva compiler option [C#]"
ms.assetid: eaf409b3-384e-49dd-9417-62453658f421
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /highentropyva (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione del compilatore **\/highentropyva** indica al kernel di Windows se un particolare eseguibile supporta ASLR \(Address Space Layout Randomization\) ad elevata entropia.  
  
## Sintassi  
  
```  
/highentropyva[+ | -]  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Questa opzione specifica che un eseguibile a 64\-bit o un eseguibile contrassegnata dall'opzione del compilatore [\/platform:anycpu](../../../csharp/language-reference/compiler-options/platform-compiler-option.md) supporta uno spazio degli indirizzi virtuali ad entropia elevata.  L'opzione è disabilitata per impostazione predefinita.  Utilizzare **\/highentropyva\+** o **\/highentropyva** per abilitarla.  
  
## Note  
 L'opzione **\/highentropyva** consente alle versioni precedenti del kernel di Windows di utilizzare i livelli superiori di entropia quando randomizza il layout dello spazio degli indirizzi di un processo come parte di ASLR.  Utilizzando i livelli superiori di entropia indica che un numero maggiore degli indirizzi può essere allocato alle aree di memoria come gli stack e heap.  Pertanto, è più difficile indovinare la posizione di un'area di archiviazione specifica.  
  
 Quando l'opzione del compilatore **\/highentropyva** è specificata, l'eseguibile di destinazione e tutti i moduli da cui dipende devono essere in grado di gestire i valori di puntatore maggiori di 4 gigabyte \(GB\) quando sono in esecuzione processi a 64 bit.  
  
 Per ulteriori informazioni su ASLR, vedere [Riduzione delle Vulnerabilità Software](http://go.microsoft.com/fwlink/?LinkId=226234).