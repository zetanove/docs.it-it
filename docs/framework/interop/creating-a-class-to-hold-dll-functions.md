---
title: "Creating a Class to Hold DLL Functions | Microsoft Docs"
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
  - "COM interop, DLL functions"
  - "unmanaged functions"
  - "COM interop, platform invoke"
  - "interoperation with unmanaged code, DLL functions"
  - "interoperation with unmanaged code, platform invoke"
  - "platform invoke, creating class for functions"
  - "DLL functions"
ms.assetid: e08e4c34-0223-45f7-aa55-a3d8dd979b0f
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Creating a Class to Hold DLL Functions
Il wrapping di una funzione di DLL frequentemente utilizzata in una classe gestita è un modo efficace per incapsulare la funzionalità della piattaforma.  Sebbene non sia obbligatorio farlo in tutti i casi, è preferibile fornire un wrapper di classe, perché la definizione delle funzioni di DLL è un'attività complessa e soggetta a errori.  In caso di programmazione in C\# o in Visual Basic, è necessario dichiarare le funzioni di DLL in una classe o in un modulo Visual Basic.  
  
 All'interno di una classe, si definisce un metodo statico per ciascuna funzione di DLL che si desidera chiamare.  La definizione può includere informazioni aggiuntive, come il set di caratteri o la convenzione di chiamata utilizzata per passare gli argomenti del metodo. Se si omettono queste informazioni, verranno utilizzate le impostazioni predefinite.  Per un elenco completo delle opzioni di dichiarazione e delle relative impostazioni predefinite, vedere [Creazione di prototipi nel codice gestito](../../../docs/framework/interop/creating-prototypes-in-managed-code.md).  
  
 Una volta effettuato il wrapping, sarà possibile chiamare i metodi della funzione così come si chiamano i metodi di qualsiasi altra funzione statica.  Con platform invoke, la funzione esportata sottostante viene gestita automaticamente.  
  
 Quando si progetta una classe gestita che supporti platform invoke, sarà necessario tenere in considerazione le relazioni tra le classi e le funzioni di DLL.  Ad esempio, è possibile:  
  
-   Dichiarare funzioni di DLL in una classe esistente.  
  
-   Creare una classe distinta per ciascuna funzione di DLL, mantenendo le funzioni isolate e facilmente rintracciabili.  
  
-   Creare una sola classe per un insieme di funzioni di DLL correlate, al fine di formare raggruppamenti logici e ridurre l'overhead.  
  
 È possibile assegnare alla classe e ai relativi metodi i nomi desiderati.  Per esempi della costruzione di dichiarazioni basate su .NET da utilizzare con platform invoke, vedere [Marshalling dei dati con platform invoke](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md).  
  
## Vedere anche  
 [Consuming Unmanaged DLL Functions](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)   
 [Identifying Functions in DLLs](../../../docs/framework/interop/identifying-functions-in-dlls.md)   
 [Creating Prototypes in Managed Code](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)   
 [Calling a DLL Function](../../../docs/framework/interop/calling-a-dll-function.md)