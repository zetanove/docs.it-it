---
title: "Creating Threads and Passing Data at Start Time | Microsoft Docs"
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
  - "threading [.NET Framework], creating"
  - "threading [.NET Framework], passing data to threads"
  - "threading [.NET Framework], retrieving data from threads"
ms.assetid: 52b32222-e185-4f42-91a7-eaca65c0ab6d
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Creating Threads and Passing Data at Start Time
Quando viene creato un processo di sistema operativo, quest'ultimo inserisce un thread per eseguire del codice in quel processo, inclusi gli eventuali domini dell'applicazione originali.  Da quel punto in poi i domini dell'applicazione possono essere creati e distrutti senza che sia necessario creare e distruggere alcun thread del sistema operativo.  Se è in esecuzione il codice gestito, è possibile ottenere un oggetto <xref:System.Threading.Thread> per il thread in esecuzione nel dominio dell'applicazione corrente recuperando la proprietà <xref:System.Threading.Thread.CurrentThread%2A> statica di tipo <xref:System.Threading.Thread>.  In questo argomento viene illustrata la creazione di thread e vengono illustrate le possibili alternative per il passaggio di dati alla routine del thread.  
  
## Creazione di un thread  
 La creazione di un nuovo oggetto <xref:System.Threading.Thread> determina la generazione di un nuovo thread gestito.  La classe <xref:System.Threading.Thread> dispone di costruttori che accettano un delegato <xref:System.Threading.ThreadStart> o <xref:System.Threading.ParameterizedThreadStart>. Il delegato esegue il wrapping del metodo richiamato dal nuovo thread quando viene eseguita una chiamata al metodo <xref:System.Threading.Thread.Start%2A>.  Chiamando più volte <xref:System.Threading.Thread.Start%2A>, verrà generata un'eccezione <xref:System.Threading.ThreadStateException>.  
  
 Il metodo <xref:System.Threading.Thread.Start%2A> restituisce immediatamente un valore, spesso prima dell'avvio effettivo del nuovo thread.  È possibile utilizzare le proprietà <xref:System.Threading.Thread.ThreadState%2A> e <xref:System.Threading.Thread.IsAlive%2A> per determinare lo stato del thread in qualsiasi momento, ma queste proprietà non dovrebbero mai essere utilizzate per la sincronizzazione delle attività dei thread.  
  
> [!NOTE]
>  Una volta avviato un thread, non è necessario mantenere un riferimento all'oggetto <xref:System.Threading.Thread>.  Il thread continua l'esecuzione fino al termine della routine del thread.  
  
 Nell'esempio di codice che segue vengono creati due nuovi thread per chiamare i metodi di istanza e statici su un altro oggetto.  
  
 [!code-cpp[System.Threading.ThreadStart2#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source2.cpp#2)]
 [!code-csharp[System.Threading.ThreadStart2#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source2.cs#2)]
 [!code-vb[System.Threading.ThreadStart2#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source2.vb#2)]  
  
## Passaggio di dati ai thread e recupero di dati dai thread  
 In .NET Framework versione 2.0, il delegato <xref:System.Threading.ParameterizedThreadStart> offre una tecnica semplice per passare un oggetto contenente dati a un thread quando viene chiamato l'overload del metodo <xref:System.Threading.Thread.Start%2A?displayProperty=fullName>.  Per un esempio di codice, vedere <xref:System.Threading.ParameterizedThreadStart>.  
  
 L'utilizzo del delegato <xref:System.Threading.ParameterizedThreadStart> non è una tecnica di passaggio dei dati indipendente dai tipi perché l'overload del metodo <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> accetta qualsiasi oggetto.  Un'alternativa consiste nell'incapsulare la routine del thread e i dati in una classe di supporto e nell'utilizzare il delegato <xref:System.Threading.ThreadStart> per eseguire la routine del thread.  Questa tecnica è illustrata nei due esempi di codice riportati di seguito.  
  
 Nessuno di questi delegati restituisce un valore perché non è possibile definire una posizione per la restituzione dei dati da una chiamata asincrona.  Per recuperare i risultati di un metodo di thread, è possibile utilizzare un metodo di callback, come illustrato nel secondo esempio di codice.  
  
 [!code-cpp[System.Threading.ThreadStart2#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source3.cpp#3)]
 [!code-csharp[System.Threading.ThreadStart2#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source3.cs#3)]
 [!code-vb[System.Threading.ThreadStart2#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source3.vb#3)]  
  
### Recupero di dati con metodi di callback  
 Negli esempi riportati di seguito viene illustrato il recupero di dati da un thread tramite un metodo di callback.  Nel costruttore della classe contenente i dati e il metodo di thread viene accettato anche un delegato che rappresenta il metodo di callback. Prima del termine del metodo di thread, viene richiamato il delegato del callback.  
  
 [!code-cpp[System.Threading.ThreadStart2#4](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source4.cpp#4)]
 [!code-csharp[System.Threading.ThreadStart2#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source4.cs#4)]
 [!code-vb[System.Threading.ThreadStart2#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source4.vb#4)]  
  
## Vedere anche  
 <xref:System.Threading.Thread>   
 <xref:System.Threading.ThreadStart>   
 <xref:System.Threading.ParameterizedThreadStart>   
 <xref:System.Threading.Thread.Start%2A?displayProperty=fullName>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)