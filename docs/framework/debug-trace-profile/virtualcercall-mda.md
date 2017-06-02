---
title: "virtualCERCall MDA | Microsoft Docs"
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
  - "virtualCERCall MDA"
  - "virtual CER calls"
  - "constrained execution regions"
  - "CER calls"
  - "managed debugging assistants (MDAs), CER calls"
ms.assetid: 1eb18c7a-f5e0-443f-80fb-67bfbb047da2
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# virtualCERCall MDA
L'assistente al debug gestito `virtualCERCall` viene attivato come avviso indicante che un sito di chiamata all'interno di un grafico di chiamata di un'area a esecuzione vincolata \(CER, Constrained Execution Region\) fa riferimento a una destinazione virtuale, ovvero una chiamata virtuale a un metodo virtuale non final o una chiamata mediante un'interfaccia.  Poiché Common Language Runtime \(CLR\) non è in grado di prevedere il metodo di destinazione di queste chiamate semplicemente dal linguaggio MSIL \(Microsoft Intermediate Language\) e dall'analisi dei metadati,  la struttura ad albero delle chiamate non può essere preparata insieme al grafico CER e le interruzioni dei thread nel sottoalbero non possono essere bloccate automaticamente.  Questo assistente al debug gestito segnala i casi in cui potrebbe essere necessario estendere un'area CER mediante chiamate esplicite al metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> una volta che le informazioni aggiuntive necessarie per calcolare la destinazione della chiamata sono note in fase di esecuzione.  
  
## Sintomi  
 CER che non vengono eseguite quando viene interrotto un thread o viene scaricato un dominio applicazione.  
  
## Causa  
 Una CER contiene una chiamata a un metodo virtuale che non può essere preparata automaticamente.  
  
## Risoluzione  
 Chiamare <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> per il metodo virtuale.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  
  
## Output  
  
```  
Method 'MethodWithCer', while executing within a constrained execution region, makes a call  
at IL offset 0x0024 to 'VirtualMethod', which is virtual and cannot be prepared automatically  
at compile time. The caller must ensure this method is prepared explicitly at  
runtime before entering the constrained execution region.  
method name="VirtualMethod"  
declaringType name="VirtualCERCall+MyClass"  
  declaringModule name="mda"  
    callsite name="MethodWithCer" offset="0x0024"  
```  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    < VirtualCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
  
```  
class MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    virtual void VirtualMethod()  
    {  
        ...  
    }  
}  
  
class MyDerivedClass : MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    override void VirtualMethod()  
    {  
        ...  
    }  
}  
  
void MethodWithCer(MyClass object)  
{  
    RuntimeHelpers.PrepareConstrainedRegions();  
    try  
    {  
        ...  
    }  
    finally  
    {  
        // Start of the CER.  
  
        // Cannot tell at analysis time whether object is a MyClass  
        // or a MyDerivedClass, so we do not know which version of   
        // VirtualMethod we are going to call.  
        object.VirtualMethod();  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)