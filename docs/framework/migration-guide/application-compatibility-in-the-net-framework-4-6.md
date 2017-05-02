---
title: "Compatibilità delle applicazioni in .NET Framework 4.6 | Microsoft Docs"
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
- application compatibility, .NET Framework
- application compatibility. NET Framework 4.6
ms.assetid: 7a3fd352-a8ba-4f9a-8250-951f2c994248
caps.latest.revision: 7
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 32bbbf7cb9acd71f5b8e28b7b12aab706221fab9
ms.lasthandoff: 04/18/2017

---
# <a name="application-compatibility-in-the-net-framework-46"></a>Compatibilità delle applicazioni in .NET Framework 4.6
Questo argomento contiene collegamenti a informazioni sui problemi di compatibilità delle applicazioni tra .NET Framework 4.5.2 e 4.6. I problemi sono divisi in due categorie:  
  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6.md)  
 Le modifiche in fase di esecuzione influiscono su tutte le app in esecuzione in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e che usano una determinata funzionalità.  
  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)  
 Le modifiche di reindirizzamento influiscono sulle app ricompilate per .NET Framework 4.5, 4.5.1, 4.5.2 o 4.6. e che comprendono:  
  
-   Modifiche all'ambiente in fase di progettazione. Gli strumenti di compilazione, ad esempio, possono generare avvisi mentre in precedenza non lo facevano.  
  
-   Modifiche all'ambiente di runtime. Queste influiscono solo sulle app destinate specificamente a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. Le app destinate a versioni precedenti di .NET Framework si comportano come se venissero eseguite in tali versioni.  
  
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
 [Compatibilità delle applicazioni nella versione 4.5.2](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)
