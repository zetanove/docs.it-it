---
title: "Passaggi del processo di serializzazione | Microsoft Docs"
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
  - "serializzazione binaria, passaggi"
  - "serializzazione, passaggi"
ms.assetid: 4bcbc883-2a91-418f-b968-6c86a25e9737
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Passaggi del processo di serializzazione
Quando viene chiamato il metodo [Serialize](frlrfSystemRuntimeSerializationFormatterClassSerializeTopic) su un [formattatore](frlrfSystemRuntimeSerializationFormatterClassTopic), la serializzazione dell'oggetto continua secondo la sequenza di regole riportata di seguito:  
  
-   Viene effettuato un controllo per determinare se il formattatore dispone di un selettore di surrogati.In caso affermativo, controllare se il selettore di surrogati gestisce oggetti del tipo specificato.Se il selettore gestisce il tipo di oggetto, viene chiamato **ISerializable.GetObjectData** sul selettore di surrogati.  
  
-   Se non è presente alcun selettore di surrogati o il tipo di oggetto non viene gestito, viene effettuato un controllo per determinare se l'oggetto è contrassegnato con l'attributo [Serializable](frlrfSystemSerializableAttributeClassTopic).Se ciò non si verifica, viene generata una [SerializationException](frlrfSystemRuntimeSerializationSerializationExceptionClassTopic).  
  
-   Se l'oggetto è contrassegnato in modo appropriato, controllare se l'oggetto implementa l'interfaccia [ISerializable](frlrfSystemRuntimeSerializationISerializableClassTopic).In caso affermativo, viene chiamato [GetObjectData](frlrfSystemRuntimeSerializationISerializableClassGetObjectDataTopic) sull'oggetto.  
  
-   Se l'oggetto non implementa **ISerializable**, vengono utilizzati i criteri di serializzazione predefiniti, che serializzano tutti i campi non contrassegnati come [NonSerialized](frlrfSystemNonSerializedAttributeClassTopic).  
  
## Vedere anche  
 [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md)   
 [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58)   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)