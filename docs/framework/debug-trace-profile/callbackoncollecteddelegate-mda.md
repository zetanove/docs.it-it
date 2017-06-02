---
title: "callbackOnCollectedDelegate MDA | Microsoft Docs"
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
  - "MDAs (managed debugging assistants), garbage collection"
  - "managed debugging assistants (MDAs), callback on collected delegates"
  - "MDAs (managed debugging assistants), callback on collected delegates"
  - "callback on delegate after garbage collection"
  - "callbackOnCollectedDelegate MDA"
  - "managed debugging assistants (MDAs), garbage collection"
  - "call back collected delegates"
  - "garbage collection, run-time errors"
  - "delegates [.NET Framework], garbage collection"
ms.assetid: 398b0ce0-5cc9-4518-978d-b8263aa21e5b
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# callbackOnCollectedDelegate MDA
L'Assistente al debug gestito \(MDA\) `callbackOnCollectedDelegate` viene attivato se viene eseguito il marshalling di un delegato da un codice gestito a un codice non gestito, ad esempio un puntatore a funzione, e se viene inserito un callback in tale puntatore dopo che il delegato è stato sottoposto a Garbage Collection.  
  
## Sintomi  
 Le violazioni di accesso si verificano durante il tentativo di chiamare codice gestito mediante puntatori a funzione ottenuti da delegati gestiti.  Questi errori possono sembrare bug di Common Language Runtime \(CLR\), anche se non lo sono, perché la violazione di accesso si verifica nel codice CLR.  
  
 L'errore non è coerente. L’esito della chiamata sul puntatore a funzione è a volte positivo e a volte negativo.  L'errore può verificarsi solo in situazioni di carico eccessivo o in un numero casuale di tentativi.  
  
## Causa  
 Il delegato dal quale il puntatore a funzione è stato creato ed esposto al codice non gestito è stato sottoposto a Garbage Collection.  Quando il componente non gestito tenta una chiamata sul puntatore a funzione, viene generata una violazione di accesso.  
  
 L'errore viene visualizzato in modo casuale perché dipende da quando si verifica la Garbage Collection.  Se un delegato è idoneo per la raccolta, la Garbage Collection può verificarsi dopo il callback e la chiamata ha esito positivo.  In altri casi, le Garbage Collection vengono eseguite prima del callback, che genera una violazione di accesso e causa l’arresto del programma.  
  
 La probabilità di errore dipende dal tempo compreso tra il marshalling del delegato e il callback sul puntatore a funzione, nonché dalla frequenza delle Garbage Collection.  L'errore si verifica raramente se il tempo compreso tra il marshalling del delegato e il callback è breve.  Spesso accade quando il metodo non gestito che riceve il puntatore a funzione non lo salva per un utilizzo futuro ma esegue subito il callback sul puntatore a funzione per completare l'operazione prima della restituzione.  Analogamente, si verificano altre Garbage Collection quando un sistema è sottoposto a un carico eccessivo che rende più probabile che si verifichi una Garbage Collection prima del callback.  
  
## Risoluzione  
 Dopo il marshalling di un delegato come puntatore a funzione non gestito, il Garbage Collector non può più registrarne la durata.  È invece necessario che il codice mantenga un riferimento al delegato per la durata del puntatore a funzione non gestito.  Tuttavia, è necessario prima identificare quale delegato sia stato raccolto.  Quando l'MDA è attivato, fornisce il nome del tipo del delegato.  Usare questo nome per cercare il codice per pInvoke o per le firme COM che passano il delegato al codice non gestito.  Il delegato interessato viene passato attraverso uno di questi siti di chiamata.  È anche possibile abilitare l'MDA `gcUnmanagedToManaged` per imporre una Garbage Collection prima di ogni callback nel runtime.  Questa operazione rimuoverà le incertezze introdotte dalla Garbage Collection garantendone l'esecuzione sempre prima del callback.  Quando si è certi che il delegato sia stato raccolto, modificare il codice per mantenere un riferimento al delegato sul lato gestito per la durata del puntatore a funzione non gestito sottoposto a marshalling.  
  
## Effetto sull'ambiente di esecuzione  
 Quando viene eseguito il marshalling dei delegati come puntatori a funzione, il runtime alloca un thunk che effettua la transizione da non gestito a gestito.  Questo thunk è l'oggetto effettivamente chiamato dal codice non gestito prima di richiamare il delegato gestito.  Senza l'MDA `callbackOnCollectedDelegate` abilitato, il codice di marshalling non gestito viene eliminato quando il delegato viene raccolto.  Con l'MDA `callbackOnCollectedDelegate` abilitato, il codice di marshalling non gestito non viene eliminato immediatamente dopo aver raccolto il delegato.  Per impostazione predefinita le ultime 1.000 istanze vengono invece conservate e modificate per attivare l'MDA quando viene chiamato.  Il thunk viene infine eliminato dopo che vengono raccolti altri 1.001 delegati sottoposti a marshalling.  
  
## Output  
 L'MDA indica il nome del tipo del delegato raccolto prima di un tentativo di callback al relativo puntatore a funzione non gestito.  
  
## Configurazione  
 L'esempio seguente mostra le opzioni di configurazione dell’applicazione.  Imposta il numero di thunk mantenuto attivo dall'MDA su 1.500.  Il valore predefinito `listSize` è 1.000, il valore minimo è 50 e il valore massimo è 2.000.  
  
```  
<mdaConfig>  
  <assistants>  
    <callbackOnCollectedDelegate listSize="1500" />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 L'esempio seguente illustra una situazione in cui è possibile attivare questo MDA:  
  
```  
// Library.cpp : Defines the unmanaged entry point for the DLL application.  
#include "windows.h"  
#include "stdio.h"  
  
void (__stdcall *g_pfTarget)();  
  
void __stdcall Initialize(void __stdcall pfTarget())  
{  
    g_pfTarget = pfTarget;  
}  
  
void __stdcall Callback()  
{  
    g_pfTarget();  
}  
// ---------------------------------------------------  
// C# Client  
using System;  
using System.Runtime.InteropServices;  
  
public class Entry  
{  
    public delegate void DCallback();  
  
    public static void Main()  
    {  
        new Entry();  
        Initialize(Target);  
        GC.Collect();  
        GC.WaitForPendingFinalizers();  
        Callback();  
    }  
  
    public static void Target()  
    {          
    }  
  
    [DllImport("Library", CallingConvention = CallingConvention.StdCall)]  
    public static extern void Initialize(DCallback pfDelegate);  
  
    [DllImport ("Library", CallingConvention = CallingConvention.StdCall)]  
    public static extern void Callback();  
  
    ~Entry() { Console.Error.WriteLine("Entry Collected"); }  
}  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)   
 [gcUnmanagedToManaged](../../../docs/framework/debug-trace-profile/gcunmanagedtomanaged-mda.md)