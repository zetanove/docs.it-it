---
title: Guida di migrazione a .NET Framework 4.6 e 4.5 | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- .NET Framework, migrating applications to
- migration, .NET Framework
ms.assetid: 02d55147-9b3a-4557-a45f-fa936fadae3b
caps.latest.revision: 56
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: 9004e102dac346e7d7d627f5adc573a18a53952e
ms.lasthandoff: 04/08/2017

---
# <a name="migration-guide-to-the-net-framework-46-and-45"></a>Guida di migrazione a .NET Framework 4.6 e 4.5 
Se un'app è stata creata usando una versione precedente di .NET Framework, in genere è possibile aggiornarla facilmente alla versione 4.5 e versioni intermedie (4.5.1 e 4.5.2), alla versione 4.6 e versioni intermedie (4.6.1 e 4.6.2) o alla versione 4.7. Aprire il progetto in Visual Studio. Se il progetto è stato creato in una versione precedente, verrà automaticamente aperta la finestra di dialogo **Project Compatibility** (Compatibilità progetto). Per altre informazioni sull'aggiornamento di un progetto in Visual Studio, vedere [Conversione, migrazione e aggiornamento dei progetti di Visual Studio](https://docs.microsoft.com/en-us/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects) e [Selezione della piattaforma e compatibilità di Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).  
  
 Tuttavia, alcune modifiche in .NET Framework richiedono modifiche al codice. È possibile che si voglia sfruttare le nuove funzionalità incluse in .NET Framework 4.5 e versioni intermedie, in .NET Framework 4.6 e versioni intermedie o in .NET Framework 4.7. L'introduzione di questo tipo di modifiche in un'app per una nuova versione di .NET Framework viene in genere definita *migrazione*. Se non è necessario eseguire la migrazione dell'app, è possibile eseguirla in .NET Framework 4.5 o versioni successive senza ricompilazione.  
  
## <a name="migration-resources"></a>Risorse di migrazione  
 Esaminare i documenti seguenti prima di eseguire la migrazione dell'app da versioni precedenti di .NET Framework alla versione 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2 o 4.7:  
  
-   Vedere [Versioni e dipendenze](../../../docs/framework/migration-guide/versions-and-dependencies.md) per conoscere la versione CLR sottostante a ogni versione di .NET Framework e rivedere le linee guida per specificare le app come destinazione.  
  
-   Consultare [Compatibilità delle applicazioni](../../../docs/framework/migration-guide/application-compatibility.md) per ottenere informazioni sul runtime e sulle modifiche di reindirizzamento che potrebbero interessare l'app e su come gestirle.  
  
-   Consultare [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md) per determinare i tipi o i membri del codice resi obsoleti e le alternative consigliate.  
  
-   Vedere [Novità](../../../docs/framework/whats-new/index.md) per le descrizioni di nuove funzionalità che possono essere aggiunte all'app.  
  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità delle applicazioni](../../../docs/framework/migration-guide/application-compatibility.md)   
 [Migrazione da .NET Framework 1.1](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)   
 [Compatibilità tra le versioni](../../../docs/framework/migration-guide/version-compatibility.md)   
 [Versioni e dipendenze](../../../docs/framework/migration-guide/versions-and-dependencies.md)   
 [Procedura: Configurare un'app per supportare .NET Framework 4 o 4.5](../../../docs/framework/migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)   
 [Novità](../../../docs/framework/whats-new/index.md)   
 [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md)   
 [.NET Framework Version and Assembly Information](http://go.microsoft.com/fwlink/?LinkId=201701)  (Versione di .NET Framework e informazioni assembly)  
 [Criteri relativi al ciclo di vita del supporto di Microsoft .NET Framework](http://go.microsoft.com/fwlink/?LinkId=196607)
