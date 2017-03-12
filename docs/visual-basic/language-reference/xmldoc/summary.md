---
title: "&lt;summary&gt; (Visual Basic) | Microsoft Docs"
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
  - "<summary> XML tag"
  - "summary XML tag"
ms.assetid: 861c847d-dd94-478a-aa23-bf4899cdc848
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# &lt;summary&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica il riepilogo del membro.  
  
## Sintassi  
  
```  
<summary>description</summary>  
```  
  
#### Parametri  
 `description`  
 Riepilogo relativo all'oggetto.  
  
## Note  
 Utilizzare il tag `<summary>` per descrivere un tipo o un membro di tipo.  Utilizzare [\<remarks\>](../../../visual-basic/language-reference/xmldoc/remarks.md) per aggiungere informazioni supplementari alla descrizione di un tipo.  
  
 Il testo per il tag `<summary>` è l'unica fonte di informazioni sul tipo in IntelliSense e visualizza nel Visualizzatore oggetti.  Per informazioni sul Visualizzatore oggetti, vedere [Visualizzazione della struttura del codice](/visual-studio/ide/viewing-the-structure-of-code).  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 In questo esempio il tag `<summary>` viene utilizzato per descrivere il metodo `ResetCounter` e la proprietà `Counter`.  
  
 [!code-vb[VbVbcnXmlDocComments#1](../../../visual-basic/language-reference/xmldoc/codesnippet/visualbasic/summary_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)