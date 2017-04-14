---
title: "Modifiche al runtime in .NET Framework 4.6.1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modifiche al runtime, .NET Framework"
  - "modifiche al runtime, .NET Framework 4.6.1"
  - "compatibilità delle applicazioni"
ms.assetid: 9d97421c-5fee-4523-98c9-a158e7e6a1ee
caps.latest.revision: 5
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 5
---
# Modifiche al runtime in .NET Framework 4.6.1
In rari casi, le modifiche al runtime potrebbero incidere sulle app esistenti destinate alle versioni precedenti di .NET Framework, ma eseguite in una versione successiva del runtime di .NET Framework. Includono anche le differenze di comportamento tra le applicazioni eseguite in diversi ambienti di runtime di .NET Framework. Il [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] include modifiche nelle aree seguenti:  
  
-   [Windows Communication Foundation (WCF)](#WCF)  
  
-   [Windows Presentation Foundation (WPF)](#WPF)  
  
<a name="WCF"></a>   
## <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Associazione di WCF con il `TransportWithMessageCredential` modalità di sicurezza|Per impostazione predefinita, WCF associazione che utilizza il `TransportWithMessageCredential` modalità di sicurezza non consente i messaggi con un unsigned "a" intestazione per le chiavi di sicurezza asimmetrica. A partire dalle applicazioni che eseguono il [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], è possibile ridurre questo requisito e ricevere messaggi che non sono firmati "intestazioni to".|È un comportamento che prevede il consenso esplicito. Per consentire i messaggi con unsigned "intestazioni a", aggiungere la seguente impostazione di configurazione per il [ <> \> ](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) sezione del file di configurazione dell'applicazione:<br /><br /> `<runtime>     <AppContextSwitchOverrides value="Switch.System.ServiceModel.AllowUnsignedToHeader=true" />  </runtime>`<br /><br /> Poiché è una funzionalità che prevede il consenso esplicito, non dovrebbe influire sul comportamento delle app esistenti.|Microsoft Edge|  
  
<a name="WPF"></a>   
## <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=fullName>|Quando un <xref:System.Windows.Controls.ItemsControl> Visualizza una raccolta mediante la virtualizzazione (<xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A> = `true`) e lo scorrimento elemento (<xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A>=<xref:System.Windows.Controls.ScrollUnit?displayProperty=fullName>), e quando si scorre il controllo per visualizzare un elemento la cui altezza in pixel è diverso dal router adiacenti, il <xref:System.Windows.Controls.VirtualizingStackPanel?displayProperty=fullName> scorre tutti gli elementi nella raccolta.   L'interfaccia utente non risponde durante l'iterazione;  Se la raccolta è di grandi dimensioni, questo può essere percepito come un blocco.<br /><br /> Si verifica l'iterazione in altre circostanze, anche nelle versioni precedenti a di [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Ad esempio, si verifica quando lo scorrimento pixel (<xref:System.Windows.Controls.VirtualizingPanel.ScrollUnit%2A>=<xref:System.Windows.Controls.ScrollUnit?displayProperty=fullName>) in presenza di un elemento con un'altezza di pixel diversa e durante lo scorrimento elemento dati gerarchici (ad esempio in un <xref:System.Windows.Controls.TreeView> controllo o un <xref:System.Windows.Controls.ItemsControl> con raggruppamento abilitato) in presenza di un elemento con un numero diverso di elementi discendenti più gli elementi adiacenti.<br /><br /> Nel caso di altezza di scorrimento elemento e diversi pixel, l'iterazione è stata introdotta nel [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] per correggere i bug nel layout di dati gerarchici.  Non è necessaria se i dati flat (non dispone di alcuna gerarchia) e [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] non viene eseguita in questo caso.|Se si verifica l'iterazione nel [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] ma non nelle versioni precedenti, vale a dire, se il <xref:System.Windows.Controls.ItemsControl> elemento-scorre l'elenco con elementi di altezza in pixel diversi, esistono due soluzioni:<br /><br /> Installare il [.NET Framework 4.6.2](../../../docs/framework/install/guide-for-developers.md).<br /><br /> Installare [hotfix 1605 HR](https://support.microsoft.com/en-us/kb/3154529) per il [!INCLUDE[net_v461](../../../includes/net-v461-md.md)].|Secondario|  
  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità delle applicazioni in 4.6.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)