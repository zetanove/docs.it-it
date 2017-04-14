---
title: "Marshalling in base al valore | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "serializzazione binaria, marshalling in base al valore"
  - "oggetti marshalling in base al valore"
  - "serializzazione, marshalling in base al valore"
ms.assetid: ee91e8f0-92e0-4732-8015-d17dee154be1
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Marshalling in base al valore
Gli oggetti sono validi solo nel dominio dell'applicazione in cui sono stati creati.Qualsiasi tentativo di passare l'oggetto come parametro o restituirlo come risultato non avrà esito positivo, a meno che l'oggetto non derivi da [MarshalByRefObject](frlrfSystemMarshalByRefObjectClassTopic) o sia contrassegnato come [Serializable](frlrfSystemSerializableAttributeClassTopic).Se l'oggetto è contrassegnato come **Serializable**, l'oggetto sarà serializzato automaticamente, verrà trasportato da un dominio dell'applicazione all'altro e sarà successivamente deserializzato in modo da produrre una copia esatta dell'oggetto nel secondo dominio dell'applicazione.Tale processo viene generalmente denominato marshalling in base al valore.  
  
 Quando un oggetto deriva da **MarshalByRefObject**, viene passato un riferimento all'oggetto da uno dominio dell'applicazione a un altro e non l'oggetto stesso.È inoltre possibile contrassegnare un oggetto che deriva da **MarshalByRefObject** come **Serializable**.Se questo oggetto è utilizzato con .NET Remoting, il formattatore responsabile della serializzazione, preconfigurato con un selettore di surrogati \([SurrogateSelector](frlrfSystemRuntimeSerializationSurrogateSelectorClassTopic)\), prende il controllo del processo di serializzazione e sostituisce tutti gli oggetti derivati da [MarshalByRefObject](frlrfSystemMarshalByRefObjectClassTopic) con un proxy.Senza [SurrogateSelector](frlrfSystemRuntimeSerializationSurrogateSelectorClassTopic), invece, l'architettura della serializzazione segue le regole della serializzazione standard descritte nei [Passaggi del processo di serializzazione](../../../docs/framework/serialization/steps-in-the-serialization-process.md).  
  
## Vedere anche  
 [Concetti relativi alla serializzazione](../../../docs/framework/serialization/serialization-concepts.md)   
 [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58)   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)