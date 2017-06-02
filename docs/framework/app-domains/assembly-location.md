---
title: "Posizione dell&#39;assembly | Microsoft Docs"
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
  - "assembly [.NET Framework], posizione"
  - "individuazione di assembly"
ms.assetid: 9f1f41a7-2954-49d3-a2c0-62b6ef4d40ab
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Posizione dell&#39;assembly
La posizione di un assembly consente di stabilire se Common Language Runtime è in grado di individuarlo quando vi si fa riferimento e consente inoltre di stabilire se è possibile condividere l'assembly con altri assembly.  È possibile distribuire un assembly nelle seguenti posizioni:  
  
-   La directory o le sottodirectory dell'applicazione.  
  
     L'assembly viene solitamente distribuito in questa posizione.  Le sottodirectory della directory radice di un'applicazione possono essere basate sulla lingua o sulle impostazioni cultura.  Se nell'attributo relativo alle impostazioni cultura di un assembly sono contenute informazioni, è necessario inserire tale assembly in una sottodirectory della directory dell'applicazione a cui è assegnato il nome delle impostazioni cultura specificate.  
  
-   La Global Assembly Cache.  
  
     Si tratta di una cache di codice binario, installata a ogni installazione di Common Language Runtime.  Nella maggior parte dei casi, se si desidera condividere un assembly con più applicazioni, si consiglia di distribuire tale assembly nella Global Assembly Cache.  
  
-   Un server HTTP.  
  
     È necessario che un assembly distribuito su un server HTTP disponga di un nome sicuro. Si punta all'assembly dalla sezione relativa alla base di codice del file di configurazione dell'applicazione.  
  
## Vedere anche  
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)   
 [Global Assembly Cache](../../../docs/framework/app-domains/gac.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)