---
title: "&lt;c&gt; (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "c XML tag"
  - "<c> XML tag"
ms.assetid: 36ad5d1b-11f7-4012-8932-41962ac327d1
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;c&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

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