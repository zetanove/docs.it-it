---
title: "Procedura: eseguire una query su una raccolta di oggetti (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "raccolta di oggetti (query) [C#]"
  - "query [LINQ in C#], raccolte di oggetti"
  - "query (espressioni) [LINQ in C#], raccolte di oggetti"
ms.assetid: 122d1e3b-1604-4add-b6b4-b84530a77b6b
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: eseguire una query su una raccolta di oggetti (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In questo esempio viene illustrato come eseguire una query semplice su un elenco di oggetti `Student`.  Ogni oggetto `Student` contiene alcune informazioni di base sullo studente e un elenco che rappresenta i voti dello studente in quattro esami.  
  
 Questa applicazione funge da framework per molti altri esempi di questa sezione che utilizzano la stessa origine dati `students` .  
  
## Esempio  
 La query seguente restituisce gli studenti che prendono un voto pari a 90 o superiore nel primo esame.  
  
 [!code-cs[csProgGuideLINQ#15](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-query-a-collection-of-objects_1.cs)]  
  
 Questa query è intenzionalmente semplice per consentire all'utente di fare pratica.  È possibile, ad esempio, provare più predicati nella clausola `where` o utilizzare la clausola `orderby` per ordinare i risultati.  
  
## Compilazione del codice  
  
-   Creare un progetto [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)] per .NET Framework versione 3.5.  Per impostazione predefinita, il progetto include un riferimento a System.Core.dll e una direttiva `using` per lo spazio dei nomi System.Linq.  
  
-   Copiare il codice nel progetto.  
  
-   Premere F5 per compilare ed eseguire il programma.  
  
-   Premere un tasto per chiudere la finestra della console.  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)