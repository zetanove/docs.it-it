---
title: "Tag consigliati per i commenti relativi alla documentazione (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "XML [C#], tag"
  - "documentazione XML [C#], tag"
ms.assetid: 6e98f7a9-38f4-4d74-b644-1ff1b23320fd
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Tag consigliati per i commenti relativi alla documentazione (Guida per programmatori C#)
Il compilatore C\# elabora i commenti relativi alla documentazione nel codice e li formatta come XML in un file cui il nome viene specificato nell'opzione della riga di comando **\/doc**.  Per creare la documentazione finale basata sul file generato dal compilatore, è possibile creare uno strumento personalizzato, o utilizzare uno strumento come [Sandcastle](http://shfb.codeplex.com/).  
  
 I tag vengono elaborati su determinati costrutti del codice, ad esempio i tipi e i membri dei tipi.  
  
> [!NOTE]
>  Non è possibile applicare a uno spazio dei nomi i commenti relativi alla documentazione.  
  
 Il compilatore elabora tutti i tag validi per XML.  I tag riportati di seguito forniscono le funzionalità più comunemente utilizzate nella documentazione per l'utente.  
  
## Tag  
  
||||  
|-|-|-|  
|[\<c\>](../../../csharp/programming-guide/xmldoc/code-inline.md)|[\<para\>](../../../csharp/programming-guide/xmldoc/para.md)|[\<see\>](../../../csharp/programming-guide/xmldoc/see.md)\*|  
|[\<code\>](../../../csharp/programming-guide/xmldoc/code.md)|[\<param\>](../../../csharp/programming-guide/xmldoc/param.md)\*|[\<seealso\>](../../../csharp/programming-guide/xmldoc/seealso.md)\*|  
|[\<example\>](../../../csharp/programming-guide/xmldoc/example.md)|[\<paramref\>](../../../csharp/programming-guide/xmldoc/paramref.md)|[\<summary\>](../../../csharp/programming-guide/xmldoc/summary.md)|  
|[\<exception\>](../../../csharp/programming-guide/xmldoc/exception.md)\*|[\<permission\>](../../../csharp/programming-guide/xmldoc/permission.md)\*|[\<typeparam\>](../../../csharp/programming-guide/xmldoc/typeparam.md)\*|  
|[\<include\>](../../../csharp/programming-guide/xmldoc/include.md)\*|[\<remarks\>](../../../csharp/programming-guide/xmldoc/remarks.md)|[\<typeparamref\>](../../../csharp/programming-guide/xmldoc/typeparamref.md)|  
|[\<list\>](../../../csharp/programming-guide/xmldoc/list.md)|[\<returns\>](../../../csharp/programming-guide/xmldoc/returns.md)|[\<value\>](../../../csharp/programming-guide/xmldoc/value.md)|  
  
 \* indica che il compilatore esegue la verifica della sintassi.  
  
 Se si desidera che nel testo di un commento relativo alla documentazione vengano visualizzate parentesi angolari, utilizzare `<` e `>`, come illustrato nell'esempio che segue.  
  
```xml  
/// <summary cref="C < T >">  
/// </summary>  
```  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [\/doc \(Process Documentation Comments\)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [Commenti relativi alla documentazione XML](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)