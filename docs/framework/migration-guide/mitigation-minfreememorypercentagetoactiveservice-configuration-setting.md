---
title: "Attenuazione: impostazione della configurazione minFreeMemoryPercentageToActiveService | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a7875f26-0da8-4afe-9846-7a21778f757b
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Attenuazione: impostazione della configurazione minFreeMemoryPercentageToActiveService
In [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] viene generata un'eccezione se la memoria disponibile sul server Web è inferiore alla percentuale specificata per l’impostazione di configurazione [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md).  In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] questa impostazione è stata ignorata.  
  
## Impatto  
 Nella maggior parte dei casi è utile l'impatto dell’osservazione dell’impostazione [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md): migliora la stabilità del sistema impedendo le eccezioni <xref:System.OutOfMemoryException> che possono verificarsi durante l'avvio di un servizio Windows Communication Foundation \(WCF\) in un sistema con memoria limitata.  
  
 Tuttavia, in alcuni casi, potrebbe non essere possibile l’avvio di un servizio che era stato avviato correttamente in precedenza.  In tal caso, viene visualizzato un messaggio di errore dettagliato:  
  
```Output  
  
Controllo dei gate di memoria non riuscito perché la memoria libera (nnnn byte) è inferiore al nn% della memoria totale.  Di conseguenza, il servizio non sarà disponibile per le richieste in ingresso.  Per risolvere questo problema, ridurre il carico sul computer o modificare il valore di minFreeMemoryPercentageToActivateService nell'elemento di configurazione serviceHostingEnvironment.    
```  
  
## Attenuazione  
 Per ripristinare il comportamento precedente dove  è stata ignorata l'impostazione [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md), modificare il file web.config come segue:  
  
```  
  
<serviceHostingEnvironment multipleSiteBindingsEnabled="true"   
                           minFreeMemoryPercentageToActivateService="0">  
   <serviceActivations>  
   ...  
   </serviceActivations>  
</serviceHostingEnvironment>  
  
```  
  
## Vedere anche  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-1.md)