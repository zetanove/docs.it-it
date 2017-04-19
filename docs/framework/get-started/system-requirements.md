---
title: Requisiti di sistema di .NET Framework | Microsoft Docs
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
- software requirements
- .NET Framework, system requirements
- system requirements
- operating systems supported
- hardware requirements
ms.assetid: 298275e2-da1d-4618-9f74-6a3567832350
caps.latest.revision: 95
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: b550e69dfdf0db47b22c89dee4bc3a98d2beac16
ms.lasthandoff: 04/18/2017

---
# <a name="net-framework-system-requirements"></a>Requisiti di sistema di .NET Framework
Le tabelle in questo argomento illustrano i requisiti hardware, software e del sistema operativo per .NET Framework 4.5 e le relative versioni intermedie (4.5.1 e 4.5.2), per [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e le relative versioni intermedie (4.6.1 e 4.6.2) e per .NET Framework 4.7. Gli ambienti di sviluppo che consentono di sviluppare applicazioni per .NET Framework dispongono di un set separato di requisiti.  
  
 Per informazioni sul download e i collegamenti, vedere [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md).  
  
 Per informazioni sul ciclo di vita del supporto delle versioni di .NET Framework, vedere [Ciclo di vita del supporto Microsoft](https://support.microsoft.com/en-us/lifecycle/search?sort=PN&alpha=Microsoft%20.NET%20Framework&Filter=FilterNO).  
  
## <a name="hardware-requirements"></a>Requisiti hardware  
  
|||  
|-|-|  
|**Processore**|1 GHz|  
|**RAM**|512 MB|  
|**Spazio su disco (minimo)**||  
|32 bit|4,5 GB|  
|64 bit|4,5 GB|  
  
## <a name="installation-requirements"></a>Requisiti di installazione  
  
-   Per poter installare .NET Framework, sono necessari privilegi di amministratore. Se non si dispone di diritti di amministratore nel computer in cui si vuole installare .NET Framework, contattare l'amministratore di rete.  
  
## <a name="supported-client-operating-systems"></a>Sistemi operativi client supportati  
  
|Sistema operativo|Edizioni supportate|Preinstallato con il sistema operativo|Installabile separatamente|  
|----------------------|------------------------|------------------------------|----------------------------|  
| Windows 10 Creators Update|32 e 64 bit|.NET Framework 4.7|| 
|Aggiornamento dell'anniversario di Windows 10|32 bit e 64 bit|[!INCLUDE[net_v462](../../../includes/net-v462-md.md)]||  
|Aggiornamento di novembre di Windows 10|32 bit e 64 bit|[!INCLUDE[net_v461](../../../includes/net-v461-md.md)]||  
|Windows 10|32 bit e 64 bit|[!INCLUDE[net_v46](../../../includes/net-v46-md.md)]|[!INCLUDE[net_v461](../../../includes/net-v461-md.md)]|  
|[!INCLUDE[win81](../../../includes/win81-md.md)]|32 bit, 64 bit e ARM|[!INCLUDE[net_v451](../../../includes/net-v451-md.md)]|[!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|  
|[!INCLUDE[win8](../../../includes/win8-md.md)]|32 bit, 64 bit e ARM|[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]|[!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]|  
|Windows 7 SP1|32 e 64 bit|--|.NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|  
|Windows Vista SP2|32 e 64 bit|--|.NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]|  
|Windows XP|32 e 64 bit|--|.NET Framework 4|  
  
 **Note:**  
  
- .NET Framework 4.7 è preinstallato in Windows 10 Creators Update. Non è disponibile per l'installazione in altri sistemi operativi Windows.

-   Nei sistemi Windows 7, .NET Framework richiede Windows 7 SP1. Se si dispone di Windows 7 ma non è ancora stato installato il Service Pack 1, è necessario farlo prima di installare .NET Framework.  
  
-   [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] è supportato nell'Ambiente preinstallazione di Windows (Windows PE). Non tutte le funzionalità sono supportate in Windows PE.  
  
-   .NET Framework 4 supporta inoltre la piattaforma IA64.  
  
-   Per tutte le piattaforme, si consiglia di eseguire l'aggiornamento al Service Pack di Windows più recente e di installare gli aggiornamenti critici disponibili nel [sito Web Windows Update](http://go.microsoft.com/fwlink/?LinkId=168461) per garantire la massima compatibilità e sicurezza.  
  
-   Nei sistemi operativi a 64 bit, .NET Framework supporta sia WOW64 (elaborazione a 32 bit su un computer a 64 bit) che l'elaborazione nativa a 64 bit.  
  
## <a name="supported-server-operating-systems"></a>Sistemi operativi server supportati  
  
|Sistema operativo|Edizioni supportate|Preinstallato con il sistema operativo|Installabile separatamente|  
|----------------------|------------------------|------------------------------|----------------------------|  
|Windows Server 2016|64 bit|[!INCLUDE[net_v462](../../../includes/net-v462-md.md)]||  
|[!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)]|64 bit|[!INCLUDE[net_v451](../../../includes/net-v451-md.md)]|[!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|  
|[!INCLUDE[winserver8](../../../includes/winserver8-md.md)] (edizione a 64 bit)|64 bit|[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]|[!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|  
|Windows Server 2008 R2 SP1|64 bit|--|.NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|  
|Windows Server 2008 SP2|32 e 64 bit|--|.NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]|  
  
 **Note:**  
  
-   In [!INCLUDE[winserver8](../../../includes/winserver8-md.md)] è incluso [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], pertanto non è necessario installarlo separatamente. Analogamente, in [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] è incluso [!INCLUDE[net_v451](../../../includes/net-v451-md.md)].  
  
-   .NET Framework è supportato nel ruolo Server Core con Windows Server 2008 R2 SP1 o versioni successive, ma non è supportato in Windows Server 2008 R2 per sistemi basati su Itanium.  
  
-   .NET Framework non è supportato nel ruolo Server Core di Windows Server 2008 SP2.  
  
-   Per tutte le piattaforme, si consiglia di eseguire l'aggiornamento al Service Pack di Windows più recente e installare gli aggiornamenti critici disponibili nel [sito Web Windows Update](http://go.microsoft.com/fwlink/?LinkId=168461) per garantire la massima compatibilità e sicurezza. Su alcuni sistemi operativi potrebbe essere necessaria l'installazione dell'ultimo Windows Service Pack.  
  
-   Nei sistemi operativi a 64 bit, .NET Framework supporta sia WOW64 (elaborazione a 32 bit su un computer a 64 bit) che l'elaborazione nativa a 64 bit.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md)   
 [Introduzione](../../../docs/framework/get-started/index.md)   
 [Risoluzione dei problemi](../../../docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)
