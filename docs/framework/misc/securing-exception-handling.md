---
title: "Securing Exception Handling | Microsoft Docs"
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
  - "code security, exception handling"
  - "security [.NET Framework], exception handling"
  - "secure coding, exception handling"
  - "exception handling, security"
ms.assetid: 1f3da743-9742-47ff-96e6-d0dd1e9e1c19
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# Securing Exception Handling
In Visual C\+\+ e Visual Basic un'espressione di filtro di un livello superiore dello stack viene eseguita prima dell'istruzione **finally**.  Il blocco **catch** associato a tale filtro viene eseguito dopo l'istruzione **finally**.  Per ulteriori informazioni, vedere [Utilizzo di eccezioni filtrate dall'utente](../../../docs/standard/exceptions/using-user-filtered-exception-handlers.md).  In questa sezione sono esaminate le implicazioni che questo ordine di istruzioni può avere sulla sicurezza.  Nell'esempio di pseudo\-codice riportato di seguito è illustrato l'ordine di esecuzione delle istruzioni di filtro e delle istruzioni **finally**.  
  
```cpp  
void Main()   
{  
    try   
    {  
        Sub();  
    }   
    except (Filter())   
    {  
        Console.WriteLine("catch");  
    }  
}  
bool Filter () {  
    Console.WriteLine("filter");  
    return true;  
}  
void Sub()   
{  
    try   
    {  
        Console.WriteLine("throw");  
        throw new Exception();  
    }   
    finally   
    {  
        Console.WriteLine("finally");  
    }  
}                        
```  
  
 Il codice viene visualizzato nel seguente modo:  
  
```  
Throw  
Filter  
Finally  
Catch  
```  
  
 Il filtro viene eseguito prima dell'istruzione **finally**; problemi di sicurezza possono essere provocati da elementi che determinino un cambiamento di stato che può essere sfruttato tramite l'esecuzione di altro codice.  Di seguito è riportato un esempio:  
  
```cpp  
try   
{  
    Alter_Security_State();  
    // This means changing anything (state variables,  
    // switching unmanaged context, impersonation, and   
    // so on) that could be exploited if malicious   
    // code ran before state is restored.  
    Do_some_work();  
}   
finally   
{  
    Restore_Security_State();  
    // This simply restores the state change above.  
}  
```  
  
 Questo pseudo\-codice consente l'esecuzione di codice arbitrario da parte di un filtro nella parte alta dello stack.  Altri esempi di operazioni che possono avere un effetto simile sono la rappresentazione temporanea di un'altra identità, l'impostazione di un flag interno che consente di ignorare un controllo di sicurezza o la modifica delle impostazioni cultura associate al thread.  Si consiglia di introdurre un gestore di eccezioni per isolare le modifiche dello stato del thread da parte del codice dai blocchi dei filtri del chiamante.  È tuttavia importante che il gestore eccezioni sia introdotto in modo adeguato; in caso contrario, non sarà possibile risolvere il problema.  Nell'esempio riportato di seguito vengono modificate le impostazioni cultura dell'interfaccia utente, ma è possibile esporre in modo simile qualsiasi tipo di cambiamento di stato del thread.  
  
```cpp  
YourObject.YourMethod()  
{  
   CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
   try {  
      Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
      // Do something that throws an exception.  
}  
   finally {  
      Thread.CurrentThread.CurrentUICulture = saveCulture;  
   }  
}  
  
```  
  
```vb  
Public Class UserCode  
   Public Shared Sub Main()  
      Try  
         Dim obj As YourObject = new YourObject  
         obj.YourMethod()  
      Catch e As Exception When FilterFunc  
         Console.WriteLine("An error occurred: '{0}'", e)  
         Console.WriteLine("Current Culture: {0}",   
Thread.CurrentThread.CurrentUICulture)  
      End Try  
   End Sub  
  
   Public Function FilterFunc As Boolean  
      Console.WriteLine("Current Culture: {0}", Thread.CurrentThread.CurrentUICulture)  
      Return True  
   End Sub  
  
End Class  
```  
  
 La soluzione corretta in questo caso consiste nell'eseguire il wrapping di un blocco **try**\/**finally** presente in un blocco **try**\/**catch**.  La semplice introduzione di una clausola **catch\-throw** nel blocco **try**\/**finally** non comporta la correzione del problema, come mostrato nell'esempio riportato di seguito.  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
  
    try   
    {  
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
        // Do something that throws an exception.  
    }  
    catch { throw; }  
    finally   
    {  
        Thread.CurrentThread.CurrentUICulture = saveCulture;  
    }  
}  
```  
  
 Il problema non viene risolto in quanto l'istruzione **finally** non viene eseguita prima che `FilterFunc` ottenga il controllo.  
  
 Nell'esempio riportato di seguito il problema viene risolto facendo in modo che la clausola **finally** sia eseguita prima della generazione di un'eccezione nei blocchi dei filtri delle eccezioni del chiamante.  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
    try    
    {  
        try   
        {  
            Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
            // Do something that throws an exception.  
        }  
        finally   
        {  
            Thread.CurrentThread.CurrentUICulture = saveCulture;  
        }  
    }  
    catch { throw; }  
}  
```  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)