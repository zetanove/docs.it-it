---
title: "into (Riferimenti per C#) | Microsoft Docs"
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
  - "into_CSharpKeyword"
  - "into"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "parola chiave into [C#]"
ms.assetid: 81ec62c1-f0b1-4755-8a31-959876e77f65
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# into (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave contestuale `into` può essere utilizzata per creare un identificatore temporaneo per l'archiviazione dei risultati di una clausola [group](../../../csharp/language-reference/keywords/group-clause.md), [join](../../../csharp/language-reference/keywords/join-clause.md) o [select](../../../csharp/language-reference/keywords/select-clause.md) in un nuovo identificatore.  Questo identificatore può essere un generatore per ulteriori comandi di query.  Se utilizzato in una clausola `group` o `select`, l'uso del nuovo identificatore viene talvolta definito *continuazione*.  
  
## Esempio  
 Nell'esempio seguente viene illustrato l'utilizzo della parola chiave `into` per attivare un identificatore temporaneo `fruitGroup` che contiene un tipo dedotto di `IGrouping`.  Utilizzando l'identificatore, è possibile richiamare il metodo <xref:System.Linq.Enumerable.Count%2A> su ogni gruppo e selezionare solo i gruppi che contengono due o più parole.  
  
 [!code-cs[cscsrefQueryKeywords#18](../../../csharp/language-reference/keywords/codesnippet/CSharp/into_1.cs)]  
  
 L'utilizzo di `into` in una clausola `group` è necessario solo quando si desidera eseguire operazioni di query aggiuntive in ogni gruppo.  Per ulteriori informazioni, vedere [Clausola group](../../../csharp/language-reference/keywords/group-clause.md).  
  
 Per un esempio dell'uso di `into` in una clausola `join`, vedere [Clausola join](../../../csharp/language-reference/keywords/join-clause.md).  
  
## Vedere anche  
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola group](../../../csharp/language-reference/keywords/group-clause.md)