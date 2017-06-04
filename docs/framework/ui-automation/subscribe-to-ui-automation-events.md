---
title: "Sottoscrivere gli eventi di automazione interfaccia utente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Automazione interfaccia utente, la sottoscrizione di eventi"
  - "sottoscrizione a eventi di automazione interfaccia utente"
  - "eventi, la sottoscrizione a"
  - "attesa di eventi"
ms.assetid: b688effa-b3e8-4b05-944d-05ed89a245aa
caps.latest.revision: 16
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 16
---
# Sottoscrivere gli eventi di automazione interfaccia utente
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare gestita [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classi definite nel <xref:System.Windows.Automation> dello spazio dei nomi. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Questo argomento illustra come sottoscrivere gli eventi generati dai provider di automazione interfaccia utente.  
  
## <a name="example"></a>Esempio  
 Il codice di esempio seguente registra un gestore eventi per l'evento che viene generato quando viene richiamato un controllo, ad esempio un pulsante, e lo rimuove quando il form dell'applicazione viene chiuso. L'evento è identificato da un <xref:System.Windows.Automation.AutomationEvent> passato come parametro per <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>.  
  
 [!code-csharp[UIAClient_snip#101](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#101)]
 [!code-vb[UIAClient_snip#101](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#101)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] per sottoscrivere un evento generato quando cambia lo stato attivo. Il gestore eventi non è registrato in un metodo che può essere chiamato all'arresto dell'applicazione o quando la notifica degli eventi dell'interfaccia utente non è più necessaria.  
  
 [!code-csharp[UIAClient_snip#102](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#102)]
 [!code-vb[UIAClient_snip#102](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#102)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>   
 <xref:System.Windows.Automation.Automation.RemoveAllEventHandlers%2A>   
 <xref:System.Windows.Automation.Automation.RemoveAutomationEventHandler%2A>   
 [Cenni preliminari sugli eventi di automazione interfaccia utente](../../../docs/framework/ui-automation/ui-automation-events-overview.md)