---
title: "Procedura: accedere a una classe di raccolte con foreach (Guida per programmatori C#) | Microsoft Docs"
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
  - "classi di raccolte [C#], foreach (istruzione)"
ms.assetid: a6b9cf5c-6c8d-4223-b12c-288949434493
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: accedere a una classe di raccolte con foreach (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nell'esempio di codice seguente viene illustrato come scrivere una classe Collection non generica utilizzabile con [foreach](../../../csharp/language-reference/keywords/foreach-in.md).  Nell'esempio viene definita una classe tokenizer di stringa.  
  
> [!NOTE]
>  La procedura riportata in questo esempio è consigliata solo quando non è possibile utilizzare una classe Collection generica.  Per un esempio di come implementare una classe Collection generica indipendente dai tipi che supporta <xref:System.Collections.Generic.IEnumerable%601>, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Nell'esempio il segmento di codice seguente utilizza la classe `Tokens` per suddividere la frase "This is a sample sentence." in token utilizzando ' ' e '\-' come separatori.  Il codice consente quindi di visualizzare tali token utilizzando un'istruzione `foreach`.  
  
 [!code-cs[csProgGuideCollections#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-access-a-collection-class-with-foreach_1.cs)]  
  
## Esempio  
 Internamente, la classe `Tokens` utilizza una matrice per archiviare i token.  Poiché le matrici implementano <xref:System.Collections.IEnumerator> e <xref:System.Collections.IEnumerable>, l'esempio di codice avrebbe potuto utilizzare i metodi di enumerazione della matrice \(<xref:System.Collections.IEnumerable.GetEnumerator%2A>, <xref:System.Collections.IEnumerator.MoveNext%2A>, <xref:System.Collections.IEnumerator.Reset%2A> e <xref:System.Collections.IEnumerator.Current%2A>\) anziché definirli nella classe `Tokens`.  Le definizioni dei metodi sono incluse nell'esempio per chiarire come vengono definiti i metodi e lo scopo di ognuno di essi.  
  
 [!code-cs[csProgGuideCollections#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-access-a-collection-class-with-foreach_2.cs)]  
  
 In C\# non è necessario che una classe Collection implementi <xref:System.Collections.IEnumerable> e <xref:System.Collections.IEnumerator> per essere compatibile con `foreach`.  Se la classe dispone dei membri <xref:System.Collections.IEnumerable.GetEnumerator%2A>, <xref:System.Collections.IEnumerator.MoveNext%2A>, <xref:System.Collections.IEnumerator.Reset%2A> e <xref:System.Collections.IEnumerator.Current%2A> necessari, funzionerà con `foreach`.  L'omissione delle interfacce consente di definire come tipo restituito da `Current` un tipo più specifico di <xref:System.Object>.  In questo modo viene garantita l'indipendenza dai tipi.  
  
 Modificare ad esempio le righe seguenti dell'esempio precedente.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Poiché `Current` restituisce una stringa, il compilatore è in grado di rilevare l'eventuale utilizzo di un tipo non compatibile in un'istruzione `foreach`, come illustrato nel codice seguente.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 L'omissione di <xref:System.Collections.IEnumerable> e <xref:System.Collections.IEnumerator> impedisce tuttavia l'interoperabilità della classe Collection con le istruzioni `foreach` o con istruzioni equivalenti di altri linguaggi compatibili con Common Language Runtime.  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)