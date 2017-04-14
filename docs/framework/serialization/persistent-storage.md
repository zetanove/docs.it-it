---
title: "Archiviazione permanente | Microsoft Docs"
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
  - "serializzazione binaria, archiviazione permanente"
  - "archiviazione permanente"
  - "serializzazione, archiviazione permanente"
ms.assetid: b112c0dd-93e2-4eef-908d-5963f80bab65
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Archiviazione permanente
Spesso risulta necessario archiviare il valore dei campi di un oggetto su disco e in un secondo momento recuperare tali dati.Sebbene ciò sia facilmente realizzabile senza basarsi sulla serializzazione, questo approccio è spesso scomodo e tendente all'errore e diviene sempre più complesso quando è necessario registrare una gerarchia di oggetti.Si provi a immaginare di dovere scrivere un'applicazione aziendale di grandi dimensioni contenente migliaia di oggetti e di dovere scrivere codice per salvare e ripristinare i campi e le proprietà su e da disco per ogni oggetto.La serializzazione fornisce un comodo meccanismo per raggiungere tale obiettivo.  
  
 Il Common Language Runtime gestisce il modo in cui gli oggetti vengono archiviati in memoria e fornisce un meccanismo di serializzazione automatizzato tramite l'utilizzo della [reflection](../../../docs/framework/reflection-and-codedom/reflection.md).Quando un oggetto viene serializzato, il nome della classe, l'assembly e tutti i membri dati dell'istanza della classe vengono scritti nell'archiviazione.Gli oggetti spesso archiviano riferimenti ad altre istanze nelle variabili membro.Quando la classe viene serializzata, il motore di serializzazione registra oggetti a cui viene fatto riferimento, già serializzati, in modo da assicurare che lo stesso oggetto non venga serializzato più volte.L'architettura di serializzazione fornita con il [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] gestisce correttamente e automaticamente gli oggetti grafici e i riferimenti circolari.L'unico requisito a cui devono attenersi gli oggetti grafici è che tutti gli oggetti, a cui viene fatto riferimento dall'oggetto serializzato, devono essere anche contrassegnati come [Serializable](frlrfSystemSerializableAttributeClassTopic) \(per ulteriori informazioni, vedere [Serializzazione di base](../../../docs/framework/serialization/basic-serialization.md)\).Se ciò non viene fatto, viene generata un'eccezione nel momento in cui il serializzatore tenta di serializzare l'oggetto non contrassegnato.  
  
 Quando la classe serializzata viene deserializzata, la classe viene ricreata e i valori di tutti i membri dati vengono ripristinati automaticamente.  
  
## Vedere anche  
 [Concetti relativi alla serializzazione](../../../docs/framework/serialization/serialization-concepts.md)   
 [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58)   
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)