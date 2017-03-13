---
title: "&lt;c&gt; (Visual Basic) | Microsoft Docs"
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
  - "c XML tag"
  - "<c> XML tag"
ms.assetid: 36ad5d1b-11f7-4012-8932-41962ac327d1
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# &lt;c&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica che il testo all'interno di una descrizione è codice.  
  
## Sintassi  
  
```  
<c>text</c>  
```  
  
#### Parametri  
  
|||  
|-|-|  
|Parametro|Descrizione|  
|`text`|Testo che si desidera indicare come codice.|  
  
## Note  
 Il tag `<c>` consente di specificare che il testo di una descrizione deve essere contrassegnato come codice.  Utilizzare [\<code\>](../../../visual-basic/language-reference/xmldoc/code.md) per indicare più righe come codice.  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 Nell'esempio riportato di seguito il tag `<c>` viene utilizzato nella sezione del riepilogo per indicare che `Counter` è codice.  
  
 [!code-vb[VbVbcnXmlDocComments#1](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/c_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)