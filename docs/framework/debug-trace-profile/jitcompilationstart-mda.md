---
title: "jitCompilationStart MDA | Microsoft Docs"
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
  - "JIT compilation"
  - "MDAs (managed debugging assistants), JIT compilation"
  - "JitCompilationStart MDA"
  - "managed debugging assistants (MDAs), JIT compilation"
ms.assetid: 5ffd2857-d0ba-4342-9824-9ffe04ec135d
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# jitCompilationStart MDA
L'assistente al debug gestito `jitCompilationStart` viene attivato quando il compilatore JIT \(Just\-In\-Time\) avvia la compilazione di una funzione.  
  
## Sintomi  
 Le dimensioni del working set aumentano per un programma già nel formato immagine nativo in quanto il file mscorjit.dll è caricato nel processo.  
  
## Causa  
 Non tutti gli assembly da cui dipende il programma sono stati generati nel formato nativo oppure la registrazione di quelli che lo sono stati non è corretta.  
  
## Risoluzione  
 L'attivazione di questo assistente consente di individuare la funzione compilata tramite JIT.  Verificare se l'assembly contenente la funzione viene generato nel formato nativo ed è registrato correttamente.  
  
## Effetto sul runtime  
 Questo assistente registra un messaggio prima che un metodo venga compilato tramite JIT. Pertanto, la sua attivazione non ha un impatto significativo sulle prestazioni.  Se un metodo è inline, l'assistente in questione non genera un messaggio specifico.  
  
## Output  
 Nell'esempio di codice riportato di seguito viene illustrato l'output di esempio.  Nel caso specifico, l'output indica che nell'assembly Test il metodo "m" sulla classe "ns2.CO" è stato compilato tramite JIT.  
  
```  
method name="Test!ns2.C0::m"  
```  
  
## Configurazione  
 Nel file di configurazione riportato di seguito vengono illustrati i diversi filtri che è possibile utilizzare per escludere dal rapporto i metodi alla relativa prima compilazione tramite JIT.  Per specificare l'inserimento nel rapporto di tutti i metodi è possibile impostare il valore dell'attributo name su \*.  
  
```  
<mdaConfig>  
  <assistants>  
    <jitCompilationStart>  
      <methods>  
        <match name="C0::m" />  
        <match name="MyMethod" />  
        <match name="C2::*" />  
        <match name="ns0::*" />  
        <match name="ns1.C0::*" />  
        <match name="ns2.C0::m" />  
        <match name="ns2.C0+N0::m" />  
      </methods>  
    </jitCompilationStart >  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 L'esempio di codice riportato di seguito è destinato a essere utilizzato con il file di configurazione precedente.  
  
```  
using System;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
using System.Runtime.InteropServices;  
  
public class Entry  
{  
    public static void Main(string[] args)  
    {  
        C0.m();  
        C1.MyMethod();  
        C2.m();  
  
        ns0.C0.m();  
        ns0.C0.N0.m();  
        ns0.C1.m();  
  
        ns1.C0.m();  
        ns1.C0.N0.m();  
  
        ns2.C0.m();  
        ns2.C0.N0.m();  
    }  
}  
  
public class C0  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
public class C1  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void MyMethod() { }  
}  
  
public class C2  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
namespace ns0  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
  
    public class C1  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
    }  
}  
  
namespace ns1  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
  
namespace ns2  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)