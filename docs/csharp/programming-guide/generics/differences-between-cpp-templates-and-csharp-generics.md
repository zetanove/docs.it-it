---
title: "Differenze tra modelli C++ e generics C# (Guida per programmatori C#) | Microsoft Docs"
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
  - "generics [C#], e modelli C++"
ms.assetid: 1da6beeb-d4a4-4da0-87b7-0cfbe04920b7
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Differenze tra modelli C++ e generics C# (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

I generics C\# e i modelli C\+\+ sono entrambi funzionalità del linguaggio che forniscono il supporto per i tipi con parametri.  Esistono tuttavia numerose differenze tra queste due funzionalità.  A livello di sintassi, i generics C\# rappresentano un approccio più semplice ai tipi con parametri, senza la complessità dei modelli C\+\+.  Inoltre, il linguaggio C\# non è stato concepito per fornire tutte le funzionalità dei modelli C\+\+.  A livello di implementazione, la differenza principale consiste nel fatto che le sostituzioni di tipi generici C\# vengono eseguite in fase di esecuzione e, di conseguenza, le informazioni sui tipi generici vengono mantenute per gli oggetti di cui viene creata un'istanza.  Per ulteriori informazioni, vedere [Generics nel runtime](../../../csharp/programming-guide/generics/generics-in-the-run-time.md).  
  
 Di seguito sono riportate le principali differenze tra generics C\# e modelli C\+\+:  
  
-   I generics C\# non forniscono lo stesso livello di flessibilità dei modelli C\+\+.  Non è ad esempio possibile chiamare operatori aritmetici in una classe generica C\#, anche se è possibile chiamare operatori definiti dall'utente.  
  
-   C\# non consente di utilizzare parametri di modello non di tipo, ad esempio `template C<int i> {}`.  
  
-   C\# non supporta la specializzazione esplicita, ossia un'implementazione personalizzata di un modello per un tipo specifico.  
  
-   C\# non supporta la specializzazione parziale, ossia un'implementazione personalizzata per un sottoinsieme degli argomenti del tipo.  
  
-   C\# non consente l'utilizzo del parametro di tipo come classe base per il tipo generico.  
  
-   C\# non consente l'utilizzo di tipi predefiniti per i parametri di tipo.  
  
-   In C\# un parametro di tipo generico non può essere di per sé un elemento generico, anche se i tipi costruiti possono essere utilizzati come generics.  C\+\+ non consente l'utilizzo di parametri di modello.  
  
-   C\+\+ consente di utilizzare codice che potrebbe non essere valido per tutti i parametri di tipo nel modello, che viene quindi controllato per verificare la disponibilità del tipo specifico utilizzato come parametro di tipo.  In C\# il codice di una classe deve essere scritto in modo da funzionare con qualsiasi tipo in grado di soddisfare i vincoli.  Ad esempio, in C\+\+ è possibile scrivere una funzione in cui sono utilizzati gli operatori aritmetici `+` e `-` sugli oggetti del parametro di tipo, generando un errore al momento della creazione di un'istanza del modello con un tipo che non supporta tali operatori.  In C\# questo non è possibile. Gli unici costrutti di linguaggio ammessi sono quelli deducibili dai vincoli.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [Modelli](/visual-cpp/cpp/templates-cpp)