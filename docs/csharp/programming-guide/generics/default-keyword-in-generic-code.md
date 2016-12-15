---
title: "Parola chiave default in codice generico (Guida per programmatori C#) | Microsoft Docs"
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
  - "default (parola chiave) [C#], programmazione generica"
  - "generics [C#], default (parola chiave)"
ms.assetid: b9daf449-4e64-496e-8592-6ed2c8875a98
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Parola chiave default in codice generico (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nelle classi e nei metodi generici, è determinante capire come assegnare un valore predefinito a un tipo T con parametri quando non si dispone in anticipo delle informazioni riportate di seguito:  
  
-   Non si sa se T sarà un tipo di riferimento o un tipo di valore.  
  
-   Nel caso in cui T sia un tipo di valore, non si sa se sarà una struttura o un valore numerico.  
  
 Data una variabile t di un tipo T con parametri, l'istruzione t \= null sarà valida solo se T è un tipo di riferimento e t \= 0 sarà valida solo per i tipi di valore numerico e non per le strutture.  La soluzione consiste nell'utilizzare la parola chiave `default` che restituirà null per i tipi di riferimento e zero per i tipi di valore numerico.  Per le strutture, restituirà ogni membro della struttura inizializzato su zero o null a seconda che si tratti di tipi di valore o di riferimento.  Per i tipi di valori nullable, default restituisce un oggetto <xref:System.Nullable%601?displayProperty=fullName>, che viene inizializzato come qualsiasi struct.  
  
 Nell'esempio riportato di seguito riferito alla classe `GenericList<T>` viene illustrato come utilizzare la parola chiave `default`.  Per ulteriori informazioni, vedere [Cenni preliminari sui generics](../../../csharp/programming-guide/generics/introduction-to-generics.md).  
  
 [!code-cs[csProgGuideGenerics#41](../../../csharp/programming-guide/generics/codesnippet/CSharp/default-keyword-in-generic-code_1.cs)]  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Generics](../../../csharp/programming-guide/generics/index.md)   
 [Metodi generici](../../../csharp/programming-guide/generics/generic-methods.md)   
 [Generics](../Topic/Generics%20in%20the%20.NET%20Framework.md)