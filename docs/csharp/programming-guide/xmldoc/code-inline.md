---
title: "&lt;c&gt; (Guida per programmatori C#) | Microsoft Docs"
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
  - "c"
  - "<c>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<c> (tag XML C#)"
  - "c (tag XML C#)"
  - "codice, contrassegno di testo come [C#]"
  - "testo, contrassegno come codice [C#]"
ms.assetid: aad5b16e-a29e-445e-bd0d-eea0b138d7b2
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;c&gt; (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## Sintassi  
  
```  
<c>text</c>  
```  
  
#### Parametri  
 `text`  
 Testo che si desidera indicare come codice.  
  
## Note  
 Il tag \<c\> consente di specificare che il testo di una descrizione deve essere contrassegnato come codice.  Per indicare più righe come codice, utilizzare [\<code\>](../../../csharp/programming-guide/xmldoc/code.md).  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#2](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/code-inline_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)