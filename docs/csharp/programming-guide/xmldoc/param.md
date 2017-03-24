---
title: "&lt;param&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "param"
  - "<param>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<param> (tag XML C#)"
  - "param (tag XML C#)"
ms.assetid: 46d329b1-5b84-4537-9e17-73ca97313e4e
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# &lt;param&gt; (Guida per programmatori C#)
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
 Il tag \<param\> viene utilizzato nel commento per una dichiarazione di metodo per descrivere uno dei parametri del metodo.  Per documentare più parametri, utilizzare più tag \<param\>.  
  
 Il testo del tag \<param\> verrà visualizzato in IntelliSense, nel Visualizzatore oggetti e nel report Web sui commenti del codice.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#1](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/param_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)