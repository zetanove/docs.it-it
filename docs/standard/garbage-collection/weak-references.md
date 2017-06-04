---
title: "Weak References | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "weak references, short"
  - "weak references, using"
  - "weak references, long"
  - "garbage collection, weak references"
ms.assetid: 6a600fe5-3af3-4c64-82da-10a0a8e2d79b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Weak References
Il Garbage Collector non può raccogliere un oggetto utilizzato da un'applicazione mentre il codice dell'applicazione può raggiungere tale oggetto.  In questo caso si dice che l'applicazione ha un riferimento forte all'oggetto.  
  
 Un riferimento debole consente al Garbage Collector di raccogliere l'oggetto, senza tuttavia impedire all'applicazione di accedervi.  Tale riferimento rimane valido a tempo indeterminato finché l'oggetto non viene raccolto quando non esiste alcun riferimento forte.  Quando si utilizza un riferimento debole, l'applicazione può comunque ottenere un riferimento forte all'oggetto, il quale però non può essere raccolto.  Vi è tuttavia sempre il rischio che il Garbage Collector arrivi all'oggetto prima che venga ristabilito un riferimento forte.  
  
 I riferimenti deboli sono utili per gli oggetti che utilizzano una quantità elevata di memoria, ma che possono essere ricreati facilmente se vengono recuperati dalla Garbage Collection.  
  
 Si supponga che una visualizzazione struttura in un'applicazione Windows Form presenti all'utente un complesso insieme gerarchico di opzioni.  Se i dati sottostanti sono di dimensioni considerevoli, non è efficiente tenere in memoria la struttura ad albero mentre l'utente esegue un'altra operazione all'interno dell'applicazione.  
  
 Quando l'utente passa a un'altra area dell'applicazione, è possibile utilizzare la classe <xref:System.WeakReference> per creare un riferimento debole alla struttura ad albero e distruggere tutti i riferimenti forti.  Quando l'utente torna alla struttura ad albero, l'applicazione tenta di ottenere un riferimento forte alla struttura e, se il tentativo riesce, evita di ricostruirla.  
  
 Per stabilire un riferimento debole a un oggetto, è necessario creare una classe <xref:System.WeakReference> utilizzando l'istanza dell'oggetto di cui si desidera tenere traccia.  È quindi necessario impostare la proprietà <xref:System.WeakReference.Target%2A> su tale oggetto e impostare la referenza originale all'oggetto su `null`.  Per un esempio di codice, vedere <xref:System.WeakReference> nella libreria di classi.  
  
## Riferimenti deboli brevi e lunghi  
 È possibile creare un riferimento debole breve oppure lungo:  
  
-   Short  
  
     La destinazione di un riferimento debole breve diventa `null` quando l'oggetto viene recuperato dalla Garbage Collection.  Il riferimento debole è di per sé un oggetto gestito ed è soggetto alla Garbage Collection come qualsiasi altro oggetto gestito.  Un riferimento debole breve è il costruttore predefinito per <xref:System.WeakReference>.  
  
-   Long  
  
     Un riferimento debole lungo viene mantenuto dopo la chiamata al metodo <xref:System.Object.Finalize%2A> dell'oggetto.  In questo modo l'oggetto può essere ricreato, ma il relativo stato resta imprevedibile.  Per utilizzare un riferimento lungo, specificare `true` nel costruttore <xref:System.WeakReference>.  
  
     Se al tipo dell'oggetto non è associato un metodo <xref:System.Object.Finalize%2A>, verrà applicata la funzionalità riferimento debole breve e il riferimento debole sarà valido solo finché la destinazione non verrà raccolta, eventualità che può verificarsi in qualsiasi momento dopo l'esecuzione del finalizzatore.  
  
 Per stabilire un riferimento forte e utilizzare nuovamente l'oggetto, eseguire il cast della proprietà <xref:System.WeakReference.Target%2A> di una classe <xref:System.WeakReference> sul tipo dell'oggetto.  Se la proprietà <xref:System.WeakReference.Target%2A> restituisce `null`, l'oggetto è stato raccolto. In caso contrario, sarà possibile continuare a utilizzare l'oggetto perché l'applicazione ha ottenuto di nuovo un riferimento forte a esso.  
  
## Linee guida per l'utilizzo di riferimenti deboli  
 Utilizzare riferimenti deboli lunghi solo quando necessario, dal momento che lo stato dell'oggetto risulta imprevedibile dopo la finalizzazione.  
  
 Evitare di utilizzare riferimenti deboli a oggetti di piccole dimensioni perché il puntatore potrebbe avere le stesse dimensioni o essere addirittura più grande.  
  
 Evitare di utilizzare riferimenti deboli come soluzione automatica a problemi di gestione della memoria.  Sviluppare invece criteri efficaci di memorizzazione nella cache per gestire gli oggetti dell'applicazione.  
  
## Vedere anche  
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)