---
title: "Spazi dei nomi (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, spazi dei nomi"
  - "spazi dei nomi [C#]"
ms.assetid: b1c4ab46-3fad-4ffa-9deb-dd50a2d8c65a
caps.latest.revision: 27
caps.handback.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Spazi dei nomi (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Gli spazi dei nomi vengono ampiamente utilizzati all'interno dei programmi C\# in due modi.  In primo luogo, vengono utilizzati in .NET Framework per organizzare le numerose classi disponibili come descritto di seguito:  
  
 [!code-cs[csProgGuide#22](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/index_1.cs)]  
  
 `System` è uno spazio dei nomi e `Console` è una classe in tale spazio dei nomi.  La parola chiave `using` può essere utilizzata in modo che il nome completo non sia necessario, come nell'esempio seguente:  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/index_2.cs)]  
  
 [!code-cs[csProgGuide#25](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/index_3.cs)]  
  
 Per ulteriori informazioni, vedere [Direttiva using](../../../csharp/language-reference/keywords/using-directive.md).  
  
 In secondo luogo, nei progetti di programmazione di grandi dimensioni la dichiarazione di spazi dei nomi consente di controllare l'ambito dei nomi di classi e metodi.  Utilizzare la parola chiave [namespace](../../../csharp/language-reference/keywords/namespace.md) per dichiarare uno spazio dei nomi, come illustrato nel seguente esempio:  
  
 [!code-cs[csProgGuideNamespaces#6](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/index_4.cs)]  
  
## Cenni preliminari sugli spazi dei nomi  
 Di seguito sono riportate le caratteristiche principali degli spazi dei nomi:  
  
-   Consentono di organizzare progetti di codice di grandi dimensioni.  
  
-   Sono delimitati dall'operatore `.`.  
  
-   La parola chiave `using directive` elimina la necessità di specificare il nome dello spazio dei nomi per ciascuna classe.  
  
-   Lo spazio dei nomi `global` rappresenta lo spazio dei nomi "radice": `global::System` farà sempre riferimento allo spazio dei nomi `System` di .NET Framework.  
  
## Sezioni correlate  
 Per ulteriori informazioni sugli spazi dei nomi, vedere gli argomenti elencati di seguito:  
  
-   [Utilizzo degli spazi dei nomi](../../../csharp/programming-guide/namespaces/using-namespaces.md)  
  
-   [Procedura: utilizzare l'alias dello spazio dei nomi globale](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md)  
  
-   [Procedura: utilizzare lo spazio dei nomi My](../../../csharp/programming-guide/namespaces/how-to-use-the-my-namespace.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave per spazi dei nomi](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [Direttiva using](../../../csharp/language-reference/keywords/using-directive.md)   
 [Operatore ::](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)   
 [. Operatore](../../../csharp/language-reference/operators/member-access-operator.md)