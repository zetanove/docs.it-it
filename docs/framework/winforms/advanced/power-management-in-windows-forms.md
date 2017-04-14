---
title: "Power Management in Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "battery states"
  - "power states"
ms.assetid: ad04a801-5682-4d88-92c5-26eb9cdb209a
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Power Management in Windows Forms
Le applicazioni Windows Form possono sfruttare le funzionalità di risparmio energia disponibili nel sistema operativo Windows.  Le applicazioni possono monitorare lo stato dell'alimentazione di un computer ed eseguire una determinata azione in caso di variazione di tale stato.  Se ad esempio l'applicazione è in esecuzione su un computer portatile, è possibile disabilitare alcune funzionalità dell'applicazione quando il livello di carica della batteria scende al di sotto di una determinata soglia.  
  
 In [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] è disponibile un evento <xref:Microsoft.Win32.SystemEvents.PowerModeChanged> che viene generato ogni volta che si verifica una variazione nello stato dell'alimentazione, ad esempio quando un utente sospende o ripristina il sistema operativo oppure quando lo stato dell'alimentazione CA o della batteria cambia.  La proprietà <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A> della classe <xref:System.Windows.Forms.SystemInformation> può essere utilizzata per eseguire una query sullo stato corrente, come illustrato nell'esempio di codice riportato di seguito.  
  
 [!code-csharp[PowerMode#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/powermode/cs/form1.cs#1)]
 [!code-vb[PowerMode#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/powermode/vb/form1.vb#1)]  
  
 Oltre alle enumerazioni <xref:System.Windows.Forms.BatteryChargeStatus>, la proprietà <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A> contiene anche le enumerazioni per determinare la capacità della batteria \(<xref:System.Windows.Forms.PowerStatus.BatteryFullLifetime%2A>\) e la percentuale di carica della batteria \(<xref:System.Windows.Forms.PowerStatus.BatteryLifePercent%2A>, <xref:System.Windows.Forms.PowerStatus.BatteryLifeRemaining%2A>\).  
  
 È possibile utilizzare il metodo <xref:System.Windows.Forms.Application.SetSuspendState%2A> di <xref:System.Windows.Forms.Application> per impostare il computer in modalità di ibernazione.  Se l'argomento `force` è impostato su `false`, verrà trasmesso un evento a tutte le applicazioni che richiedono, per la sospensione, un'autorizzazione.  Se l'argomento `disableWakeEvent` è impostato su `true`, verranno disabilitati automaticamente tutti gli eventi di riattivazione.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come impostare un computer in modalità di ibernazione.  
  
 [!code-csharp[PowerMode#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/powermode/cs/form1.cs#2)]
 [!code-vb[PowerMode#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/powermode/vb/form1.vb#2)]  
  
## Vedere anche  
 <xref:Microsoft.Win32.SystemEvents.PowerModeChanged>   
 <xref:System.Windows.Forms.SystemInformation.PowerStatus%2A>   
 <xref:System.Windows.Forms.Application.SetSuspendState%2A>   
 <xref:Microsoft.Win32.SystemEvents.SessionSwitch>