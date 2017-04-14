---
title: "Utilizzo dei componenti serviti con la Global Assembly Cache | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], Global Assembly Cache"
  - "GAC (Global Assembly Cache), componenti serviti"
  - "Global Assembly Cache, componenti serviti"
  - "componenti serviti, Global Assembly Cache"
ms.assetid: 3423e5d9-234c-4571-8161-e35f6d130128
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Utilizzo dei componenti serviti con la Global Assembly Cache
È consigliabile inserire nella Global Assembly Cache i componenti serviti \(componenti COM\+ di codice gestito\).  In alcuni scenari, ma non in tutti, la gestione dei componenti serviti non inclusi nella Global Assembly Cache può essere compiuta da Common Language Runtime e dai servizi COM\+.  Questa problematica viene illustrata negli scenari seguenti:  
  
-   Per quanto riguarda i componenti serviti di un'applicazione COM\+ Server, è necessario che l'assembly contenente i componenti si trovi nella Global Assembly Cache, poiché Dllhost.exe non viene eseguito nella stessa directory in cui si trovano i componenti serviti.  
  
-   Per quanto riguarda i componenti serviti di un'applicazione COM\+ Library, Common Language Runtime e i servizi COM\+ sono in grado di risolvere i riferimenti all'assembly contenente i componenti effettuando una ricerca nella directory corrente.  In questo caso non è quindi necessario che l'assembly si trovi nella Global Assembly Cache.  
  
-   La situazione è diversa per i componenti serviti di un'applicazione ASP.NET.  Se si inserisce l'assembly contenente i componenti serviti nella directory bin in cui risiede il codice base dell'applicazione e si utilizza la registrazione su richiesta, verrà effettuata la copia con shadowing dell'assembly nella Download Cache, poiché ASP.NET si avvale delle funzionalità di shadowing di Common Language Runtime.  
  
## Vedere anche  
 [How to: Create a Serviced Component](http://msdn.microsoft.com/it-it/7ec0b488-e5fc-46f2-a48d-1278ea4e301d)   
 [Utilizzo di assembly e della Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)   
 [Assembly Cache Viewer \(Shfusion.dll\)](http://msdn.microsoft.com/it-it/0d9464cf-ddba-4ca9-bbec-f678fb58f380)