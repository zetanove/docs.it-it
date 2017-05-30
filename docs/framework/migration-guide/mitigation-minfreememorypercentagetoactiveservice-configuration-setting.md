---
title: 'Mitigazione: impostazione della configurazione minFreeMemoryPercentageToActiveService | Microsoft Docs'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7875f26-0da8-4afe-9846-7a21778f757b
caps.latest.revision: 4
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 783dd4fb28f1590722833ce9a456b9c2c76ecd80
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-minfreememorypercentagetoactiveservice-configuration-setting"></a>Mitigazione: impostazione della configurazione minFreeMemoryPercentageToActiveService
In [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] viene generata un'eccezione se la memoria disponibile sul server Web è inferiore alla percentuale specificata per l'impostazione di configurazione [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md). In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] questa impostazione è stata ignorata.  
  
## <a name="impact"></a>Impatto  
 Nella maggior parte dei casi è utile l'impatto dell'osservazione dell'impostazione [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md): migliora la stabilità del sistema impedendo le eccezioni <xref:System.OutOfMemoryException> che possono verificarsi durante l'avvio di un servizio Windows Communication Foundation (WCF) in un sistema con memoria limitata.  
  
 Tuttavia, in alcuni casi, potrebbe non essere possibile l’avvio di un servizio che era stato avviato correttamente in precedenza. In tal caso, viene visualizzato un messaggio di errore dettagliato:  
  
```console
Memory gates checking failed because the free memory (nnnn bytes) is less than nn% of total memory. As a result, the service will not be available for incoming requests. To resolve this, either reduce the load on the machine or adjust the value of minFreeMemoryPercentageToActivateService on the serviceHostingEnvironment config element.
```
  
## <a name="mitigation"></a>Attenuazione  
 Per ripristinare il comportamento precedente dove è stata ignorata l'impostazione [minFreeMemoryPercentageToActivateService](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md), modificare il file web.config come segue:  
  
```xml
<serviceHostingEnvironment multipleSiteBindingsEnabled="true"   
                           minFreeMemoryPercentageToActivateService="0">  
   <serviceActivations>  
   ...  
   </serviceActivations>  
</serviceHostingEnvironment>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-1.md)

