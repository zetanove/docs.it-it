---
title: "&lt;remarks&gt; (Guida per programmatori C#) | Microsoft Docs"
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
  - "remarks"
  - "<remarks>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<remarks> (tag XML C#)"
  - "remarks (tag XML C#)"
ms.assetid: f8641391-31f3-4735-af7a-c502a5b6a251
caps.latest.revision: 15
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;remarks&gt; (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## Sintassi  
  
```  
<remarks>description</remarks>  
```  
  
#### Parametri  
 `Description`  
 Descrizione del membro.  
  
## Note  
 Il tag \<remarks\> viene utilizzato per aggiungere informazioni sul tipo che integrano quelle specificate con [\<summary\>](../../../csharp/programming-guide/xmldoc/summary.md).  Tali informazioni vengono visualizzate in [Object Browser Window](http://msdn.microsoft.com/it-it/3c7f1673-1f0d-41b1-94ca-a3dcfcb82cda).  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#9](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/remarks_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)