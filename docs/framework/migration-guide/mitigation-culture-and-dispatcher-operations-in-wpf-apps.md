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
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 1aee32c5c50c4ff4309f93bff270e6c3b3c8f7cc
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="mitigation-culture-and-dispatcher-operations-in-wpf-apps"></a>Mitigazione: Impostazioni cultura e operazioni asincrone in app WPF
Nelle app destinate a .NET Framework 4.6 e .NET Framework 4.6.1 le modifiche alla proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> eseguite all'interno di <xref:System.Windows.Threading.Dispatcher> vengono perse al termine dell'operazione di Dispatcher. In modo analogo, le modifiche apportate a <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> all'esterno di un'operazione di Dispatcher potrebbero non essere disponibili quando viene eseguita l'operazione.  
  
 Questo è dovuto a una modifica in <xref:System.Threading.ExecutionContext> che determina l'archiviazione di <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> nel contesto di esecuzione. Le operazioni del dispatcher WPF archiviano il contesto di esecuzione usato per avviare l'operazione e ripristinano il contesto precedente dopo il completamento dell'operazione. Dato che <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> fanno ora parte di tale contesto, le modifiche di questi elementi all'interno di un'operazione di Dispatcher non vengono mantenute all'esterno dell'operazione.  
  
## <a name="impact"></a>Impatto  
 In pratica, questo significa che le modifiche apportate alle proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> potrebbero non essere trasferite tra i callback dell'interfaccia utente di WPF e altro codice in un'applicazione WPF.  
  
## <a name="mitigation"></a>Mitigazione  
 Le app interessate da questa modifica possono aggirare il problema in uno dei due modi:  
  
-   archiviando i valori <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> desiderati in un campo e controllando che siano impostati i valori corretti di <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> o <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> in tutti i corpi delle operazioni di <xref:System.Windows.Threading.Dispatcher> (inclusi i gestori di callback degli eventi dell'interfaccia utente).  
  
-   Poiché la modifica alla proprietà <xref:System.Threading.ExecutionContext> interessa solo le applicazioni WPF destinate a .NET Framework 4.6 o a .NET Framework 4.6.1, tale modifica può essere evitata impostando come destinazione .NET Framework 4.5.2 o a una versione di .NET Framework a partire dalla 4.6.2.  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)
