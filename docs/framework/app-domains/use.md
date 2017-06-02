---
title: "Uso dei domini dell&#39;applicazione | Microsoft Docs"
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
  - "domini dell'applicazione, informazioni"
  - "Common Language Runtime, domini dell'applicazione"
  - "runtime, domini dell'applicazione"
ms.assetid: c6d99815-e022-4d2c-9420-1d7ab5b9d504
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Uso dei domini dell&#39;applicazione
I domini applicazione offrono un'unità di isolamento per Common Language Runtime  e vengono creati ed eseguiti all'interno di un processo.  I domini applicazione vengono solitamente creati da un host Common Language Runtime, ovvero un'applicazione responsabile del caricamento di Common Language Runtime in un processo e dell'esecuzione del codice utente all'interno di un dominio applicazione.  Grazie all'host Common Language Runtime vengono creati un processo e un dominio applicazione predefinito, al cui interno viene eseguito codice gestito.  Tra gli host Common Language Runtime sono inclusi ASP.NET, Microsoft Internet Explorer e la shell di Windows.  
  
 Per la maggior parte delle applicazioni non è richiesta alcuna creazione di domini applicazione da parte del programmatore. Tutti i domini applicazione necessari vengono creati dall'host Common Language Runtime.  È tuttavia possibile creare e configurare domini applicazione aggiuntivi se per l'applicazione è necessario isolare codice oppure utilizzare e scaricare DLL.  
  
## In questa sezione  
 [Procedura: Creare un dominio dell'applicazione](../../../docs/framework/app-domains/how-to-create-an-application-domain.md)  
 Viene descritto come creare a livello di codice un dominio applicazione.  
  
 [Procedura: Scaricare un dominio dell'applicazione](../../../docs/framework/app-domains/how-to-unload-an-application-domain.md)  
 Viene descritto come scaricare a livello di codice un dominio applicazione.  
  
 [Procedura: configurare un dominio applicazione](../../../docs/framework/app-domains/how-to-configure-an-application-domain.md)  
 Vengono fornite informazioni introduttive sulla configurazione di un dominio applicazione.  
  
 [Recupero di informazioni di installazione da un dominio applicazione](../../../docs/framework/app-domains/retrieve-setup-information.md)  
 Viene descritto come recuperare informazioni di installazione da un dominio applicazione.  
  
 [Procedura: caricare assembly in un dominio applicazione](../../../docs/framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)  
 Viene descritto come caricare un assembly in un dominio applicazione.  
  
 [Procedura: reperire informazioni su tipo e membro da un assembly](../../../docs/framework/app-domains/how-to-obtain-type-and-member-information-from-an-assembly.md)  
 Viene descritto come recuperare informazioni relative a un assembly.  
  
 [Creazione di copie replicate di assembly](../../../docs/framework/app-domains/shadow-copy-assemblies.md)  
 Viene descritto come utilizzare la funzionalità di copia replicata per aggiornare gli assembly mentre sono in uso e come configurare la funzionalità di copia replicata.  
  
 [Procedura: ricevere notifiche di eccezioni first\-chance](../../../docs/framework/app-domains/how-to-receive-first-chance-exception-notifications.md)  
 Viene illustrato come ricevere una notifica in cui si informa che è stata generata un'eccezione, prima che Common Language Runtime cominci a cercare gestori di eccezioni.  
  
 [Risoluzione caricamenti assembly](../../../docs/framework/app-domains/resolve-assembly-loads.md)  
 Vengono fornite indicazioni sull'utilizzo dell'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> per risolvere gli errori di caricamento dell'assembly.  
  
## Riferimenti  
 <xref:System.AppDomain>  
 Rappresenta un dominio applicazione.  Fornisce metodi per la creazione e il controllo di domini applicazione.  
  
## Sezioni correlate  
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)  
 Viene fornita una panoramica delle funzioni svolte dagli assembly.  
  
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)  
 Viene descritto come creare, firmare e impostare gli attributi degli assembly.  
  
 [Emitting Dynamic Methods and Assemblies](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
 Viene descritto come creare assembly dinamici.  
  
 [Domini applicazione](../../../docs/framework/app-domains/application-domains.md)  
 Viene fornita una panoramica sui concetti di base relativi ai domini applicazione.  
  
 [Cenni preliminari su reflection](../../../docs/framework/reflection-and-codedom/reflection.md)  
 Viene descritto l'utilizzo della classe **Reflection** per ottenere informazioni su un assembly.