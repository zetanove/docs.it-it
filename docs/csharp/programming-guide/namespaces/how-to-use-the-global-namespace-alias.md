---
title: "Procedura: utilizzare l&#39;alias dello spazio dei nomi globale (Guida per programmatori C#) | Microsoft Docs"
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
  - "alias [C#]"
  - "spazio dei nomi globale [C#]"
  - "spazi dei nomi [C#], qualificatore di spazio dei nomi globale [C#]"
ms.assetid: 98a1d89b-3c5a-44f7-8400-c4a3c0ec22a9
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: utilizzare l&#39;alias dello spazio dei nomi globale (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La possibilità di accedere a un membro dello [spazio dei nomi](../../../csharp/language-reference/keywords/namespace.md) globale risulta utile quando il membro può essere nascosto da un'altra entità con lo stesso nome.  
  
 Nell'esempio di codice riportato di seguito `Console` viene risolto in `TestApp.Console` anziché nel tipo `Console` dello spazio dei nomi <xref:System>.  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/how-to-use-the-global-namespace-alias_1.cs)]  
  
 [!code-cs[csProgGuideNamespaces#1](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-global-namespace-alias_2.cs)]  
  
 L'utilizzo di `System.Console` determina un errore in quanto lo spazio dei nomi `System` è nascosto dalla classe `TestApp.System`:  
  
 [!code-cs[csProgGuideNamespaces#2](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-global-namespace-alias_3.cs)]  
  
 È tuttavia possibile evitare questo errore utilizzando `global::System.Console` nel modo seguente:  
  
 [!code-cs[csProgGuideNamespaces#3](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-global-namespace-alias_4.cs)]  
  
 Se l'identificatore di sinistra è `global`, la ricerca dell'identificatore di destra ha inizio dallo spazio dei nomi globale.  La seguente dichiarazione fa ad esempio riferimento a `TestApp` come membro dello spazio globale.  
  
 [!code-cs[csProgGuideNamespaces#4](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-global-namespace-alias_5.cs)]  
  
 Non è ovviamente consigliabile creare spazi dei nomi personali denominati `System` ed è improbabile che trovare codice che include uno spazio dei nomi con tale nome.  Nei progetti di grandi dimensioni è tuttavia molto probabile che si verifichi la duplicazione degli spazi dei nomi in un form o in un altro.  In queste situazioni è possibile utilizzare il qualificatore dello spazio dei nomi globale per specificare lo spazio dei nomi di primo livello.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato lo spazio dei nomi `System` per includere la classe `TestClass`. Di conseguenza, è necessario utilizzare `global::System.Console` per fare riferimento alla classe `System.Console`, nascosta dallo spazio dei nomi `System`.  Viene inoltre utilizzato l'alias `colAlias` per fare riferimento allo spazio dei nomi `System.Collections`. Di conseguenza, l'istanza di una <xref:System.Collections.Hashtable?displayProperty=fullName> è stata creata utilizzando questo alias anziché lo spazio dei nomi.  
  
 [!code-cs[csProgGuideNamespaces#5](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/how-to-use-the-global-namespace-alias_6.cs)]  
  
  **A 1**  
**B 2**  
**C 3**   
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Spazi dei nomi](../../../csharp/programming-guide/namespaces/index.md)   
 [. Operatore](../../../csharp/language-reference/operators/member-access-operator.md)   
 [Operatore ::](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)   
 [extern](../../../csharp/language-reference/keywords/extern.md)