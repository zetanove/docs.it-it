---
title: "&lt;remarks&gt; (Visual Basic) | Microsoft Docs"
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
  - "<remarks> XML tag"
  - "remarks XML tag"
ms.assetid: c6241773-a7ed-41c9-9a8b-9722a0c606a9
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;remarks&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica una sezione relativa alle osservazioni per il membro.  
  
## Sintassi  
  
```  
<remarks>description</remarks>  
```  
  
#### Parametri  
 `description`  
 Descrizione del membro.  
  
## Note  
 Il tag `<remarks>` viene utilizzato per aggiungere informazioni su un tipo, che integrano quelle specificate con [\<summary\>](../../../visual-basic/language-reference/xmldoc/summary.md).  
  
 Queste informazioni vengono visualizzati nel Visualizzatore oggetti.  Per informazioni sul Visualizzatore oggetti, vedere [Visualizzazione della struttura del codice](/visual-studio/ide/viewing-the-structure-of-code).  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 Nell'esempio riportato di seguito il tag `<remarks>` viene utilizzato per illustrare le operazioni che vengono eseguite dal metodo `UpdateRecord`.  
  
 [!code-vb[VbVbcnXmlDocComments#6](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/remarks_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)