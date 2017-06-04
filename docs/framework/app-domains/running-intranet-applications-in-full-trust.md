---
title: "Esecuzione di applicazioni Intranet in attendibilit&#224; totale | Microsoft Docs"
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
  - "attendibilità totale, esecuzione di applicazioni Intranet in"
  - "applicazioni Intranet, esecuzione in attendibilità totale"
  - "esecuzione di applicazioni Intranet in attendibilità totale"
ms.assetid: ee13c0a8-ab02-49f7-b8fb-9eab16c6c4f0
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Esecuzione di applicazioni Intranet in attendibilit&#224; totale
A partire da .NET Framework versione 3.5 Service Pack 1 \(SP1\) le applicazioni e gli assembly di librerie possono essere eseguiti come assembly con attendibilità totale da una condivisione di rete.  Agli assembly caricati da una condivisione nella rete Intranet viene automaticamente aggiunta l'evidenza di zona <xref:System.Security.SecurityZone>.  Questa evidenza fornisce a tali assembly la stessa concessione \(che è in genere di attendibilità totale\) degli assembly che risiedono nel computer.  Questa funzionalità non si applica alle applicazioni ClickOnce o alle applicazioni progettate per essere eseguite in un host.  
  
## Regole per gli assembly di librerie  
 Le regole seguenti si applicano agli assembly caricati da un file eseguibile su una condivisione di rete:  
  
-   Gli assembly di librerie devono risiedere nella stessa cartella dell'assembly eseguibile.  Agli assembly che si trovano in una sottocartella o a cui viene fatto riferimento in un percorso diverso non viene concessa l'attendibilità totale.  
  
-   Se l'eseguibile effettua il caricamento ritardato di un assembly, deve utilizzare lo stesso percorso impiegato per avviare l'eseguibile.  Se ad esempio \\\\*network\-computer*\\*share* è mappata a una lettera di unità e l'eseguibile viene eseguito da tale percorso, agli assembly caricati dall'eseguibile tramite il percorso di rete non verrà concessa attendibilità totale.  Per eseguire il caricamento ritardato di un assembly nella zona <xref:System.Security.SecurityZone>, l'eseguibile deve utilizzare il percorso della lettera dell'unità.  
  
## Ripristino dei criteri Intranet precedenti  
 Nelle versioni precedenti di .NET Framework, agli assembly condivisi viene concessa l'evidenza della zona <xref:System.Security.SecurityZone>.  È necessario specificare criteri di sicurezza per l'accesso al codice per concedere attendibilità totale a un assembly in una condivisione.  
  
 Questo nuovo comportamento rappresenta l'impostazione predefinita per gli assembly su reti Intranet.  È possibile tornare al comportamento precedente, che consiste nel fornire l'evidenza <xref:System.Security.SecurityZone> impostando una chiave del Registro di sistema che si applica a tutte le applicazioni nel computer.  Questo processo è diverso per computer a 32 bit e a 64 bit:  
  
-   Nei computer a 32 bit creare una sottochiave della chiave HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\.NETFramework nel Registro di sistema.  Utilizzare il nome di chiave LegacyMyComputerZone con il valore di DWORD impostato su 1.  
  
-   Nei computer a 64 bit creare una sottochiave della chiave HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\.NETFramework nel Registro di sistema.  Utilizzare il nome di chiave LegacyMyComputerZone con il valore di DWORD impostato su 1.  Creare la stessa sottochiave nella chiave HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\.NETFramework.  
  
## Vedere anche  
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)