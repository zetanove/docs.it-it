---
title: "Vantaggi dei generics (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "generics [C#], vantaggi"
ms.assetid: 80f037cd-9ea7-48be-bfc1-219bfb2d4277
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# Vantaggi dei generics (Guida per programmatori C#)
I generics rappresentano la soluzione a una limitazione presente nelle versioni precedenti di Common Language Runtime e del linguaggio C\#, in cui la generalizzazione viene effettuata mediante il cast di tipi in e dal tipo base universale <xref:System.Object>.  Una classe generica consente invece di creare una raccolta indipendente dai tipi in fase di compilazione.  
  
 È possibile dimostrare le limitazioni associate all'utilizzo di classi di raccolte non generiche scrivendo un breve programma in cui si utilizza la classe Collection <xref:System.Collections.ArrayList> della libreria di classi di .NET Framework.  <xref:System.Collections.ArrayList> è una classe Collection estremamente utile che è possibile utilizzare senza modifiche per archiviare qualsiasi tipo di riferimento o di valore.  
  
 [!code-cs[csProgGuideGenerics#4](../../../csharp/programming-guide/generics/codesnippet/CSharp/benefits-of-generics_1.cs)]  
  
 Questa soluzione presenta tuttavia anche alcuni svantaggi.  Qualsiasi tipo di riferimento o di valore aggiunto a <xref:System.Collections.ArrayList> viene implicitamente sottoposto a upcast in <xref:System.Object>.  Se gli elementi sono tipi di valore, devono essere boxed quando vengono aggiunti all'elenco e unboxed quando vengono recuperati.  Le operazioni di cast e quelle di boxing e unboxing influiscono negativamente sulle prestazioni. L'effetto delle conversioni boxing e unboxing può essere piuttosto significativo nelle situazioni in cui è necessario scorrere gli elementi di raccolte di grandi dimensioni.  
  
 L'altra limitazione è la mancanza di controllo dei tipi in fase di compilazione. Poiché <xref:System.Collections.ArrayList> esegue il cast di tutti gli elementi in <xref:System.Object>, non è possibile impedire situazioni simili a quella riportata di seguito nel codice client in fase di compilazione:  
  
 [!code-cs[csProgGuideGenerics#5](../../../csharp/programming-guide/generics/codesnippet/CSharp/benefits-of-generics_2.cs)]  
  
 Anche se perfettamente accettabile e a volte intenzionale se si crea una raccolta eterogenea, la combinazione di stringhe e `ints` in un'unica classe <xref:System.Collections.ArrayList> si rivela nella maggior parte dei casi un errore di programmazione, che verrà rilevato solo in fase di esecuzione.  
  
 Nelle versioni 1.0 e 1.1 del linguaggio C\# era possibile evitare i rischi del codice generalizzato nelle classi Collection della libreria di classi base di .NET Framework solo scrivendo raccolte specifiche di tipi.  Ovviamente, poiché una classe di questo tipo non è riutilizzabile per più di un tipo di dati, si perdono i vantaggi della generalizzazione ed è necessario riscrivere la classe per ogni tipo che verrà archiviato.  
  
 Per la classe <xref:System.Collections.ArrayList> e altre classi simili è in realtà necessario specificare nel codice client, per ogni singola istanza, il particolare tipo di dati che si prevede di utilizzare.  In questo modo non è più necessario eseguire l'upcast in `T:System.Object` ed è inoltre possibile demandare al compilatore il controllo dei tipi.  In altre parole, la classe <xref:System.Collections.ArrayList> richiede un parametro di tipo,  esattamente ciò che viene fornito dai generics.  Nella raccolta <xref:System.Collections.Generic.List%601> generica dello spazio dei nomi `N:System.Collections.Generic` la stessa operazione di aggiunta di elementi alla raccolta è simile a quella riportata di seguito:  
  
 [!code-cs[csProgGuideGenerics#6](../../../csharp/programming-guide/generics/codesnippet/CSharp/benefits-of-generics_3.cs)]  
  
 Per il codice client, l'unica sintassi aggiunta con <xref:System.Collections.Generic.List%601> rispetto a <xref:System.Collections.ArrayList> è l'argomento di tipo nella dichiarazione e nella creazione di istanze.  Anche se tale codifica implica una maggiore complessità, consente di creare un elenco non solo più sicuro di <xref:System.Collections.ArrayList>, ma anche sensibilmente più veloce, soprattutto quando le voci dell'elenco sono tipi di valore.  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [Boxing e unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)   
 [Procedure consigliate relative alle raccolte](http://go.microsoft.com/fwlink/?LinkId=112403)