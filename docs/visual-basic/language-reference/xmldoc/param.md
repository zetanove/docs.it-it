---
title: "&lt;param&gt; (Visual Basic) | Microsoft Docs"
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
  - "param XML tag"
  - "<param> XML tag"
ms.assetid: 4e32e86f-f6f3-4301-b7fc-2f321fb54368
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# &lt;param&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Definisce un nome e una descrizione di parametro.  
  
## Sintassi  
  
```  
<param name="name">description</param>  
```  
  
#### Parametri  
 `name`  
 Nome di un parametro di metodo.  Racchiudere il nome tra virgolette doppie \(" "\).  
  
 `description`  
 Descrizione del parametro.  
  
## Note  
 Il tag `<param>` viene utilizzato nel commento per una dichiarazione del metodo al fine di descrivere uno dei parametri del metodo.  
  
 Il testo per il tag `<param>` verrà visualizzato nelle seguenti posizioni:  
  
-   Informazioni sul parametro IntelliSense.  Per ulteriori informazioni, vedere [Utilizzo di IntelliSense](/visual-studio/ide/using-intellisense).  
  
-   Visualizzatore oggetti.  Per ulteriori informazioni, vedere [Visualizzazione della struttura del codice](/visual-studio/ide/viewing-the-structure-of-code).  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 In questo esempio il tag `<param>` viene utilizzato per descrivere il parametro `id`.  
  
 [!code-vb[VbVbcnXmlDocComments#6](../../../visual-basic/language-reference/xmldoc/codesnippet/visualbasic/param_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)