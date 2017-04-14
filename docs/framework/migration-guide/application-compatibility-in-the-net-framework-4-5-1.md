---
title: "Compatibilit&#224; delle applicazioni in .NET Framework 4.5.1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b07b729-e2bf-4925-8b83-9c9ee6c48612
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Compatibilit&#224; delle applicazioni in .NET Framework 4.5.1
In questo argomento vengono forniti i collegamenti alle informazioni sui problemi di compatibilità tra .NET Framework 4.5 e 4.5.1.  I problemi sono divisi in due categorie:  
  
 [Modifiche in fase di esecuzione](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-1.md)  
 Le modifiche in fase di esecuzione influiscono su tutte le app in esecuzione in [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] e che usano una determinata funzionalità.  
  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-5-1.md)  
 Le modifiche di reindirizzamento influiscono sulle app che vengono ricompilate per [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] e che comprendono:  
  
-   Modifiche all'ambiente in fase di progettazione.  Gli strumenti di compilazione, ad esempio, possono generare avvisi mentre in precedenza non lo facevano.  
  
-   Modifiche all'ambiente di runtime.  Queste influiscono solo sulle app destinate specificamente a [!INCLUDE[net_v451](../../../includes/net-v451-md.md)].  Le app destinate a versioni precedenti di .NET Framework si comportano come se venissero eseguite in tali versioni.  
  
 Negli argomenti che descrivono le modifiche in fase di esecuzione e quelle di reindirizzamento i singoli elementi sono stati classificati in base all'impatto previsto, come descritto di seguito:  
  
 Principale  
 Si tratta di una modifica significativa che influisce su un numero elevato di app o che richiede variazioni sostanziali del codice.  
  
 Secondario  
 Si tratta di una modifica che influisce su un numero ridotto di app o che richiede variazioni marginali del codice.  
  
 Caso limite  
 Si tratta di una modifica che influisce sulle app in scenari molto specifici e non comuni.  
  
 Trasparente  
 Si tratta di una modifica che non ha effetti evidenti sullo sviluppatore o sull'utente dell'app.  L'app non dovrebbe richiedere variazioni a causa di questa modifica.  
  
## Vedere anche  
 [Versioni e dipendenze](../../../docs/framework/migration-guide/versions-and-dependencies.md)   
 [Compatibilità delle applicazioni](../../../docs/framework/migration-guide/application-compatibility.md)   
 [Compatibilità delle applicazioni nella versione 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [Compatibilità delle applicazioni nella versione 4.5.2](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)