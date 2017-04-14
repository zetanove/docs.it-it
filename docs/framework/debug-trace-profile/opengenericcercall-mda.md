---
title: "openGenericCERCall MDA | Microsoft Docs"
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
  - "MDAs (managed debugging assistants), CER calls"
  - "open generic CER calls"
  - "constrained execution regions"
  - "openGenericCERCall MDA"
  - "CER calls"
  - "managed debugging assistants (MDAs), CER calls"
  - "generics [.NET Framework], open generic CER calls"
ms.assetid: da3e4ff3-2e67-4668-9720-fa776c97407e
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# openGenericCERCall MDA
L'assistente al debug gestito `openGenericCERCall` viene attivato per avvisare che il grafico di un'area a esecuzione vincolata \(CER, Constrained Execution Region\) con variabili di tipo generico nel metodo radice è in corso di elaborazione durante la compilazione JIT o la generazione dell'immagine nativa e che almeno una delle variabili di tipo generico è un tipo di riferimento a un oggetto.  
  
## Sintomi  
 Codice CER che non viene eseguito quando viene interrotto un thread o viene scaricato un dominio applicazione.  
  
## Causa  
 Durante la compilazione JIT, la creazione di un'istanza contenente un tipo di riferimento a un oggetto è solo rappresentativa poiché il codice risultante è condiviso e ognuna delle variabili potrebbe essere di qualsiasi tipo di riferimento a oggetto.  Ciò potrebbe impedire la preparazione anticipata di alcune risorse di runtime.  
  
 In particolare, i metodi con variabili di tipo generico possono allocare lentamente risorse in background.  Queste risorse sono dette voci di dizionario generiche.  Ad esempio, per l'istruzione `List<T> list = new List<T>();` \(dove `T` è una variabile di tipo generico\), il runtime deve cercare e possibilmente creare un'istanza esatta in fase di esecuzione, ad esempio, `List<Object>, List<String>`, `` e così via.  Questa operazione può avere esito negativo per una serie di motivi non soggetti al controllo dello sviluppatore, ad esempio l'esaurimento della memoria.  
  
 Questo assistente al debug gestito deve essere attivato soltanto al momento della compilazione JIT e non quando è presente un'istanza esatta.  
  
 Quando viene attivato, i sintomi più probabili sono che le CER non sono funzionali per la creazione di istanze non valide.  Common Language Runtime, infatti, non ha tentato di implementare una CER nelle circostanze che hanno causato l'attivazione dell'assistente al debug gestito.  Di conseguenza, se lo sviluppatore utilizza un'istanza condivisa della CER, gli errori di compilazione JIT, gli errori di caricamento di tipi generici o le interruzioni dei thread all'interno della CER non verranno intercettati.  
  
## Risoluzione  
 Non utilizzare variabili di tipo generico che sono di tipo di riferimento a oggetto per i metodi che possono contenere una CER.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  
  
## Output  
 Di seguito è riportato un esempio di output generato da questo assistente al debug gestito.  
  
 `Method 'GenericMethodWithCer', which contains at least one constrained execution region, cannot be prepared automatically since it has one or more unbound generic type parameters.`  
  
 `The caller must ensure this method is prepared explicitly at run time prior to execution.`  
  
 `method name="GenericMethodWithCer"`  
  
 `declaringType name="OpenGenericCERCall"`  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <openGenericCERCall/>  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 Il codice CER non viene eseguito.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Runtime.CompilerServices;  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        CallGenericMethods();  
    }  
    static void CallGenericMethods()  
    {  
        // This call is correct. The instantiation of the method  
        // contains only nonreference types.  
        MyClass.GenericMethodWithCer<int>();  
  
        // This call is incorrect. A shared version of the method that  
        // cannot be completely analyzed will be JIT-compiled. The   
        // MDA will be activated at JIT-compile time, not at run time.  
        MyClass.GenericMethodWithCer<String>();  
    }  
}  
  
    class MyClass  
{  
    public static void GenericMethodWithCer<T>()  
    {  
        RuntimeHelpers.PrepareConstrainedRegions();  
        try  
        {  
  
        }  
        finally  
        {  
            // This is the start of the CER.  
            Console.WriteLine("In finally block.");  
        }  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>   
 <xref:System.Runtime.ConstrainedExecution>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)