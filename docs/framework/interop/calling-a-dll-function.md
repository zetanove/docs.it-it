---
title: "Calling a DLL Function | Microsoft Docs"
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
  - "unmanaged functions, calling"
  - "unmanaged functions"
  - "COM interop, platform invoke"
  - "platform invoke, calling unmanaged functions"
  - "interoperation with unmanaged code, platform invoke"
  - "DLL functions"
ms.assetid: 113646de-7ea0-4f0e-8df0-c46dab3e8733
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Calling a DLL Function
Anche se le chiamate a funzioni di DLL non gestite sono quasi identiche alle chiamate ad altro codice gestito, esistono alcune differenze che possono rendere apparentemente poco chiaro l'utilizzo delle funzioni di DLL.  In questa sezione vengono presentati argomenti in cui sono descritti alcuni aspetti meno comuni delle chiamate.  
  
 Le strutture che vengono restituite dalle chiamate platform invoke devono essere tipi di dati contenenti la stessa rappresentazione in codice gestito e non gestito.  Tali tipi sono denominati *tipi non copiabili* perché non richiedono la conversione \(vedere [Blittable and Non\-Blittable Types](../../../docs/framework/interop/blittable-and-non-blittable-types.md)\).  Per chiamare una funzione con una struttura non copiabile come tipo restituito, è possibile definire un tipo di supporto copiabile della stessa dimensione del tipo non copiabile e convertire i dati dopo la restituzione della funzione.  
  
## In questa sezione  
 [Passaggio di strutture](../../../docs/framework/interop/passing-structures.md)  
 Vengono descritte le problematiche del passaggio di strutture di dati con un layout predefinito.  
  
 [Funzioni di callback](../../../docs/framework/interop/callback-functions.md)  
 Vengono fornite informazioni di base sulle funzioni di callback.  
  
 [Procedura: implementare funzioni di callback](../../../docs/framework/interop/how-to-implement-callback-functions.md)  
 Viene descritto come implementare funzioni di callback nel codice gestito.  
  
## Sezioni correlate  
 [Consuming Unmanaged DLL Functions](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)  
 Viene descritto come chiamare le funzioni di DLL non gestite mediante platform invoke.  
  
 [Marshaling Data with Platform Invoke](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)  
 Viene descritto come dichiarare i parametri dei metodi e passare gli argomenti alle funzioni esportate dalle librerie non gestite.