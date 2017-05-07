---
title: 'Mitigazione: Impostazioni cultura e operazioni asincrone | Documenti di Microsoft'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d2cdb578-9923-47df-9ffd-5865333ac1a4
caps.latest.revision: 4
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: c2dbf60cacf47be3c448b5683b771840ef85ddaf
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-culture-and-asynchronous-operations"></a>Mitigazione: Impostazioni cultura e operazioni asincrone
Per le app destinate a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e versioni successive, <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> vengono archiviate nell'oggetto <xref:System.Threading.ExecutionContext> di un thread, che passa attraverso operazioni asincrone.  
  
## <a name="impact"></a>Impatto  
 Come risultato di questa modifica, eventuali modifiche alle proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> si rifletteranno nelle attività che verranno avviate in seguito in modo asincrono. Questo comportamento è diverso dal comportamento delle versioni precedenti di .NET Framework, in cui le proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> sarebbero state riportate alle impostazioni predefinite di sistema in tutte le attività asincrone.  
  
## <a name="mitigation"></a>Attenuazione  
 Le app interessate da questa modifica possono aggirare il problema in uno dei due modi:  
  
-   Impostando in modo esplicito la proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> come prima operazione in un'attività asincrona.  
  
-   Consentendo il comportamento precedente di non propagazione delle proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> e aggiungendo l'elemento `AppContextSwitchOverrides` seguente al file di configurazione dell'applicazione:  
  
    ```xml  
  
    <configuration>  
        <runtime>  
            <AppContextSwitchOverrides value="Switch.System.Globalization.NoAsyncCurrentCulture=true" />  
        </runtime>  
    </configuration>  
  
    ```  
  
-   Consentendo il comportamento precedente di non propagazione delle proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> e impostando il commutatore di compatibilità seguente in modo programmatico:  
  
    ```csharp  
    AppContext.SetSwitch("Switch.System.Globalization.NoAsyncCurrentCulture", true);  
    ```  
  
    ```vb  
    AppContext.SetSwitch("Switch.System.Globalization.NoAsyncCurrentCulture", true)  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)
