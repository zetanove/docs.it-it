---
title: "&lt;typeparamref&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "typeparamref"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<typeparamref> (tag XML C#)"
  - "typeparamref (tag XML C#)"
ms.assetid: 6d8ffc58-12c5-4688-8db6-833a7ded5886
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# &lt;typeparamref&gt; (Guida per programmatori C#)
## Sintassi  
  
```  
<typeparamref name="name"/>  
```  
  
#### Parametri  
 `name`  
 Nome del parametro del tipo.  Racchiudere il nome tra virgolette doppie \(" "\).  
  
## Note  
 Per ulteriori informazioni sui parametri di tipo in metodi e tipi generici, vedere [Generics](../../../csharp/programming-guide/generics/index.md).  
  
 Utilizzare questo tag per consentire agli utenti del file di documentazione di formattare la parola in modo da distinguerla, ad esempio in corsivo.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#13](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/typeparamref_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)