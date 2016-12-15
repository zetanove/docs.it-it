---
title: "Generics nel runtime (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "generics [C#], in fase di esecuzione"
ms.assetid: 119df7e6-9ceb-49df-af36-24f8f8c0747f
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Generics nel runtime (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando un metodo o un tipo generico viene compilato in MSIL \(Microsoft intermediate language\), contiene metadati che lo identificano come dotato di parametri di tipo.  Le modalità di utilizzo di MSIL per un tipo generico variano a seconda che il parametro di tipo fornito sia un tipo valore o un tipo riferimento.  
  
 Quando un tipo generico viene costruito per la prima volta con un tipo valore come parametro, viene creato un tipo generico specializzato con il parametro o i parametri forniti sostituiti nelle posizioni appropriate in MSIL.  I tipi generici specializzati vengono creati una volta per ogni tipo valore univoco utilizzato come parametro.  
  
 Si supponga, ad esempio, che il codice del programma abbia dichiarato uno stack costituito da interi:  
  
 [!code-cs[csProgGuideGenerics#42](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_1.cs)]  
  
 A questo punto viene generata una versione specializzata della classe <xref:System.Collections.Generic.Stack%601> con l'intero sostituito in modo corretto con il parametro relativo.  In questo modo, ogni volta che il codice del programma utilizza uno stack di interi, viene riutilizzata la classe specializzata <xref:System.Collections.Generic.Stack%601> generata.  Nell'esempio riportato di seguito, vengono create due istanze di uno stack di interi che condividono una singola istanza del codice `Stack<int>`:  
  
 [!code-cs[csProgGuideGenerics#43](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_2.cs)]  
  
 Si supponga ora che un'altra classe <xref:System.Collections.Generic.Stack%601> con un tipo valore diverso, ad esempio `long`, o con una struttura definita dall'utente come relativo parametro venga creata in un altro punto nel codice.  Di conseguenza, viene generata un'altra versione del tipo generico e il valore `long` viene sostituito nelle posizioni appropriate in MSIL.  Le conversioni non sono più necessarie poiché ogni classe generica specializzata contiene a livello nativo il tipo di valore.  
  
 Il funzionamento dei generics presenta alcune lievi differenze rispetto a quello dei tipi riferimento.  Quando un tipo generico viene costruito per la prima volta con un tipo di riferimento qualsiasi, viene creato un tipo generico specializzato con riferimenti a oggetti sostituiti dai parametri in MSIL.  In seguito, ogni volta che viene creata un'istanza di un tipo costruito utilizzando come relativo parametro un tipo riferimento qualsiasi, verrà riutilizzata la versione specializzata del tipo generico creata in precedenza.  Questa situazione è possibile perché tutti i riferimenti presentano le stesse dimensioni.  
  
 Si supponga, ad esempio, di disporre di due tipi riferimento, una classe `Customer` e una classe `Order`, e di aver creato uno stack di tipi `Customer`:  
  
 [!code-cs[csProgGuideGenerics#47](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_3.cs)]  
  
 [!code-cs[csProgGuideGenerics#44](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_4.cs)]  
  
 A questo punto, viene generata una versione specializzata della classe <xref:System.Collections.Generic.Stack%601> che, anziché archiviare dati, archivia riferimenti a oggetti che verranno inseriti in seguito.  Si supponga inoltre che la riga di codice successiva crei uno stack di un altro tipo riferimento, denominato `Order`:  
  
 [!code-cs[csProgGuideGenerics#45](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_5.cs)]  
  
 Diversamente dai tipi di valore, non viene creata un'altra versione specializzata della classe <xref:System.Collections.Generic.Stack%601> per il tipo `Order`.  Viene invece creata un'istanza della versione specializzata della classe <xref:System.Collections.Generic.Stack%601> e viene impostata la variabile `orders` per farvi riferimento.  Si supponga di trovare successivamente una riga di codice per creare uno stack di un tipo `Customer`:  
  
 [!code-cs[csProgGuideGenerics#46](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_6.cs)]  
  
 Analogamente all'utilizzo precedente della classe <xref:System.Collections.Generic.Stack%601> creata con il tipo `Order`, viene creata un'altra istanza della classe <xref:System.Collections.Generic.Stack%601> specializzata.  I puntatori in essa contenuti vengono impostati per fare riferimento a un'area di memoria con le dimensioni di un tipo `Customer`.  Poiché il numero di tipi riferimento può variare notevolmente da un programma a un altro, l'implementazione di C\# dei generics riduce in modo significativo la quantità di codice riducendo a una le classi specializzate create dal compilatore per le classi generiche di tipi riferimento.  
  
 Inoltre, quando viene creata un'istanza di una classe C\# generica con un parametro di tipo valore o di tipo riferimento, è possibile sottoporla a query in fase di esecuzione utilizzando la reflection e determinare sia il tipo che il parametro di tipo relativi.  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [Generics](../Topic/Generics%20in%20the%20.NET%20Framework.md)