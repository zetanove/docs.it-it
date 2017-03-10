---
title: "Propriet&#224; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cs.properties"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, proprietà"
  - "proprietà [C#]"
ms.assetid: e295a8a2-b357-4ee7-a12e-385a44146fa8
caps.latest.revision: 38
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 38
---
# Propriet&#224; (Guida per programmatori C#)
Una proprietà è un membro che fornisce un meccanismo flessibile per leggere, scrivere o calcolare il valore di un campo privato.  Le proprietà possono essere usate come se fossero membri dati pubblici, ma sono in realtà metodi speciali denominati *funzioni di accesso*.  Questo consente di accedere facilmente ai dati e di alzare di livello la sicurezza e la flessibilità dei metodi.  
  
 In questo esempio, la classe `TimePeriod` archivia un periodo di tempo.  Internamente la classe archivia il periodo in secondi, ma una proprietà denominata `Hours` consente a un client di specificare un periodo in ore.  Le funzioni di accesso per la proprietà `Hours` eseguono la conversione tra ore e secondi.  
  
## Esempio  
 [!code-cs[csProgGuideProperties#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/properties_1.cs)]  
  
## Definizioni di espressioni corpo  
 È normale che alcune proprietà si limitino a restituire immediatamente il risultato di un'espressione.  Esiste una sintassi breve per definire queste proprietà usando `=>`:  
  
```c#  
public string Name => First + " " + Last;   
```  
  
 La proprietà deve essere di sola lettura e non è necessario usare la parola chiave della funzione di accesso `get`.  
  
## Cenni preliminari sulle proprietà  
  
-   Le proprietà consentono a una classe di esporre un modo pubblico per ottenere e impostare i valori, nascondendo però il codice di implementazione o di verifica.  
  
-   Una funzione di accesso della proprietà [get](../../../csharp/language-reference/keywords/get.md) viene usata per restituire il valore della proprietà e una funzione di accesso [set](../../../csharp/language-reference/keywords/set.md) viene usata per assegnare un nuovo valore.  Queste funzioni di accesso possono avere diversi livelli di accesso.  Per altre informazioni, vedere [Limitazione dell'accessibilità delle funzioni di accesso](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md).  
  
-   La parola chiave [value](../../../csharp/language-reference/keywords/value.md) viene usata per definire il valore che deve essere assegnato dalla funzione di accesso `set`.  
  
-   Le proprietà che non implementano una funzione di accesso `set` sono di sola lettura.  
  
-   Per le proprietà semplici che non richiedono alcun codice di accesso personalizzato, prendere in considerazione la possibilità di usare le proprietà implementate automaticamente.  Per altre informazioni, vedere [Proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md).  
  
## Sezioni correlate  
  
-   [Utilizzo delle proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)  
  
-   [Proprietà dell'interfaccia](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)  
  
-   [Confronto tra proprietà e indicizzatori](../../../csharp/programming-guide/indexers/comparison-between-properties-and-indexers.md)  
  
-   [Limitazione dell'accessibilità delle funzioni di accesso](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)  
  
-   [Proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Utilizzo delle proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)