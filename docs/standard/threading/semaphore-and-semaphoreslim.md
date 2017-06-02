---
title: "Semaphore and SemaphoreSlim | Microsoft Docs"
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
  - "counting semaphores"
  - "semaphores"
  - "threading [.NET Framework], cross-process synchronization"
  - "Semaphore class, about Semaphore class"
  - "SemaphoreSlim class, about SemaphoreSlim class"
  - "threading [.NET Framework], Semaphore class"
ms.assetid: 7722a333-b974-47a2-a7c0-f09097fb644e
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# Semaphore and SemaphoreSlim
La classe <xref:System.Threading.Semaphore?displayProperty=fullName> rappresenta un semaforo denominato \(systemwide\) o locale.  È un semplice wrapper per l'oggetto semaforo Win32.  I semafori Win32 sono semafori di conteggio che possono essere usati per controllare l'accesso a un pool di risorse.  
  
 La classe <xref:System.Threading.SemaphoreSlim> rappresenta un semaforo leggero e veloce che può essere usato per l'attesa in un singolo processo quando si prevedono tempi di attesa molto brevi.  <xref:System.Threading.SemaphoreSlim> si basa quanto più possibile sulle primitive di sincronizzazione fornite da Common Language Runtime \(CLR\).  Tuttavia, fornisce anche gli handle di attesa basati sul kernel e inizializzati in modo differito necessari per supportare l'attesa in più semafori.  <xref:System.Threading.SemaphoreSlim> supporta anche l'utilizzo di token di annullamento, ma non supporta i semafori denominati né l'utilizzo di un handle di attesa per la sincronizzazione.  
  
## Gestione di una risorsa limitata  
 I thread entrano nel semaforo chiamando il metodo <xref:System.Threading.WaitHandle.WaitOne%2A>, che viene ereditato dalla classe <xref:System.Threading.WaitHandle>, nel caso di un oggetto <xref:System.Threading.Semaphore?displayProperty=fullName>, oppure il metodo <xref:System.Threading.SemaphoreSlim.Wait%2A?displayProperty=fullName> o <xref:System.Threading.SemaphoreSlim.WaitAsync%2A?displayProperty=fullName>, nel caso di un oggetto <xref:System.Threading.SemaphoreSlim>.  Al termine della chiamata, il conteggio del semaforo viene decrementato.  Quando un thread richiede accesso e il conteggio è zero, il thread si blocca.  Quando i thread rilasciano il semaforo chiamando il metodo <xref:System.Threading.Semaphore.Release%2A?displayProperty=fullName> o <xref:System.Threading.SemaphoreSlim.Release%2A?displayProperty=fullName>, i thread bloccati potranno entrare.  Per i thread bloccati al semaforo non esiste alcun ordine garantito, ad esempio first\-in, first\-out \(FIFO\) o last\-in, first\-out \(LIFO\).  
  
 Un thread può entrare nel semaforo più volte chiamando il metodo <xref:System.Threading.WaitHandle.WaitOne%2A> dell'oggetto <xref:System.Threading.Semaphore?displayProperty=fullName> oppure il metodo <xref:System.Threading.SemaphoreSlim.Wait%2A> dell'oggetto <xref:System.Threading.SemaphoreSlim> ripetutamente.  Per rilasciare il semaforo, il thread può chiamare l'overload del metodo <xref:System.Threading.Semaphore.Release?displayProperty=fullName> o <xref:System.Threading.SemaphoreSlim.Release?displayProperty=fullName> per lo stesso numero di volte oppure chiamare l'overload del metodo <xref:System.Threading.Semaphore.Release%28System.Int32%29?displayProperty=fullName> o <xref:System.Threading.SemaphoreSlim.Release%28System.Int32%29?displayProperty=fullName> e specificare il numero di accessi da rilasciare.  
  
### Semafori e identità thread  
 I due tipi di semaforo non applicano l'identità thread alle chiamate ai metodi <xref:System.Threading.WaitHandle.WaitOne%2A>, <xref:System.Threading.SemaphoreSlim.Wait%2A>, <xref:System.Threading.Semaphore.Release%2A> e <xref:System.Threading.SemaphoreSlim.Release%2A?displayProperty=fullName>.  Ad esempio, uno scenario di utilizzo comune per i semafori implica un thread producer e un thread consumer, di cui uno incrementa sempre il conteggio del semaforo e l'altro lo decrementa sempre.  
  
 È compito del programmatore garantire che un thread non rilasci il semaforo troppe volte.  Ad esempio, si consideri un semaforo con un conteggio massimo di due e il thread A e B accedano entrambi al semaforo.  Se un errore di programmazione nel thread B fa sì che venga chiamato `Release` due volte, entrambe le chiamate hanno esito positivo.  Il conteggio sul semaforo è completo e quando il thread A alla fine chiama `Release`, viene generata una <xref:System.Threading.SemaphoreFullException>.  
  
## Semafori denominati  
 Il sistema operativo Windows consente di assegnare nomi ai semafori.  Un semaforo denominato è a livello di sistema:  vale a dire che, una volta creato, il semaforo denominato è visibile a tutti i thread in tutti i processi.  In questo modo, il semaforo denominato può essere usato per sincronizzare le attività di processi e thread.  
  
 È possibile creare un oggetto <xref:System.Threading.Semaphore> che rappresenta un semaforo di sistema denominato usando uno dei costruttori che specifica un nome.  
  
> [!NOTE]
>  Poiché i semafori denominati sono a livello di sistema, è possibile avere più oggetti <xref:System.Threading.Semaphore> che rappresentano lo stesso semaforo denominato.  A ogni chiamata a un costruttore o al metodo <xref:System.Threading.Semaphore.OpenExisting%2A?displayProperty=fullName> viene creato un nuovo oggetto <xref:System.Threading.Semaphore>.  Specificando lo stesso nome ripetutamente verranno creati più oggetti che rappresentano lo stesso semaforo denominato.  
  
 Prestare attenzione quando si usano i semafori denominati:  siccome sono a livello di sistema, un altro processo che usa lo stesso nome può accedere al semaforo in modo imprevisto.  Il malware in esecuzione sullo stesso computer potrebbe sfruttare questa opportunità per un attacco Denial of Service.  
  
 Usare il controllo degli accessi per proteggere un oggetto <xref:System.Threading.Semaphore> che rappresenta un semaforo denominato, preferibilmente usando un costruttore che specifichi un oggetto <xref:System.Security.AccessControl.SemaphoreSecurity?displayProperty=fullName>.  È anche possibile applicare la sicurezza del controllo degli accessi usando il metodo <xref:System.Threading.Semaphore.SetAccessControl%2A?displayProperty=fullName>, ma in tal modo verrà creata una finestra di vulnerabilità tra l'ora di creazione del semaforo e l'ora in cui viene protetto.  La protezione dei semafori con la sicurezza del controllo degli accessi aiuta a impedire gli attacchi dannosi, ma non risolve il problema dei conflitti di nomi non intenzionali.  
  
## Vedere anche  
 <xref:System.Threading.Semaphore>   
 <xref:System.Threading.SemaphoreSlim>   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)