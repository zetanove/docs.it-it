---
title: "Costruttori statici (Guida per programmatori C#) | Microsoft Docs"
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
  - "costruttori [C#], statiche"
  - "costruttori statici [C#]"
ms.assetid: 151ec95e-3c4d-4ed7-885d-95b7a3be2e7d
caps.latest.revision: 23
caps.handback.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Costruttori statici (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un costruttore statico consente di inizializzare gli eventuali dati [statici](../../../csharp/language-reference/keywords/static.md) oppure di eseguire un'operazione specifica che deve essere effettuata una sola volta.  Viene chiamato automaticamente prima che ne venga creata la prima istanza o venga fatto riferimento a qualsiasi membro statico.  
  
 [!code-cs[csProgGuideObjects#14](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-constructors_1.cs)]  
  
 Di seguito sono riportate le proprietà dei costruttori statici:  
  
-   Un costruttore statico non accetta modificatori di accesso né parametri.  
  
-   Un costruttore statico viene chiamato automaticamente per inizializzare la [classe](../../../csharp/language-reference/keywords/class.md) prima che ne venga creata la prima istanza o venga fatto riferimento a qualsiasi membro statico.  
  
-   Un costruttore statico non può essere chiamato direttamente.  
  
-   L'utente non può controllare in alcun modo il momento in cui il costruttore statico viene eseguito nel programma.  
  
-   In genere, i costruttori statici sono utilizzati per scrivere voci nel file di log, quando alla classe è associato un file di log.  
  
-   I costruttori statici risultano utili anche durante la creazione di classi wrapper per il codice non gestito, quando il costruttore può chiamare il metodo `LoadLibrary`.  
  
-   Se un costruttore statico genera un'eccezione, il runtime non lo richiamerà una seconda volta e il tipo rimarrà non inizializzato per la durata del dominio dell'applicazione in cui il programma è in esecuzione.  
  
## Esempio  
 In questo esempio la classe `Bus` dispone di un costruttore statico.  Quando viene creata la prima istanza di `Bus` \(`bus1`\), il costruttore statico viene richiamato per inizializzare la classe.  L'output dell'esempio verifica che il costruttore statico venga eseguito una sola volta, anche se vengono create due istanze di `Bus`, e che venga eseguito prima del costruttore di istanza.  
  
 [!code-cs[csProgGuideObjects#15](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-constructors_2.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)