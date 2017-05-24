---
title: "Compatibilità delle applicazioni in .NET Framework 4.5.2 | Microsoft Docs"
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
- application compatibility
- .NET Framework 4.5.2
- application compatibility,.NET Framework
- application compatibility,.NET Framework 4.5.2
ms.assetid: 4c6a029d-c565-4f25-b87b-b2361634bd74
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 2631cb6c9464954b18cf97e21b8f48b30458c0db
ms.lasthandoff: 04/18/2017

---
# <a name="application-compatibility-in-the-net-framework-452"></a>Compatibilità delle applicazioni in .NET Framework 4.5.2
In questo argomento vengono forniti i collegamenti alle informazioni sui problemi di compatibilità tra .NET Framework 4.5.1 e 4.5.2. I problemi sono divisi in due categorie:  
  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-2.md)  
 Le modifiche in fase di esecuzione influiscono su tutte le app in esecuzione in .NET Framework 4.5.2 e che usano una determinata funzionalità.  
  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-5-2.md)  
 Le modifiche di reindirizzamento influiscono sulle app che vengono ricompilate per .NET Framework 4.5, 4.5.1 o 4.5.2 e che comprendono:  
  
-   Modifiche all'ambiente in fase di progettazione. Gli strumenti di compilazione, ad esempio, possono generare avvisi mentre in precedenza non lo facevano.  
  
-   Modifiche all'ambiente di runtime. Queste influiscono solo sulle app destinate specificamente a .NET Framework 4.5.2. Le app destinate a versioni precedenti di .NET Framework si comportano come se venissero eseguite in tali versioni.  
  
 Negli argomenti che descrivono le modifiche in fase di esecuzione e quelle di reindirizzamento i singoli elementi sono stati classificati in base all'impatto previsto, come descritto di seguito:  
  
 Principale  
 Si tratta di una modifica significativa che influisce su un numero elevato di app o che richiede variazioni sostanziali del codice.  
  
 Secondario  
 Si tratta di una modifica che influisce su un numero ridotto di app o che richiede variazioni marginali del codice.  
  
 Caso limite  
 Si tratta di una modifica che influisce sulle app in scenari molto specifici e non comuni.  
  
 Trasparente  
 Si tratta di una modifica che non ha effetti evidenti sullo sviluppatore o sull'utente dell'app. L'app non dovrebbe richiedere variazioni a causa di questa modifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Versioni e dipendenze](../../../docs/framework/migration-guide/versions-and-dependencies.md)   
 [Compatibilità delle applicazioni](../../../docs/framework/migration-guide/application-compatibility.md)   
 [Compatibilità delle applicazioni nella versione 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [Compatibilità delle applicazioni nella versione 4.5.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-1.md)
