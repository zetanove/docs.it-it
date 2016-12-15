---
title: "&lt;exception&gt; (Guida per programmatori C#) | Microsoft Docs"
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
  - "exception"
  - "<exception>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<exception> (tag XML C#)"
  - "exception (tag XML C#)"
ms.assetid: dd73aac5-3c74-4fcf-9498-f11bff3a2f3c
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;exception&gt; (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## Sintassi  
  
```  
<exception cref="member">description</exception>  
```  
  
#### Parametri  
 cref \= "`member`"  
 Riferimento a un'eccezione disponibile dall'ambiente di compilazione corrente.  Il compilatore verifica che l'eccezione specificata esiste e converte `member` nel nome canonico dell'elemento nell'XML di output.  Il parametro `member` deve essere visualizzato tra virgolette doppie \(" "\).  
  
 Per ulteriori informazioni sulla creazione di un riferimento cref a un tipo generico, vedere [\<see\>](../../../csharp/programming-guide/xmldoc/see.md).  
  
 `description`  
 Descrizione dell'eccezione.  
  
## Note  
 Il tag \<exception\> consente di specificare le eccezioni che possono essere generate  Questo tag può essere applicato alle definizioni di metodi, proprietà, eventi e indicizzatori.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
 Per ulteriori informazioni sulla gestione delle eccezioni, vedere [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md).  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#4](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/exception_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)