---
title: "&lt;code&gt; (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "code XML tag"
  - "<code> XML tag"
ms.assetid: 925e5342-be05-45f2-bf66-7398bbd6710e
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# &lt;code&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica che il testo è composto da più righe di codice.  
  
## Sintassi  
  
```  
<code>content</code>  
```  
  
#### Parametri  
 `content`  
 Testo da contrassegnare come codice.  
  
## Note  
 Utilizzare il tag `<code>` per indicare più righe come codice.  Utilizzare [\<c\>](../../../visual-basic/language-reference/xmldoc/c.md) per indicare che il testo incluso in una descrizione deve essere contrassegnato come codice.  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 Nell'esempio riportato di seguito il tag \<code\> viene utilizzato per includere un esempio di codice relativo all'utilizzo del campo `ID`.  
  
 [!code-vb[VbVbcnXmlDocComments#2](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/code_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)