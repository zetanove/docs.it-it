---
title: "&lt;example&gt; (Visual Basic) | Microsoft Docs"
ms.custom: ""
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
  - "example XML tag"
  - "<example> XML tag"
ms.assetid: 90eeda1c-3fc4-427c-879c-5046d265a97c
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &lt;example&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica un esempio per il membro.  
  
## Sintassi  
  
```  
<example>description</example>  
```  
  
#### Parametri  
 `description`  
 Descrizione dell'esempio di codice.  
  
## Note  
 Il tag `<example>` consente di specificare un esempio relativo all'utilizzo di un metodo o di un altro membro della libreria.  Questo presuppone generalmente l'utilizzo del tag [\<code\>](../../../visual-basic/language-reference/xmldoc/code.md).  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 Nell'esempio riportato di seguito il tag `<example>` viene utilizzato per includere un esempio relativo all'utilizzo del campo `ID`.  
  
 [!code-vb[VbVbcnXmlDocComments#2](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/example_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)