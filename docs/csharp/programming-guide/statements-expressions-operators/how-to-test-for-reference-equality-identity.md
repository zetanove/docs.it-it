---
title: "Procedura: testare l&#39;uguaglianza di riferimenti (identit&#224;) (Guida per programmatori C#) | Microsoft Docs"
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
  - "identità di oggetto [C#]"
  - "uguaglianza di riferimenti [C#]"
ms.assetid: 91307fda-267b-4fd2-a338-2aada39ee791
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: testare l&#39;uguaglianza di riferimenti (identit&#224;) (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Non è necessario implementare alcuna logica personalizzata per supportare i confronti di uguaglianza dei riferimenti nei tipi.  Questa funzionalità viene fornita per tutti i tipi dal metodo <xref:System.Object.ReferenceEquals%2A?displayProperty=fullName> statico.  
  
 Nell'esempio seguente viene illustrato come determinare se due variabili presentano *uguaglianza di riferimenti*, ovvero se fanno riferimento allo stesso oggetto in memoria.  
  
 Nell'esempio viene inoltre illustrato perché <xref:System.Object.ReferenceEquals%2A?displayProperty=fullName> restituisca sempre `false` per i tipi di valore e perché non sia consigliabile utilizzare  <xref:System.Object.ReferenceEquals%2A> per determinare l'uguaglianza tra stringhe.  
  
## Esempio  
 [!code-cs[csProgGuideObjects#90](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-test-for-reference-equality-identity_1.cs)]  
  
 L'implementazione di `Equals` nella classe di base universale <xref:System.Object?displayProperty=fullName> esegue anche un controllo dell'uguaglianza dei riferimenti, ma è meglio non servirsene perché, se una classe esegue l'override del metodo, i risultati potrebbero non essere quelli previsti.  La stessa considerazione vale anche per gli operatori `==` e `!=`.  Quando agiscono sui tipi di riferimento, il comportamento predefinito di \=\= e `!=` prevede l'esecuzione di un controllo dell'uguaglianza dei riferimenti.  Le classi derivate possono tuttavia eseguire l'overload dell'operatore per eseguire un controllo dell'uguaglianza dei valori.  Per ridurre al minimo la possibilità di errori, è meglio utilizzare sempre <xref:System.Object.ReferenceEquals%2A> quando è necessario determinare se due oggetti presentano uguaglianza di riferimenti.  
  
 Stringhe costanti all'interno dello stesso assembly vengono sempre archiviate dal runtime.  In altre parole, viene mantenuta una sola istanza di ogni stringa letterale univoca.  Il runtime tuttavia non garantisce che le stringhe create in fase di esecuzione vengano inserite né garantisce che vengano inserite due stringhe costanti uguali in assembly diversi.  
  
## Vedere anche  
 [Confronti di uguaglianza](../../../csharp/programming-guide/statements-expressions-operators/equality-comparisons.md)