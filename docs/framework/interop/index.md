---
title: "Interoperating with Unmanaged Code | Microsoft Docs"
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
  - "unmanaged code, interoperation"
  - "managed code, interoperation with unmanaged code"
  - ".NET Framework, interoperation with unmanaged code"
  - "unmanaged code"
  - "interoperation with unmanaged code"
  - "interoperation with unmanaged code, about interoperation"
  - "components [.NET Framework], interoperation with unmanaged code"
ms.assetid: ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Interoperating with Unmanaged Code
.NET Framework favorisce l'interazione con componenti COM, servizi COM\+, librerie dei tipi esterne e numerosi servizi del sistema operativo.  I tipi di dati, le firme dei metodi e i meccanismi di gestione errori del modello a oggetti gestito differiscono da quelli del modello a oggetti non gestito.  Per semplificare l'interoperabilità tra i componenti .NET Framework e il codice non gestito e per facilitare la migrazione, in Common Language Runtime le differenze tra questi modelli a oggetti vengono nascoste sia ai client che ai server.  
  
 Il codice che viene eseguito sotto il controllo del runtime si definisce codice gestito.  Viceversa, il codice che non si avvale del runtime si definisce non gestito.  I componenti COM, le interfacce ActiveX e le funzioni dell'API Win32 costituiscono esempi di codice non gestito.  
  
## In questa sezione  
 [Interoperating with Unmanaged Code How\-to Topics](http://msdn.microsoft.com/it-it/ec21c6e1-e233-4cd9-95ae-b9b9cf807f9d)  
 Sono riportati i collegamenti a tutte le procedure, incluse nella documentazione sui concetti, relative all'interoperabilità con il codice non gestito.  
  
 [Esposizione di componenti COM a .NET Framework](../../../docs/framework/interop/exposing-com-components.md)  
 Viene descritto come utilizzare i componenti COM dalle applicazioni .NET Framework.  
  
 [Esposizione di componenti .NET Framework a COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)  
 Viene descritto come utilizzare i componenti .NET Framework dalle applicazioni COM.  
  
 [Utilizzo di funzioni di DLL non gestite](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)  
 Viene descritto come chiamare le funzioni di DLL non gestite mediante platform invoke.  
  
 [Considerazioni di progettazione per l'interoperabilità](http://msdn.microsoft.com/it-it/b59637f6-fe35-40d6-ae72-901e7a707689)  
 Vengono forniti suggerimenti per la scrittura di componenti COM integrati.  
  
 [Marshalling di interoperabilità](../../../docs/framework/interop/interop-marshaling.md)  
 Viene descritto il marshalling per l'interoperabilità COM e platform invoke.  
  
 [How to: Map HRESULTs and Exceptions](../../../docs/framework/interop/how-to-map-hresults-and-exceptions.md)  
 Vengono descritte le associazioni tra le eccezioni e gli HRESULT.  
  
 [Interoperating Using Generic Types](http://msdn.microsoft.com/it-it/26b88e03-085b-4b53-94ba-a5a9c709ce58)  
 Viene descritto il comportamento dei tipi generici quando utilizzati nell'interoperabilità COM.  
  
## Sezioni correlate  
 [Advanced COM Interoperability](http://msdn.microsoft.com/it-it/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 Sono riportati collegamenti per accedere a ulteriori informazioni sull'inclusione di componenti COM nell'applicazione .NET Framework.