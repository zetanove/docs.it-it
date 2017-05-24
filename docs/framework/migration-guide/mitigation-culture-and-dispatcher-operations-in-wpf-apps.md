---
title: 'Mitigazione: Impostazioni cultura e operazioni asincrone in app WPF | Documenti di Microsoft'
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
ms.assetid: 455c1452-8ce0-45ae-a092-21fb8edf1cac
caps.latest.revision: 3
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 1aee32c5c50c4ff4309f93bff270e6c3b3c8f7cc
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-culture-and-dispatcher-operations-in-wpf-apps"></a>Mitigazione: Impostazioni cultura e operazioni asincrone in app WPF
Nelle app destinate a .NET Framework 4.6 e .NET Framework 4.6.1, eventuali modifiche apportate alla proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> all'interno di un <xref:System.Windows.Threading.Dispatcher> andranno perdute al termine dell'operazione del dispatcher. In modo analogo, le modifiche apportate a <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> all'esterno di un'operazione del dispatcher possono non essere disponibili quando viene eseguita l'operazione.  
  
 Ciò è dovuto a una modifica in <xref:System.Threading.ExecutionContext> che consente a <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> di essere archiviate nel contesto di esecuzione. Le operazioni del dispatcher WPF archiviano il contesto di esecuzione usato per avviare l'operazione e ripristinano il contesto precedente dopo il completamento dell'operazione. Poiché <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> fanno ora parte di questo contesto, le relative modifiche all'interno di un'operazione del dispatcher non persistono al di fuori dell'operazione.  
  
## <a name="impact"></a>Impatto  
 In pratica, ciò significa che le modifiche apportate alle proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> non vengono trasferite tra i callback dell'interfaccia utente di WPF e altro codice in un'applicazione WPF.  
  
## <a name="mitigation"></a>Attenuazione  
 Le app interessate da questa modifica possono aggirare il problema in uno dei due modi:  
  
-   Memorizzando la proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> desiderata in un campo e archiviando tutti i corpi delle operazioni <xref:System.Windows.Threading.Dispatcher> (inclusi i gestori di callback eventi dell'interfaccia utente) su cui è impostata la proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>.  
  
-   Poiché la modifica alla proprietà <xref:System.Threading.ExecutionContext> interessa solo le applicazioni WPF destinate a .NET Framework 4.6 o a .NET Framework 4.6.1, questa modifica può essere evitata indirizzando a .NET Framework 4.5.2 o a una versione di .NET Framework a partire da 4.6.2.  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)
