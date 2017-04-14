---
title: "Programmazione con i domini applicazione e gli assembly | Microsoft Docs"
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
  - "domini applicazione, programmazione"
  - "assembly [.NET Framework], programmazione"
  - "programmazione di domini applicazione"
  - "programmazione di assembly"
ms.assetid: 96d3b8e3-bef8-4da0-9a81-9841e23a94e9
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Programmazione con i domini applicazione e gli assembly
In host quali Microsoft Internet Explorer, ASP.NET e la shell di Windows, Common Language Runtime viene caricato in un processo, nel corso di tale processo viene creato un [dominio applicazione](../../../docs/framework/app-domains/application-domains.md), quindi il codice utente viene caricato ed eseguito in tale dominio applicazione durante l'esecuzione di un'applicazione .NET.  Nella maggior parte dei casi non è necessario occuparsi della creazione di domini applicazione e del caricamento di assembly, poiché tali attività vengono effettuate dall'host Common Language Runtime.  
  
 Se tuttavia si crea un'applicazione che fungerà da host per Common Language Runtime o si creano degli strumenti o del codice che si desidera scaricare a livello di codice oppure si creano componenti collegabili da scaricare e ricaricare in base alle necessità, la creazione dei domini applicazione verrà richiesta all'utente.  Anche se non si sta creando un host Common Language Runtime, in questa sezione vengono fornite importanti informazioni relative all'utilizzo dei domini applicazione e degli assembly caricati in tali domini applicazione.  
  
## In questa sezione  
 [Argomenti relativi alle procedure per domini applicazione e assembly](../../../docs/framework/app-domains/application-domains-and-assemblies-how-to-topics.md)  
 Vengono forniti collegamenti agli argomenti sulle procedure contenuti nella documentazione sui concetti relativi alla programmazione con assembly e domini applicazione.  
  
 [Utilizzo dei domini applicazione](../../../docs/framework/app-domains/use.md)  
 Vengono forniti esempi relativi alla creazione, la configurazione e l'utilizzo dei domini applicazione.  
  
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)  
 Viene descritto come creare, firmare e impostare gli attributi degli assembly.  
  
## Sezioni correlate  
 [Creazione di assembly e metodi dinamici](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
 Viene descritto come creare assembly dinamici.  
  
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)  
 Viene fornita una panoramica sui concetti di base relativi agli assembly.  
  
 [Domini applicazione](../../../docs/framework/app-domains/application-domains.md)  
 Viene fornita una panoramica sui concetti di base relativi ai domini applicazione.  
  
 [Cenni preliminari su reflection](../../../docs/framework/reflection-and-codedom/reflection.md)  
 Viene descritto l'utilizzo della classe **Reflection** per ottenere informazioni su un assembly.