---
title: "typeof (Riferimenti per C#) | Microsoft Docs"
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
  - "typeof"
  - "typeof_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "typeof (parola chiave) [C#]"
ms.assetid: 0c08d880-515e-46bb-8cd2-48b8dd62c08d
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# typeof (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Utilizzato per ottenere l'oggetto `System.Type` per un tipo.  Un'espressione `typeof` ha il formato riportato di seguito:  
  
```  
System.Type type = typeof(int);  
```  
  
## Note  
 Per ottenere il tipo in fase di esecuzione di un'espressione, è possibile utilizzare il metodo <xref:System.Object.GetType%2A> di .NET Framework, come nell'esempio riportato di seguito.  
  
```  
int i = 0;  
System.Type type = i.GetType();  
```  
  
 Non è possibile sottoporre l'operatore `typeof` a overload.  
  
 L'operatore `typeof` può essere utilizzato anche su tipi generici aperti.  I tipi con più di un parametro di tipo devono disporre del numero appropriato di virgole nella specifica.  Nell'esempio riportato di seguito viene illustrato come determinare se il tipo restituito di un metodo è un oggetto <xref:System.Collections.Generic.IEnumerable%601> generico.  Si presupponga che il metodo è un'istanza del tipo MethodInfo:  
  
```  
string s = method.ReturnType.GetInterface  
    (typeof(System.Collections.Generic.IEnumerable<>).FullName);  
```  
  
## Esempio  
 [!code-cs[csrefKeywordsOperator#12](../../../csharp/language-reference/keywords/codesnippet/CSharp/typeof_1.cs)]  
  
## Esempio  
 In questo esempio viene utilizzato il metodo <xref:System.Object.GetType%2A> per determinare il tipo utilizzato per contenere il risultato di un calcolo numerico,  che dipende dai requisiti di spazio su disco del numero risultante.  
  
 [!code-cs[csrefKeywordsOperator#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/typeof_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 <xref:System.Type?displayProperty=fullName>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md)