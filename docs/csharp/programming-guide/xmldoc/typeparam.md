---
title: "&lt;typeparam&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "typeparam"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<typeparam> (tag XML C#)"
  - "typeparam (tag XML C#)"
ms.assetid: 9b99d400-e911-4e55-99c6-64367c96aa4f
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# &lt;typeparam&gt; (Guida per programmatori C#)
## Sintassi  
  
```  
<typeparam name="name">description</typeparam>  
```  
  
#### Parametri  
 `name`  
 Nome del parametro del tipo.  Racchiudere il nome tra virgolette doppie \(" "\).  
  
 `description`  
 Descrizione del parametro di tipo.  
  
## Note  
 Il tag `<typeparam>` deve essere utilizzato nel commento relativo alla dichiarazione di un metodo o di un tipo generico per descrivere un parametro di tipo.  Aggiungere un tag per ogni parametro di tipo del metodo o del tipo generico.  
  
 Per ulteriori informazioni, vedere [Generics](../../../csharp/programming-guide/generics/index.md).  
  
 Il testo relativo al tag `<typeparam>` verrà visualizzato in IntelliSense, in [Object Browser Window](http://msdn.microsoft.com/it-it/3c7f1673-1f0d-41b1-94ca-a3dcfcb82cda) e nel report Web sui commenti del codice.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#13](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/typeparam_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)