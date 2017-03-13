---
title: "namespace (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "namespace_CSharpKeyword"
  - "namespace"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "namespace (parola chiave) [C#]"
  - "scope [C#]"
ms.assetid: 0a788423-9110-42e0-97d9-bda41ca4870f
caps.latest.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 28
---
# namespace (Riferimenti per C#)
La parola chiave `namespace` utilizzata per dichiarare un ambito che contiene un set di oggetti correlati.  È possibile utilizzare uno spazio dei nomi per organizzare gli elementi di codice e creare globale tipi univoci.  
  
 [!code-cs[csrefKeywordsNamespace#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/namespace_1.cs)]  
  
## Note  
 Dichiarazione di uno o più tipi tra quelli riportati di seguito, all'interno di uno spazio dei nomi:  
  
-   Un altro spazio dei nomi  
  
-   [class](../../../csharp/language-reference/keywords/class.md)  
  
-   [interface](../../../csharp/language-reference/keywords/interface.md)  
  
-   [struct](../../../csharp/language-reference/keywords/struct.md)  
  
-   [enum](../../../csharp/language-reference/keywords/enum.md)  
  
-   [delegato](../../../csharp/language-reference/keywords/delegate.md)  
  
 Che si dichiari o meno in modo esplicito uno spazio dei nomi in un file di origine C\#, il compilatore aggiungerà uno spazio dei nomi predefinito.  Tale spazio dei nomi, talvolta indicato come spazio dei nomi globale, è senza nome ed è presente in ogni file.  Qualsiasi identificatore nello spazio dei nomi globale può essere utilizzato all'interno di uno spazio dei nomi denominato.  
  
 Gli spazi dei nomi dispongono in modo implicito dell'accesso pubblico; tale tipo di accesso non è modificabile.  Per informazioni sui modificatori di accesso che è possibile assegnare agli elementi all'interno di uno spazio dei nomi, vedere [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md).  
  
 È possibile definire uno spazio dei nomi in una o più dichiarazioni.  Nell'esempio riportato di seguito vengono definite due classi come parte dello spazio dei nomi `MyCompany`:  
  
 [!code-cs[csrefKeywordsNamespace#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/namespace_2.cs)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come chiamare un metodo statico in uno spazio dei nomi annidato.  
  
 [!code-cs[csrefKeywordsNamespace#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/namespace_3.cs)]  
  
## Ulteriori informazioni  
 Per ulteriori informazioni sull'utilizzo degli spazi dei nomi, vedere gli argomenti riportati di seguito:  
  
-   [Spazi dei nomi](../../../csharp/programming-guide/namespaces/index.md)  
  
-   [Utilizzo degli spazi dei nomi](../../../csharp/programming-guide/namespaces/using-namespaces.md)  
  
-   [Procedura: utilizzare l'alias dello spazio dei nomi globale](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per spazi dei nomi](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [utilizzo](../../../csharp/language-reference/keywords/using.md)