---
title: "EventWaitHandle | Microsoft Docs"
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
  - "threading [.NET Framework], EventWaitHandle class"
  - "EventWaitHandle class"
  - "event wait handles [.NET Framework]"
  - "threading [.NET Framework], cross-process synchronization"
ms.assetid: 11ee0b38-d663-4617-b793-35eb6c64e9fc
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# EventWaitHandle
La classe <xref:System.Threading.EventWaitHandle> consente la comunicazione tra i thread mediante la segnalazione e l'attesa di segnali.  Gli handle di attesa dell'evento, definiti anche semplicemente eventi, sono handle di attesa che possono essere segnalati per rilasciare uno o più thread in attesa.  In seguito alla segnalazione, un handle di attesa dell'evento viene reimpostato manualmente o automaticamente.  La classe <xref:System.Threading.EventWaitHandle> può rappresentare un handle di attesa dell'evento locale \(evento locale\) o un handle di attesa dell'evento di sistema denominato \(evento denominato o di sistema, visibile a tutti i processi\).  
  
> [!NOTE]
>  Gli handle di attesa dell'evento non sono eventi secondo il significato attribuito a tale termine in .NET Framework.  Non sono infatti implicati delegati o gestori eventi.  Per descriverli viene adoperato il termine evento in quanto in passato sono stati definiti eventi del sistema operativo e perché la segnalazione dell'handle di attesa indica ai thread in attesa il verificarsi di un evento.  
  
 Sia gli handle di attesa dell'evento locale che denominato utilizzano oggetti di sincronizzazione del sistema, che sono protetti dai wrapper <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> per garantire il rilascio delle risorse.  È possibile utilizzare il metodo <xref:System.Threading.WaitHandle.System%23IDisposable%23Dispose%2A> per liberare le risorse al termine dell'utilizzo dell'oggetto.  
  
## Handle di attesa dell'evento di reimpostazione automatica  
 Per creare un evento di reimpostazione automatica è possibile specificare <xref:System.Threading.EventResetMode?displayProperty=fullName> quando si crea l'oggetto <xref:System.Threading.EventWaitHandle>.  Come indicato dal nome, questo evento di sincronizzazione viene reimpostato automaticamente quando viene segnalato, dopo il rilascio di un singolo thread in attesa.  Segnalare l'evento chiamando il relativo metodo <xref:System.Threading.EventWaitHandle.Set%2A>.  
  
 In genere, gli eventi di reimpostazione automatica consentono di accedere in modo esclusivo a una risorsa di un singolo thread alla volta.  Un thread richiede la risorsa chiamando il metodo <xref:System.Threading.WaitHandle.WaitOne%2A>.  Se nessun altro thread contiene l'handle di attesa, il metodo restituisce `true` e il thread chiamante ha il controllo della risorsa.  
  
> [!IMPORTANT]
>  Come con tutti i meccanismi di sincronizzazione, è necessario verificare che tutti i percorsi di codice siano in attesa sull'handle di attesa appropriato prima di accedere a una risorsa protetta.  La sincronizzazione dei thread è un processo cooperativo.  
  
 Se un evento di reimpostazione automatica viene segnalato quando non vi sono thread in attesa, rimarrà segnalato fino al tentativo di un thread di mettersi in attesa.  L'evento rilascia il thread e viene reimpostato immediatamente bloccando i thread successivi.  
  
## Handle di attesa dell'evento di reimpostazione manuale  
 Per creare un evento di reimpostazione manuale è possibile specificare <xref:System.Threading.EventResetMode?displayProperty=fullName> quando si crea l'oggetto <xref:System.Threading.EventWaitHandle>.  Come indicato dal nome, questo evento di sincronizzazione deve essere reimpostato manualmente dopo essere stato segnalato.  Per proseguire l'esecuzione del thread in attesa sull'handle evento, senza causare alcun blocco fino alla reimpostazione del thread stesso, è possibile chiamare il relativo metodo <xref:System.Threading.EventWaitHandle.Reset%2A>.  
  
 Un evento di reimpostazione manuale ha la stessa funzione del cancello di un recinto per cavalli.  Quando l'evento non viene segnalato, i thread che sono in attesa su di esso si bloccano, come i cavalli in un recinto.  Quando l'evento viene segnalato, chiamandone il metodo <xref:System.Threading.EventWaitHandle.Set%2A>, tutti i thread in attesa sono liberi di essere eseguiti.  L'evento rimane segnalato fino alla chiamata del relativo metodo <xref:System.Threading.EventWaitHandle.Reset%2A>.  Ciò rende l'evento di reimpostazione manuale il sistema ideale per supportare i thread che devono attendere il completamento delle attività di altri thread.  
  
 Analogamente all'uscita dei cavalli dal recinto, la pianificazione dei thread rilasciati da parte del sistema operativo e la ripresa dell'esecuzione sono operazioni che richiedono tempo.  Se il metodo <xref:System.Threading.EventWaitHandle.Reset%2A> viene chiamato prima della ripresa dell'esecuzione di tutti i thread, i thread rimanenti si bloccano di nuovo.  I thread di cui viene ripresa l'esecuzione e quelli che vengono bloccati dipendono da fattori casuali quali il carico sul sistema, il numero di thread in attesa dell'utilità di pianificazione e così via.  Non costituisce un problema la terminazione del thread che segnala l'evento dopo la segnalazione, scenario che rappresenta il modello di utilizzo più comune.  Se si desidera che il thread che ha segnalato l'evento avvii una nuova attività dopo la ripresa di tutti i thread in attesa, è necessario bloccarlo fino a tale ripresa.  In caso contrario, si verificherà una race condition e il comportamento del codice sarà imprevedibile.  
  
## Funzionalità comuni a eventi automatici e manuali  
 In genere, uno o più thread vengono bloccati su un oggetto <xref:System.Threading.EventWaitHandle> fino a quando un thread sbloccato chiama il metodo <xref:System.Threading.EventWaitHandle.Set%2A> che rilascia uno dei thread in attesa, nel caso di eventi di reimpostazione automatica, o tutti i thread, nel caso di eventi di reimpostazione manuale.  Un thread può segnalare un <xref:System.Threading.EventWaitHandle> e successivamente bloccarsi su di esso, come in un'operazione atomica, chiamando il metodo <xref:System.Threading.WaitHandle.SignalAndWait%2A?displayProperty=fullName> statico.  
  
 Gli oggetti <xref:System.Threading.EventWaitHandle> possono essere utilizzati con i metodi statici <xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=fullName> e <xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=fullName>.  Poiché le classi <xref:System.Threading.EventWaitHandle> e <xref:System.Threading.Mutex> derivano entrambe da <xref:System.Threading.WaitHandle>, è possibile utilizzarle con questi metodi.  
  
### Eventi denominati  
 Il sistema operativo Windows consente la denominazione degli handle di attesa dell'evento.  Un evento denominato è valido a livello di sistema,  ovvero, dopo essere stato creato, è visibile a tutti i thread in tutti i processi.  Gli eventi denominati possono essere pertanto utilizzati per sincronizzare le attività dei processi, nonché dei thread.  
  
 È possibile creare un oggetto <xref:System.Threading.EventWaitHandle> che rappresenti un evento di sistema denominato utilizzando uno dei costruttori che specifica un nome dell'evento.  
  
> [!NOTE]
>  Poiché gli eventi denominati sono validi a livello di sistema, è possibile che più oggetti <xref:System.Threading.EventWaitHandle> rappresentino lo stesso evento denominato.  Ogni volta che viene chiamato un costruttore o il metodo <xref:System.Threading.EventWaitHandle.OpenExisting%2A>, viene creato un nuovo oggetto <xref:System.Threading.EventWaitHandle>.  Specificando lo stesso nome ripetutamente vengono creati più oggetti che rappresentano lo stesso evento denominato.  
  
 È consigliabile prestare attenzione nell'utilizzo degli eventi denominati.  Dal momento che sono validi a livello di sistema, un altro processo che utilizza lo stesso nome può bloccare i thread in modo imprevisto.  È possibile che il malware in esecuzione sullo stesso computer si serva di questa situazione come base per un attacco di tipo Denial of Service.  
  
 Utilizzare la sicurezza del controllo di accesso per proteggere un oggetto <xref:System.Threading.EventWaitHandle> che rappresenta un evento denominato, possibilmente mediante un costruttore che specifica un oggetto <xref:System.Security.AccessControl.EventWaitHandleSecurity>.  È inoltre possibile applicare questo tipo di sicurezza utilizzando il metodo <xref:System.Threading.EventWaitHandle.SetAccessControl%2A>. Tuttavia, questo sistema lascia un margine di vulnerabilità tra il momento in cui viene creato l'handle di attesa dell'evento e il momento in cui viene applicata la sicurezza.  L'applicazione della sicurezza del controllo di accesso agli eventi impedisce gli attacchi dannosi ma non risolve il problema dei conflitti di nomi non intenzionali.  
  
> [!NOTE]
>  A differenza della classe <xref:System.Threading.EventWaitHandle>, le classi derivate <xref:System.Threading.AutoResetEvent> e <xref:System.Threading.ManualResetEvent> possono rappresentare solo handle di attesa locali  e non eventi di sistema denominati.  
  
## Vedere anche  
 <xref:System.Threading.EventWaitHandle>   
 <xref:System.Threading.WaitHandle>   
 <xref:System.Threading.AutoResetEvent>   
 <xref:System.Threading.ManualResetEvent>   
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)