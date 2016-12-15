---
title: "Module &lt;keyword&gt; (Visual Basic) | Microsoft Docs"
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
  - "vb.ModuleAttribute"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Module keyword"
  - "Module modifier"
  - "attribute blocks, Module keyword"
ms.assetid: d971b940-05ab-4d56-8485-e3b8a661906b
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Module &lt;keyword&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che un attributo all'inizio di un file di origine viene applicato al modulo in assembly corrente.  
  
## Note  
 Diversi attributi sono relativi a un singolo elemento di programmazione, quale una classe o una proprietà.  Per applicare questo tipo di attributo, collegare il blocco di attributi, racchiuso tra parentesi angolari \(`< >`\), direttamente all'istruzione per la dichiarazione.  
  
 Se un attributo è relativo non solo all'elemento che segue ma anche al modulo in assembly corrente, è possibile posizionare il blocco attributi all'inizio del file di origine e identificare l'attributo con la parola chiave `Module`.  Se l'attributo è relativo all'intero assembly, è possibile utilizzare la parola chiave [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md).  
  
 Il modificatore `Module` non corrisponde all'[Module Statement](../../../visual-basic/language-reference/statements/module-statement.md).  
  
## Vedere anche  
 [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md)   
 [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md)   
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)