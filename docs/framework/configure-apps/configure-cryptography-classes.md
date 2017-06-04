---
title: "Configurazione di classi di crittografia | Microsoft Docs"
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
  - "configurazione di applicazioni .NET Framework, crittografia"
  - "file di configurazione [.NET Framework], crittografia"
  - "algoritmi di crittografia"
  - "crittografia, classi"
  - "crittografia predefinita"
  - "sicurezza [.NET Framework], crittografia"
ms.assetid: eee3ccb8-2c0d-4f35-b38d-6892a46c14e5
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Configurazione di classi di crittografia
[!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] consente agli amministratori di computer di configurare le implementazioni di algoritmi e gli algoritmi di crittografia predefiniti che vengono utilizzati da .NET Framework e da applicazioni scritte in modo appropriato.  Un'azienda che dispone di un'implementazione personalizzata di un algoritmo di crittografia può ad esempio utilizzare tale implementazione come predefinita in alternativa a quella fornita con [!INCLUDE[winsdkshort](../../../includes/winsdkshort-md.md)].  Anche se le applicazioni gestite che utilizzano la crittografia possono sempre essere associate in modo esplicito a una specifica implementazione, è consigliabile creare oggetti di crittografia utilizzando il sistema di configurazione della crittografia.  
  
## In questa sezione  
 [Mapping di nomi di algoritmi a classi di crittografia](../../../docs/framework/configure-apps/map-algorithm-names-to-cryptography-classes.md)  
 Viene descritto come mappare un nome di algoritmo a una classe di crittografia.  
  
 [Mapping di identificatori di oggetti ad algoritmi di crittografia](../../../docs/framework/configure-apps/map-object-identifiers-to-cryptography-algorithms.md)  
 Viene descritto come mappare un identificatore di oggetto a un algoritmo di crittografia.  
  
## Sezioni correlate  
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)  
 Viene fornita una panoramica dei servizi di crittografia forniti da [!INCLUDE[winsdkshort](../../../includes/winsdkshort-md.md)].  
  
 [Schema delle impostazioni di crittografia](../../../docs/framework/configure-apps/file-schema/cryptography/index.md)  
 Vengono descritti gli elementi che eseguono il mapping dei nomi descrittivi degli algoritmi alle classi che implementano gli algoritmi di crittografia.