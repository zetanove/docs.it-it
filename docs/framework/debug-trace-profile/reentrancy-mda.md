---
title: "reentrancy MDA | Microsoft Docs"
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
  - "unmanaged code, debugging"
  - "transitioning threads unmanaged to managed code"
  - "reentrancy MDA"
  - "reentrancy without an orderly transition"
  - "managed debugging assistants (MDAs), reentrancy"
  - "illegal reentrancy"
  - "MDAs (managed debugging assistants), reentrancy"
  - "threading [.NET Framework], managed debugging assistants"
  - "managed code, debugging"
  - "native debugging, MDAs"
ms.assetid: 7240c3f3-7df8-4b03-bbf1-17cdce142d45
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# reentrancy MDA
L'assistente al debug gestito `reentrancy` viene attivato quando si tenta di eseguire una transizione da codice nativo a codice gestito nei casi in cui un precedente passaggio da codice gestito a codice nativo non è stato eseguito mediante una transizione ordinata.  
  
## Sintomi  
 L'heap oggetti viene danneggiato o si verificano altri errori gravi durante il passaggio da codice nativo a codice gestito.  
  
 I thread che passano da codice nativo a codice gestito e viceversa devono eseguire una transizione ordinata.  Nel sistema operativo, tuttavia, esistono alcuni punti di estendibilità di basso livello, ad esempio il gestore delle eccezioni basato su vettori, che consentono il passaggio da codice gestito a codice nativo senza eseguire una transizione ordinata.  Questi passaggi sono controllati dal sistema operativo anziché da Common Language Runtime.  Qualsiasi codice nativo eseguito all'interno di questi punti di estendibilità deve evitare di richiamare codice gestito.  
  
## Causa  
 Durante l'esecuzione di codice gestito è stato attivato un punto di estendibilità di basso livello del sistema operativo, ad esempio il gestore delle eccezioni basato su vettori.  Il codice dell'applicazione che viene richiamato tramite questo punto di estendibilità sta tentando di richiamare codice gestito.  
  
 Questo problema è sempre causato dal codice dell'applicazione.  
  
## Risoluzione  
 Esaminare la traccia dello stack per individuare il thread che ha attivato questo assistente al debug gestito.  Il thread sta tentando di eseguire una chiamata non valida nel codice gestito.  La traccia dello stack dovrebbe indicare il codice dell'applicazione che utilizza questo punto di estendibilità, il codice del sistema operativo che fornisce il punto di estendibilità e il codice gestito che è stato interrotto dal punto di estendibilità.  
  
 L'assistente al debug gestito verrà attivato, ad esempio, se si tenta di chiamare codice gestito dall'interno di un gestore delle eccezioni basato su vettori.  Nello stack sarà indicato il codice di gestione delle eccezioni del sistema operativo e il codice gestito che sta generando un'eccezione quale <xref:System.DivideByZeroException> o <xref:System.AccessViolationException>.  
  
 In questo esempio la soluzione corretta consiste nell'implementare il gestore delle eccezioni basato su vettori completamente nel codice non gestito.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  
  
## Output  
 L'assistente al debug gestito indica un tentativo di rientranza non valido.  Esaminare lo stack del thread per determinare la causa del problema e una possibile soluzione.  Di seguito è riportato un output di esempio.  
  
```  
Additional Information: Attempting to call into managed code without   
transitioning out first.  Do not attempt to run managed code inside   
low-level native extensibility points. Managed Debugging Assistant   
'Reentrancy' has detected a problem in 'D:\ConsoleApplication1\  
ConsoleApplication1\bin\Debug\ConsoleApplication1.vshost.exe'.  
```  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <reentrancy />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 L'esempio di codice riportato di seguito causa la generazione di un'eccezione <xref:System.AccessViolationException>.  Nelle versioni di Windows che supportano la gestione delle eccezioni basata su vettori questa eccezione determina la chiamata del gestore delle eccezioni basato su vettori.  Se abilitato, l'assistente al debug gestito `reentrancy` verrà attivato durante il tentativo di chiamata a `MyHandler` dal codice di supporto della gestione delle eccezioni basata su vettori del sistema operativo.  
  
```  
using System;  
public delegate int ExceptionHandler(IntPtr ptrExceptionInfo);  
  
public class Reenter   
{  
    public static ExceptionHandler keepAlive;  
  
    [System.Runtime.InteropServices.DllImport("kernel32", ExactSpelling=true,   
        CharSet=System.Runtime.InteropServices.CharSet.Auto)]  
    public static extern IntPtr AddVectoredExceptionHandler(int bFirst,   
        ExceptionHandler handler);  
  
    static int MyHandler(IntPtr ptrExceptionInfo)   
    {  
        // EXCEPTION_CONTINUE_SEARCH  
        return 0;  
    }  
    void Run() {}  
  
    static void Main()   
    {  
        keepAlive = new ExceptionHandler(Reenter.MyHandler);  
        IntPtr ret = AddVectoredExceptionHandler(1, keepAlive);  
        try   
        {  
            // Dispatch on null should AV.  
            Reenter r = null;   
            r.Run();  
        }   
        catch { }  
    }  
}  
```  
  
## Vedere anche  
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)