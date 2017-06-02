---
title: "Interlocked Operations | Microsoft Docs"
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
  - "Interlocked class, about Interlocked class"
  - "threading [.NET Framework], Interlocked class"
ms.assetid: cbda7114-c752-4f3e-ada1-b1e8dd262f2b
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Interlocked Operations
La classe <xref:System.Threading.Interlocked> fornisce metodi per la sincronizzazione dell'accesso a una variabile condivisa da più thread.  I thread di processi differenti possono utilizzare questo meccanismo se la variabile si trova nella memoria condivisa.  Le operazioni interlocked sono atomiche. In altri termini, un'intera operazione costituisce un'unità che non può essere interrotta da un'altra operazione interlocked sulla stessa variabile.  Questa caratteristica è importante nei sistemi operativi con multithreading preemptive, in cui un thread può essere sospeso dopo il caricamento di un valore da un indirizzo di memoria, ma prima che sia possibile modificarlo e memorizzarlo.  
  
 La classe <xref:System.Threading.Interlocked> fornisce le seguenti operazioni:  
  
-   In .NET Framework versione 2.0 il metodo <xref:System.Threading.Interlocked.Add%2A> aggiunge un valore integer a una variabile e restituisce il nuovo valore della variabile.  
  
-   In .NET Framework versione 2.0 il metodo <xref:System.Threading.Interlocked.Read%2A> legge un valore integer a 64 bit come un'operazione atomica.  Questa caratteristica è utile sui sistemi a 32 bit, in cui la lettura di un intero a 64 bit non è normalmente un'operazione atomica.  
  
-   I metodi <xref:System.Threading.Interlocked.Increment%2A> e <xref:System.Threading.Interlocked.Decrement%2A> incrementano o decrementano una variabile e restituiscono il valore risultante.  
  
-   Il metodo <xref:System.Threading.Interlocked.Exchange%2A> esegue uno scambio atomico del valore in una variabile specificata, restituendo tale valore e sostituendolo con uno nuovo.  In .NET Framework versione 2.0 è possibile utilizzare un overload generico di questo metodo per eseguire questo scambio su una variabile di qualsiasi tipo di riferimento.  Vedere <xref:System.Threading.Interlocked.Exchange%60%601%28%60%600%40%2C%60%600%29>.  
  
-   Anche il metodo <xref:System.Threading.Interlocked.CompareExchange%2A> scambia due valori, ma in base al risultato di un confronto.  In .NET Framework versione 2.0 è possibile utilizzare un overload generico di questo metodo per eseguire questo scambio su una variabile di qualsiasi tipo di riferimento.  Vedere <xref:System.Threading.Interlocked.CompareExchange%60%601%28%60%600%40%2C%60%600%2C%60%600%29>.  
  
 Nei moderni processori i metodi della classe <xref:System.Threading.Interlocked> possono essere spesso implementati da una singola istruzione.  In questo modo, forniscono una sincronizzazione ad alte prestazioni e possono essere utilizzati per compilare meccanismi di sincronizzazione di livello più elevato, come gli spin lock.  
  
 Per un esempio di utilizzo combinato delle classi <xref:System.Threading.Monitor> e <xref:System.Threading.Interlocked>, vedere [Monitor](../Topic/Monitors.md).  
  
## Esempio di metodo CompareExchange  
 Il metodo <xref:System.Threading.Interlocked.CompareExchange%2A> può essere utilizzato per la protezione di calcoli più complessi rispetto al semplice incremento o decremento.  Nell'esempio riportato di seguito viene illustrato un metodo thread\-safe per ottenere un totale parziale memorizzato come numero a virgola mobile. Per gli interi, il metodo <xref:System.Threading.Interlocked.Add%2A> costituisce una soluzione più semplice. Per esempi di codice completi, vedere gli overload di <xref:System.Threading.Interlocked.CompareExchange%2A> che accettano argomenti a virgola mobile, con precisione singola e precisione doppia \(<xref:System.Threading.Interlocked.CompareExchange%28System.Single%40%2CSystem.Single%2CSystem.Single%29> e <xref:System.Threading.Interlocked.CompareExchange%28System.Double%40%2CSystem.Double%2CSystem.Double%29>\).  
  
 [!code-cpp[Conceptual.Interlocked#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interlocked/cpp/source1.cpp#1)]
 [!code-csharp[Conceptual.Interlocked#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interlocked/cs/source1.cs#1)]
 [!code-vb[Conceptual.Interlocked#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interlocked/vb/source1.vb#1)]  
  
## Overload non tipizzati di Exchange e CompareExchange  
 Gli overload dei metodi <xref:System.Threading.Interlocked.Exchange%2A> e <xref:System.Threading.Interlocked.CompareExchange%2A> accettano argomenti di tipo <xref:System.Object>.  Il primo argomento di ciascuno di questi overload è `ref Object` \(`ByRef … As Object` in Visual Basic\) e, per garantire l'indipendenza dai tipi, la variabile passata a questo argomento deve essere rigorosamente di tipo <xref:System.Object>. Non è possibile eseguire semplicemente il cast del primo argomento nel tipo <xref:System.Object> quando vengono chiamati questi metodi.  
  
> [!NOTE]
>  In .NET Framework versione 2.0 utilizzare gli overload generici dei metodi <xref:System.Threading.Interlocked.Exchange%2A> e <xref:System.Threading.Interlocked.CompareExchange%2A> per scambiare variabili fortemente tipizzate.  
  
 Nell'esempio di codice riportato di seguito viene illustrata una proprietà di tipo `ClassA` che può essere utilizzata una sola volta poiché può essere implementata in .NET Framework versione 1.0 o 1.1.  
  
 [!code-cpp[Conceptual.Interlocked#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interlocked/cpp/source2.cpp#2)]
 [!code-csharp[Conceptual.Interlocked#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interlocked/cs/source2.cs#2)]
 [!code-vb[Conceptual.Interlocked#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interlocked/vb/source2.vb#2)]  
  
## Vedere anche  
 <xref:System.Threading.Interlocked>   
 <xref:System.Threading.Monitor>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)