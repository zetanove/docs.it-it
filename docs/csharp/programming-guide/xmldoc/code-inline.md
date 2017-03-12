---
title: "&lt;c&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
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
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# &lt;c&gt; (Guida per programmatori C#)
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
 [!code-cs[csProgGuideDocComments#2](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/code-inline_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)