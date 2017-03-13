---
title: "&lt;paramref&gt; (Visual Basic) | Microsoft Docs"
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
  - "paramref XML tag"
  - "<paramref> XML tag"
ms.assetid: 8979d53b-beb1-41b7-b41e-6bbea1c17a03
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &lt;paramref&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Formatta una parola come parametro.  
  
## Sintassi  
  
```  
<paramref name="name"/>  
```  
  
#### Parametri  
 `name`  
 Nome del parametro a cui fare riferimento.  Racchiudere il nome tra virgolette doppie \(" "\).  
  
## Note  
 Il tag `<paramref>` consente di indicare che una parola è un parametro.  Il file XML può essere elaborato in modo da formattare il parametro in maniera specifica.  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 In questo esempio il tag `<paramref>` viene utilizzato per fare riferimento al parametro `id`.  
  
 [!code-vb[VbVbcnXmlDocComments#6](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/paramref_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)