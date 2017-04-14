---
title: "Scelta tra classi e Struct | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "classe libreria linee guida di progettazione [.NET Framework], strutture"
  - "classe libreria linee guida di progettazione [.NET Framework], classi"
  - "strutture [.NET Framework], e classi"
  - "classi [.NET Framework], linee guida di progettazione"
  - "indicazioni per la progettazione di tipo, strutture"
  - "strutture di progettazione [.NET Framework]"
  - "classi [.NET Framework] e strutture"
  - "tipo di linee guida di progettazione, classi"
ms.assetid: f8b8ec9b-0ba7-4dea-aadf-a93395cd804f
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Scelta tra classi e Struct
Una delle decisioni di progettazione di base che deve affrontare ogni finestra di progettazione di framework indica se un tipo di progettazione come una classe \(un tipo di riferimento\) o uno struct \(un tipo di valore\). Buona conoscenza delle differenze nel comportamento dei tipi di riferimento e tipi di valore è fondamentale effettuare questa scelta.  
  
 La prima differenza tra i tipi di riferimento e tipi di valore che verrà presa in considerazione è che i tipi di riferimento sono allocati sull'heap e sottoposto a garbage collection, mentre i tipi di valore sono allocati nel stack o inline nella contenente i tipi e deallocati quando lo stack viene rimosso o quando tipo che li contiene viene deallocato. Pertanto, le allocazioni e deallocazioni di tipi di valore sono in genere più economiche di allocazioni e deallocazioni dei tipi di riferimento.  
  
 Successivamente, le matrici di riferimento sono tipi allocati out\-of\-line, vale a dire la matrice di elementi sono riferimenti soli alle istanze del tipo di riferimento che risiedono nell'heap. Matrici di tipi di valore vengono allocate inline, ovvero gli elementi della matrice sono le istanze effettive del tipo di valore. Pertanto, le allocazioni e deallocazioni di matrici di tipi di valore sono molto più conveniente del allocazioni e deallocazioni delle matrici di tipo riferimento. Inoltre, nella maggior parte dei casi matrici di tipi valore comportarsi in modo molto posizionamento ottimale dei riferimenti.  
  
 Differenza successiva è correlata all'utilizzo della memoria. Tipi di valore compattati quando esegue il cast a un tipo di riferimento o una delle interfacce implementate. Ottengono unboxed quando esegue il cast al tipo di valore. Poiché le caselle sono oggetti che vengono allocati nell'heap sottoposto a garbage collection, troppa boxing e unboxing può avere un impatto negativo su heap, il garbage collector e infine le prestazioni dell'applicazione.  Al contrario, si verifica alcun tali boxing come vengono eseguito il cast di tipi di riferimento.  
  
 Le assegnazioni di tipi di riferimento successivamente, copiare il riferimento, mentre le assegnazioni di tipi di valore copiare l'intero valore. Pertanto, le assegnazioni di tipi di riferimento di grandi dimensioni sono più economiche di assegnazioni di tipi di valori di grandi dimensioni.  
  
 Infine, i tipi di riferimento vengono passati per riferimento, mentre i tipi di valore vengono passati per valore. Le modifiche a un'istanza di un tipo di riferimento influiscono su tutti i riferimenti che puntano all'istanza. Istanze del tipo di valore vengono copiate quando vengono passati per valore. Quando un'istanza di un tipo di valore viene modificata, ovviamente non influisce sulle copie. Poiché le copie non vengono create in modo esplicito dall'utente, ma vengono create in modo implicito quando gli argomenti vengono passati o i valori vengono restituiti, tipi di valore che possono essere modificati possono essere confusione a molti utenti. Di conseguenza, i tipi di valore devono essere non modificabili.  
  
 Come regola generale, la maggior parte dei tipi in un framework deve essere classi. Esistono tuttavia alcune situazioni in cui le caratteristiche di un tipo valore rendono più appropriato per l'utilizzo delle strutture.  
  
 **✓ PROVARE** definire una struttura invece di una classe, se le istanze del tipo sono di piccole dimensioni e di breve durata o vengono comunemente incorporate in altri oggetti.  
  
 **X evitare** la definizione di una struttura, a meno che il tipo dispone di tutte le caratteristiche seguenti:  
  
-   Logicamente rappresenta un singolo valore, simile ai tipi primitivi \(`int`, `double`, ecc.\).  
  
-   Ha una dimensione di istanza inferiore a 16 byte.  
  
-   Non è modificabile.  
  
-   Non dovranno essere sottoposto a boxing frequentemente.  
  
 In tutti gli altri casi, è necessario definire i tipi di classi.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di tipo](../../../docs/standard/design-guidelines/type.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)