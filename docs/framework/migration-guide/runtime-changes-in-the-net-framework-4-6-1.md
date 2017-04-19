---
title: Modifiche al runtime in .NET Framework 4.6.1 | Microsoft Docs
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
- runtime changes, .NET Framework
- runtime changes, .NET Framework 4.6.1
- application compatibility
ms.assetid: 9d97421c-5fee-4523-98c9-a158e7e6a1ee
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: b8c6ec4d0bad4a769fb4d19a98c9e8a4eda0db78
ms.lasthandoff: 04/18/2017

---
# <a name="runtime-changes-in-the-net-framework-461"></a>Modifiche al runtime in .NET Framework 4.6.1
In rari casi, le modifiche al runtime potrebbero incidere sulle app esistenti destinate alle versioni precedenti di .NET Framework, ma eseguite in una versione successiva del runtime di .NET Framework. Includono anche le differenze di comportamento tra le applicazioni eseguite in diversi ambienti di runtime di .NET Framework. [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] include modifiche nelle aree seguenti:  
  
-   [Windows Communication Foundation (WCF)](#WCF)  
  
-   [Windows Presentation Foundation (WPF)](#WPF)  
  
<a name="WCF"></a>   
## <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Associazione WCF con la modalità di sicurezza `TransportWithMessageCredential`|Per impostazione predefinita, l'associazione WCF che usa la modalità di sicurezza `TransportWithMessageCredential` non consente messaggi con un'intestazione "to" non firmata per le chiavi di sicurezza asimmetriche. A partire dalle app eseguite in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], è possibile ignorare questo requisito e ricevere messaggi senza intestazioni "to" firmate.|È un comportamento che prevede il consenso esplicito. Per consentire i messaggi con intestazioni "to" non firmate, aggiungere l'impostazione di configurazione seguente alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'app:<br /><br /> `<runtime>     <AppContextSwitchOverrides value="Switch.System.ServiceModel.AllowUnsignedToHeader=true" />  </runtime>`<br /><br /> Poiché è una funzionalità che prevede il consenso esplicito, non dovrebbe influire sul comportamento delle app esistenti.|Microsoft Edge|  
  
<a name="WPF"></a>   
## <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=fullName>|Quando <xref:System.Windows.Controls.ItemsControl> visualizza una raccolta usando la virtualizzazione (<xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A> = `true`) e lo scorrimento degli elementi (<xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A>=<xref:System.Windows.Controls.ScrollUnit?displayProperty=fullName>), e quando il controllo scorre fino a visualizzare un elemento con un'altezza in pixel diversa dagli elementi adiacenti, la proprietà <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=fullName> esegue un'iterazione di tutti gli elementi nella raccolta.   L'interfaccia utente non risponde durante l'iterazione. Se la raccolta è di grandi dimensioni, questa situazione può essere percepita come un blocco.<br /><br /> L'iterazione avviene in altre circostanze, anche nelle versioni precedenti a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Ad esempio, si verifica in caso di scorrimento in pixel (<xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A>=<xref:System.Windows.Controls.ScrollUnit?displayProperty=fullName>) quando viene rilevato un elemento con un'altezza diversa in pixel e in caso di scorrimento per elementi di dati gerarchici (ad esempio in un controllo <xref:System.Windows.Controls.TreeView> o un controllo <xref:System.Windows.Controls.ItemsControl> con raggruppamento abilitato) quando viene rilevato un elemento con un numero diverso di elementi discendenti rispetto agli elementi adiacenti.<br /><br /> Nel caso dello scorrimento per elementi e di altezze diverse in pixel, l'iterazione è stata introdotta in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] per correggere i bug nel layout dei dati gerarchici.  Non è necessaria se i dati sono flat (senza gerarchia) e [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] non la esegue in questo caso.|Se l'iterazione avviene in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] ma non nelle versioni precedenti, ovvero se <xref:System.Windows.Controls.ItemsControl> esegue lo scorrimento per elementi di un elenco flat con elementi con altezze diverse in pixel, esistono due soluzioni:<br /><br /> Installare [.NET Framework 4.6.2](../../../docs/framework/install/guide-for-developers.md).<br /><br /> Installare l'[hotfix HR 1605](https://support.microsoft.com/en-us/kb/3154529) per [!INCLUDE[net_v461](../../../includes/net-v461-md.md)].|Secondario|  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità delle applicazioni nella versione 4.6.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)
