---
title: "How to: Reference .NET Types from COM | Microsoft Docs"
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
  - "importing type library"
  - "COM interop, referencing .NET types"
  - "interoperation with unmanaged code, referencing .NET types"
  - "referencing .NET types"
  - "interoperation with unmanaged code, importing type library"
  - "type libraries"
  - "COM interop, importing type library"
ms.assetid: 54917f6f-cb18-4103-b622-856b55da93f3
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Reference .NET Types from COM
Dal punto di vista del codice di client e server, le differenze tra COM e .NET Framework sono in gran parte invisibili.  I client Microsoft Visual Basic possono visualizzare un oggetto .NET nel Visualizzatore oggetti, che espone i metodi e la sintassi, le proprietà e i campi dell'oggetto come per qualunque oggetto COM.  
  
 Per i client C\+\+, il processo di importazione di una libreria dei tipi è leggermente più complesso, sebbene si utilizzino gli stessi strumenti che consentono di esportare metadati in una libreria dei tipi COM.  Per fare riferimento a membri di oggetti .NET da un client C\+\+ non gestito, fare riferimento al file TLB \(prodotto con Tlbexp.exe\) con la direttiva **\#import**.  Quando si fa riferimento a una libreria dei tipi da C\+\+, è necessario specificare l'opzione **raw\_interfaces\_only** oppure importare le definizioni nella libreria di classi base Mscorlib.tlb.  
  
### Per importare una libreria  
  
-   Specificare l'opzione **raw\_interfaces\_only** nella direttiva **\#import**.  Ad esempio:  
  
    ```cpp  
    #import "..\LoanLib\LoanLib.tlb" raw_interfaces_only  
    ```  
  
     In alternativa  
  
-   Includere una direttiva \#import per Mscorlib.tlb.  Ad esempio:  
  
    ```cpp  
    #import "mscorlib.tlb"  
    #import "..\LoanLib\LoanLib.tlb"  
    ```  
  
## Vedere anche  
 [Exposing .NET Framework Components to COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [Registering Assemblies with COM](../../../docs/framework/interop/registering-assemblies-with-com.md)   
 [Calling a .NET Object](http://msdn.microsoft.com/it-it/40c9626c-aea6-4bad-b8f0-c1de462efd33)   
 [Deploying an Application for COM Access](http://msdn.microsoft.com/it-it/fb63564c-c1b9-4655-a094-a235625882ce)