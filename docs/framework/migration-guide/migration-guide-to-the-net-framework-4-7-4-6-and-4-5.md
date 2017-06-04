---
title: "Guida di migrazione a .NET Framework 4.6 e 4.5  | Microsoft Docs"
ms.custom: ""
ms.date: "02/09/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework, migrazione di applicazioni"
  - "migrazione, .NET Framework"
ms.assetid: 02d55147-9b3a-4557-a45f-fa936fadae3b
caps.latest.revision: 56
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
---
# Guida di migrazione a .NET Framework 4.6 e 4.5 
Se un'app è stata creata usando una versione precedente di .NET Framework, in genere è possibile aggiornarla facilmente alla versione 4.5, 4.5.1 o 4.6. Aprire il progetto in Visual Studio. Se il progetto è stato creato in una versione precedente, verrà automaticamente aperta la finestra di dialogo **Compatibilità del progetto**. Per altre informazioni sull'aggiornamento di un progetto in Visual Studio 2013, vedere [Procedura: Aggiornare i progetti creati in versioni precedenti di Visual Studio](http://msdn.microsoft.com/library/vstudio/ms185327\(v=vs.100\).aspx) e [Portabilità, migrazione e aggiornamento dei progetti di Visual Studio](../Topic/Porting,%20Migrating,%20and%20Upgrading%20Visual%20Studio%20Projects.md).  
  
 Tuttavia, alcune modifiche in .NET Framework richiedono modifiche al codice. È possibile che si voglia sfruttare la nuova funzionalità inclusa in .NET Framework 4.5, nelle versioni principali o in .NET Framework 4.6. L'esecuzione di questi tipi di modifiche all'app per una nuova versione di .NET Framework viene in genere definita *migrazione*. Se non è necessario eseguire la migrazione dell'app, è possibile eseguirla in .NET Framework 4.5 o versioni successive senza ricompilazione.  
  
## Risorse di migrazione  
 Esaminare i documenti seguenti prima di eseguire la migrazione dell'app da versioni precedenti di .NET Framework alla versione 4.5, 4.5.1 o 4.5.2:  
  
-   Vedere [Versioni e dipendenze](../../../docs/framework/migration-guide/versions-and-dependencies.md) per conoscere la versione CLR sottostante a ogni versione di .NET Framework e rivedere le linee guida per specificare le app come destinazione.  
  
-   Rivedere [Compatibilità delle applicazioni](../../../docs/framework/migration-guide/application-compatibility.md) per ottenere informazioni sul runtime e sulle modifiche di reindirizzamento che potrebbero interessare l'app e la modalità di gestione.  
  
-   Rivedere [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md) per determinare i tipi o i membri nel codice reso obsoleto e le alternative consigliate.  
  
-   Vedere [Novità](../../../docs/framework/whats-new/index.md) per le descrizioni di nuove funzionalità che potrebbero essere aggiunte all'app.  
  
## Vedere anche  
 [Compatibilità delle applicazioni nella versione 4.5.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-1.md)   
 [Compatibilità delle applicazioni nella versione 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [Migrazione da .NET Framework 1.1](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)   
 [Compatibilità tra versioni](../../../docs/framework/migration-guide/version-compatibility.md)   
 [Versioni e dipendenze](../../../docs/framework/migration-guide/versions-and-dependencies.md)   
 [Procedura: configurare un'applicazione per supportare .NET Framework 4 o 4.5](../../../docs/framework/migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)   
 [Novità](../../../docs/framework/whats-new/index.md)   
 [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md)   
 [Versione di .NET Framework e informazioni assembly](http://go.microsoft.com/fwlink/?LinkId=201701)   
 [Criteri relativi al ciclo di vita del supporto Microsoft .NET Framework](http://go.microsoft.com/fwlink/?LinkId=196607)