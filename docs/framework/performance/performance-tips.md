---
title: "Suggerimenti sulle prestazioni .NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "linguaggio C#, prestazioni"
  - "prestazioni [C#]"
  - "prestazioni [Visual Basic]"
  - "Visual Basic, prestazioni"
ms.assetid: ae275793-857d-4102-9095-b4c2a02d57f4
caps.latest.revision: 36
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
caps.handback.revision: 36
---
# Suggerimenti sulle prestazioni .NET
Il termine *prestazioni* fa in genere riferimento alla velocità di esecuzione di un programma.  È talvolta possibile aumentare la velocità di esecuzione attenendosi a determinate regole nel codice sorgente.  In alcuni programmi è importante esaminare attentamente il codice e utilizzare i code profiler per assicurarsi che venga eseguito alla massima velocità possibile.  In altri, non è possibile eseguire questa ottimizzazione perché il codice viene eseguito a una velocità accettabile man mano che viene scritto.  In questo articolo vengono elencate le aree comuni in cui le prestazioni possono risultare compromesse e suggerimenti per migliorarle, oltre a collegamenti ad altri argomenti relativi alle prestazioni.  Per ulteriori informazioni sulla pianificazione e misurazione delle prestazioni, vedere [Performance](../../../docs/framework/performance/index.md).  
  
## Boxing e unboxing  
 È meglio evitare di utilizzare tipi valore nelle situazioni in cui devono essere sottoposti a boxing un numero elevato di volte, ad esempio in classi di raccolte non generiche come <xref:System.Collections.ArrayList?displayProperty=fullName>.  È possibile evitare la conversione boxing di tipi valore tramite raccolte generiche come <xref:System.Collections.Generic.List%601?displayProperty=fullName>.  Le operazioni di boxing e unboxing sono processi onerosi dal punto di vista del calcolo.  Il boxing di un tipo di valore comporta infatti la creazione di un oggetto completamente nuovo.  operazione può essere fino a 20 volte più lunga rispetto a una semplice assegnazione di riferimento.  Durante l'unboxing il processo di cast può essere quattro volte più lungo di un'assegnazione.  Per ulteriori informazioni, vedere [Boxing e unboxing](../Topic/Boxing%20and%20Unboxing%20\(C%23%20Programming%20Guide\).md).  
  
## Stringhe  
 Quando si concatena un numero elevato di variabili stringa, ad esempio in un ciclo ridotto, utilizzare <xref:System.Text.StringBuilder?displayProperty=fullName> anziché l'[operatore \+](../Topic/+%20Operator%20\(C%23%20Reference\).md) C\# oppure gli [operatori di concatenazione](../Topic/Concatenation%20Operators%20\(Visual%20Basic\).md) di Visual Basic.  Per ulteriori informazioni, vedere [Procedura: concatenare più stringhe](../Topic/How%20to:%20Concatenate%20Multiple%20Strings%20\(C%23%20Programming%20Guide\).md) e [Concatenation Operators in Visual Basic](../Topic/Concatenation%20Operators%20in%20Visual%20Basic.md).  
  
## Distruttori  
 Non utilizzare distruttori vuoti.  Quando una classe contiene un distruttore, viene creata una voce nella coda di finalizzazione.  Quando si chiama il distruttore, viene richiamato Garbage Collector per elaborare la coda.  Se il distruttore è vuoto, si verifica semplicemente un calo di prestazioni.  Per ulteriori informazioni, vedere [Distruttori](../Topic/Destructors%20\(C%23%20Programming%20Guide\).md) e [Object Lifetime: How Objects Are Created and Destroyed](../Topic/Object%20Lifetime:%20How%20Objects%20Are%20Created%20and%20Destroyed%20\(Visual%20Basic\).md).  
  
## Altre risorse  
  
-   [Writing Faster Managed Code: Know What Things Cost](http://go.microsoft.com/fwlink/?LinkId=99294) \(informazioni in lingua inglese\)  
  
-   [Writing High\-Performance Managed Applications: A Primer](http://go.microsoft.com/fwlink/?LinkId=99295) \(informazioni in lingua inglese\)  
  
-   [Nozioni fondamentali su Garbage Collection e suggerimenti sulle prestazioni](http://go.microsoft.com/fwlink/?LinkId=99296)  
  
-   [Suggerimenti sulle prestazioni in applicazioni .NET](http://go.microsoft.com/fwlink/?LinkId=99297)  
  
-   [Strumenti diagnostici interni per.NET](http://go.microsoft.com/fwlink/?LinkId=112407)  
  
-   [Considerazioni di Rico Mariani](http://go.microsoft.com/fwlink/?LinkId=115679)  
  
## Vedere anche  
 [Performance](../../../docs/framework/performance/index.md)   
 [Nozioni di base sulla programmazione](../Topic/Programming%20Concepts.md)   
 [Visual Basic Programming Guide](../Topic/Visual%20Basic%20Programming%20Guide.md)   
 [Guida per programmatori C\#](../Topic/C%23%20Programming%20Guide.md)