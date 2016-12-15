---
title: "Assembly (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Assembly"
  - "vb.AssemblyAttribute"
  - "Assembly"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Assembly modifier"
  - "Assembly keyword"
  - "attribute blocks, Assembly keyword"
ms.assetid: 925e7471-3bdf-4b51-bb93-cbcfc6efc52f
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Assembly (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che un attributo all'inizio di un file di origine viene applicato all'intero assembly.  
  
## Note  
 Diversi attributi sono relativi a un singolo elemento di programmazione, quale una classe o una proprietà.  Per applicare questo tipo di attributo, collegare il blocco di attributi, racchiuso tra parentesi angolari \(`< >`\), direttamente all'istruzione per la dichiarazione.  
  
 Se un attributo è relativo solo al seguente elemento ma non all'intero assembly, il blocco di attributi viene inserito all'inizio del file di origine e l'attributo viene identificato con la parola chiave `Assembly`.  Se è relativo al modulo dell'assembly corrente, utilizzare la parola chiave [Module](../../../visual-basic/language-reference/modifiers/module-keyword.md).  
  
 È possibile anche applicare un attributo a un assembly nel file AssemblyInfo.vb e in tal caso non è necessario utilizzare un blocco di attributi nel file del codice sorgente principale.  
  
## Vedere anche  
 [Module \<keyword\>](../../../visual-basic/language-reference/modifiers/module-keyword.md)   
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)