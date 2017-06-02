---
title: "releaseHandleFailed MDA | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "managed debugging assistants (MDAs), handles"
  - "release handle failed"
  - "CriticalHandle class, run-time errors"
  - "releaseHandleFailed MDA"
  - "ReleaseHandle method"
  - "SafeHandle class, run-time errors"
  - "MDAs (managed debugging assistants), handles"
ms.assetid: 44cd98ba-95e5-40a1-874d-e8e163612c51
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# releaseHandleFailed MDA
L'assistente al debug gestito `releaseHandleFailed` viene attivato per notificare agli sviluppatori quando il metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> di una classe derivata da <xref:System.Runtime.InteropServices.SafeHandle> o <xref:System.Runtime.InteropServices.CriticalHandle> restituisce `false`.  
  
## Sintomi  
 Perdita di risorse o di memoria  Se si verifica un errore nel metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> della classe che deriva da <xref:System.Runtime.InteropServices.SafeHandle> o <xref:System.Runtime.InteropServices.CriticalHandle>, è possibile che la risorsa incapsulata dalla classe non sia stata rilasciata o eliminata.  
  
## Causa  
 Se si creano classi che derivano da  <xref:System.Runtime.InteropServices.SafeHandle> o <xref:System.Runtime.InteropServices.CriticalHandle>, è necessario fornire l'implementazione del metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>. Di conseguenza, le problematiche sono specifiche della singola risorsa.  È necessario, tuttavia, che siano rispettati i seguenti requisiti:  
  
-   I tipi <xref:System.Runtime.InteropServices.SafeHandle> e <xref:System.Runtime.InteropServices.CriticalHandle> rappresentano wrapper per risorse vitali di un processo.  Una perdita di memoria può rendere il processo inusabile.  
  
-   È necessario che non si verifichi un errore durante l'esecuzione del metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>.  Una volta che il processo acquisisce una risorsa di questo tipo, per rilasciarla è necessario usare il metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>.  Un errore del metodo implica quindi una perdita di risorse.  
  
-   Qualsiasi errore che si verifica durante l'esecuzione del metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>, impedendo il rilascio della risorsa, costituisce un bug nell'implementazione del metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> stesso.  È compito del programmatore assicurare che il contratto venga rispettato, anche se durante l'esecuzione viene chiamato codice creato da altri utenti.  
  
## Risoluzione  
 È necessario esaminare il codice che usa lo specifico tipo <xref:System.Runtime.InteropServices.SafeHandle> \(o <xref:System.Runtime.InteropServices.CriticalHandle>\) che ha generato la notifica dell'assistente al debug gestito per individuare i punti in cui il valore dell'handle non elaborato viene estratto da <xref:System.Runtime.InteropServices.SafeHandle> e copiato in un'altra posizione.  Questa è la causa principale degli errori nelle implementazioni di <xref:System.Runtime.InteropServices.SafeHandle> o <xref:System.Runtime.InteropServices.CriticalHandle>, poiché l'uso del valore dell'handle non elaborato non viene più controllato da Common Language Runtime.  Se successivamente la copia dell'handle non elaborato viene chiusa, può verificarsi un errore in una successiva chiamata a <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> poiché la chiusura viene tentata sullo stesso handle, ormai non più valido.  
  
 Esistono alcune situazioni in cui può verificarsi la duplicazione di un handle non corretto:  
  
-   Individuare le chiamate al metodo <xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A>.  Le chiamate a questo metodo dovrebbero essere molto rare e quelle eventualmente presenti dovrebbero essere circondate da chiamate ai metodi <xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A> e <xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A>.  Questi ultimi specificano l'area di codice in cui il valore dell'handle non elaborato può essere usato in maniera sicura.  Al di fuori di quest'area, o se il conteggio dei riferimenti non viene mai incrementato nella prima posizione, il valore dell'handle può essere invalidato in qualsiasi momento da una chiamata a <xref:System.Runtime.InteropServices.SafeHandle.Dispose%2A> o <xref:System.Runtime.InteropServices.SafeHandle.Close%2A> su un altro thread.  Una volta individuati tutti gli usi di <xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A>, è necessario seguire il percorso dell'handle non elaborato per verificare che non venga passato a qualche componente che chiamerà `CloseHandle` o un altro metodo nativo di basso livello che causerà il rilascio dell'handle.  
  
-   Verificare che l'handle non elaborato appartenga al codice usato per inizializzare <xref:System.Runtime.InteropServices.SafeHandle> con un valore di handle valido.  Se si definisce un oggetto <xref:System.Runtime.InteropServices.SafeHandle> intorno a un handle che non appartiene al codice senza impostare il parametro `ownsHandle` su `false` nel costruttore base, sia <xref:System.Runtime.InteropServices.SafeHandle> che il vero proprietario dell'handle possono tentare di chiudere l'handle, generando quindi un errore in <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> se <xref:System.Runtime.InteropServices.SafeHandle> non riesce a chiudere l'handle prima del proprietario.  
  
-   Quando viene eseguito il marshalling di <xref:System.Runtime.InteropServices.SafeHandle> tra domini applicazione, verificare che la derivazione di <xref:System.Runtime.InteropServices.SafeHandle> usata sia stata contrassegnata come serializzabile.  Nei rari casi in cui una classe derivata da <xref:System.Runtime.InteropServices.SafeHandle> sia stata resa serializzabile, tale classe deve implementare l'interfaccia <xref:System.Runtime.Serialization.ISerializable> o usare una delle altre tecniche che consentono di controllare manualmente il processo di serializzazione e deserializzazione.  Questa operazione è necessaria poiché l'azione di serializzazione predefinita consiste nel creare un clone bit per bit del valore dell'handle non elaborato incluso e questo fa sì che due istanze di <xref:System.Runtime.InteropServices.SafeHandle> ritengano di essere proprietarie dello stesso handle.  A un certo punto entrambe tenteranno di chiamare <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> sullo stesso handle,  ma ovviamente la seconda istanza di <xref:System.Runtime.InteropServices.SafeHandle> non riuscirà ad eseguire questa operazione.  La procedura corretta da seguire quando si serializza un oggetto <xref:System.Runtime.InteropServices.SafeHandle> consiste nel chiamare la funzione `DuplicateHandle` o una funzione simile per il tipo di handle nativo in modo da creare una copia valida distinta dell'handle.  Se il tipo di handle non supporta questa funzione, il tipo <xref:System.Runtime.InteropServices.SafeHandle> che lo include non può essere reso serializzabile.  
  
-   È possibile individuare il punto in cui un handle viene chiuso anticipatamente, causando un errore al momento della chiamata finale al metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>, inserendo un punto di interruzione sulla routine nativa usata per rilasciare l'handle, ad esempio la funzione `CloseHandle`.  Questo potrebbe non essere possibile in situazioni di sovraccarico o anche nel caso di test funzionali di medie dimensioni a causa del volume elevato di traffico spesso associato a tali routine.   In questo caso può essere utile instrumentare il codice che chiama il metodo di rilascio nativo, allo scopo di catturare l'identità del chiamante, o eventualmente eseguire una traccia dello stack completa, in modo da ottenere il valore dell'handle rilasciato,  che può essere quindi confrontato con il valore indicato da questo assistente al debug gestito.  
  
-   Alcuni tipi di handle nativi, ad esempio tutti gli handle Win32 che possono essere rilasciati mediante la funzione `CloseHandle`, condividono lo stesso spazio dei nomi dell'handle.  Il rilascio errato di un tipo di handle può causare problemi con un altro handle.  Se ad esempio si chiude involontariamente due volte un handle di evento Win32, è possibile che venga chiuso prematuramente un handle di file apparentemente non correlato.  Questo problema si verifica quando l'handle viene rilasciato e il valore dell'handle può essere usato per controllare un'altra risorsa, eventualmente di un altro tipo.  Se in questa situazione viene eseguito per errore un secondo rilascio, è possibile che venga invalidato l'handle di un thread non correlato.  
  
## Effetto sull'ambiente di esecuzione  
 L'assistente al debug gestito non ha alcun effetto su CLR.  
  
## Output  
 Un messaggio indicante che un oggetto <xref:System.Runtime.InteropServices.SafeHandle> o <xref:System.Runtime.InteropServices.CriticalHandle> non è riuscito a rilasciare correttamente l'handle.  Ad esempio:  
  
```  
"A SafeHandle or CriticalHandle of type 'MyBrokenSafeHandle'   
failed to properly release the handle with value 0x0000BEEF. This   
usually indicates that the handle was released incorrectly via   
another means (such as extracting the handle using DangerousGetHandle   
and closing it directly or building another SafeHandle around it."  
```  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <releaseHandleFailed/>  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 i seguito è riportato un esempio di codice che può attivare l'assistente al debug gestito `releaseHandleFailed`.  
  
```  
bool ReleaseHandle()  
{  
    // Calling the Win32 CloseHandle function to release the   
    // native handle wrapped by this SafeHandle. This method returns   
    // false on failure, but should only fail if the input is invalid   
    // (which should not happen here). The method specifically must not   
    // fail simply because of lack of resources or other transient   
    // failures beyond the user’s control. That would make it unacceptable   
    // to call CloseHandle as part of the implementation of this method.  
    return CloseHandle(handle);  
}  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)