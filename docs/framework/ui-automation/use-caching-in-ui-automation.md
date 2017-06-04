---
title: "Use Caching in UI Automation | Microsoft Docs"
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
  - "caching, UI Automation"
  - "UI Automation, caching"
ms.assetid: ec722dff-6009-4279-b86a-e18d3fa94ebf
caps.latest.revision: 14
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 14
---
# Use Caching in UI Automation
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questa sezione viene illustrato come implementare la memorizzazione nella cache delle proprietà e dei pattern di controllo per <xref:System.Windows.Automation.AutomationElement>.  
  
### Attivare una richiesta della cache  
  
1.  Creare un oggetto <xref:System.Windows.Automation.CacheRequest>.  
  
2.  Specificare le proprietà e i pattern da memorizzare nella cache mediante <xref:System.Windows.Automation.CacheRequest.Add%2A>.  
  
3.  Specificare l'ambito di memorizzazione nella cache impostando la proprietà <xref:System.Windows.Automation.CacheRequest.TreeScope%2A>.  
  
4.  Specificare la visualizzazione del sottoalbero impostando la proprietà <xref:System.Windows.Automation.CacheRequest.TreeFilter%2A>.  
  
5.  Impostare la proprietà <xref:System.Windows.Automation.CacheRequest.AutomationElementMode%2A> su <xref:System.Windows.Automation.AutomationElementMode> se si desidera aumentare l'efficienza evitando di recuperare un riferimento completo agli oggetti. Ciò non consente di recuperare i valori correnti tali oggetti.  
  
6.  Attivare la richiesta usando <xref:System.Windows.Automation.CacheRequest.Activate%2A> all'interno di un blocco `using` \(`Using` in [!INCLUDE[TLA#tla_visualbnet](../../../includes/tlasharptla-visualbnet-md.md)]\).  
  
 Dopo aver ottenuto gli oggetti <xref:System.Windows.Automation.AutomationElement> o aver eseguito la sottoscrizione degli eventi, disattivare la richiesta usando <xref:System.Windows.Automation.CacheRequest.Pop%2A> \(se è stata usata <xref:System.Windows.Automation.CacheRequest.Push%2A>\) oppure eliminando l'oggetto creato da <xref:System.Windows.Automation.CacheRequest.Activate%2A>. \(Usare <xref:System.Windows.Automation.CacheRequest.Activate%2A> in un blocco `using` \(`Using` in [!INCLUDE[TLA#tla_visualbnet](../../../includes/tlasharptla-visualbnet-md.md)]\).  
  
### Memorizzare nella cache le proprietà della classe AutomationElement  
  
1.  Mentre è attiva una classe <xref:System.Windows.Automation.CacheRequest>, ottenere gli oggetti <xref:System.Windows.Automation.AutomationElement> mediante <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> o <xref:System.Windows.Automation.AutomationElement.FindAll%2A> oppure ottenere una classe <xref:System.Windows.Automation.AutomationElement> come origine di un evento per il quale è stata eseguita la registrazione quando la classe <xref:System.Windows.Automation.CacheRequest> è attiva. È inoltre possibile creare una cache passando <xref:System.Windows.Automation.CacheRequest> a GetUpdatedCache oppure uno dei metodi della classe <xref:System.Windows.Automation.TreeWalker>.  
  
2.  Usare <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A> o recuperare una proprietà dalla proprietà <xref:System.Windows.Automation.AutomationElement.Cached%2A> della classe <xref:System.Windows.Automation.AutomationElement>.  
  
### Ottenere pattern memorizzati nella cache e le relative proprietà  
  
1.  Mentre è attiva una classe <xref:System.Windows.Automation.CacheRequest>, ottenere gli oggetti <xref:System.Windows.Automation.AutomationElement> mediante <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> o <xref:System.Windows.Automation.AutomationElement.FindAll%2A> oppure ottenere una classe <xref:System.Windows.Automation.AutomationElement> come origine di un evento per il quale è stata eseguita la registrazione quando la classe <xref:System.Windows.Automation.CacheRequest> è attiva. È inoltre possibile creare una cache passando <xref:System.Windows.Automation.CacheRequest> a GetUpdatedCache oppure uno dei metodi della classe <xref:System.Windows.Automation.TreeWalker>.  
  
2.  Usare <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> o <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> per recuperare un pattern memorizzato nella cache.  
  
3.  Recuperare i valori di proprietà dalla proprietà `Cached` del pattern di controllo.  
  
## Esempio  
 Nell'esempio di codice seguente sono illustrati i vari aspetti della memorizzazione nella cache mediante l'uso di <xref:System.Windows.Automation.CacheRequest.Activate%2A> per attivare <xref:System.Windows.Automation.CacheRequest>.  
  
 [!code-csharp[UIAClient_snip#107](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#107)]
 [!code-vb[UIAClient_snip#107](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#107)]  
  
## Esempio  
 Nell'esempio di codice seguente sono illustrati i vari aspetti della memorizzazione nella cache mediante l'uso di <xref:System.Windows.Automation.CacheRequest.Push%2A> per attivare <xref:System.Windows.Automation.CacheRequest>. Tranne quando si desidera nidificare le richieste della cache, è preferibile usare <xref:System.Windows.Automation.CacheRequest.Activate%2A>.  
  
 [!code-csharp[UIAClient_snip#108](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#108)]
 [!code-vb[UIAClient_snip#108](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#108)]  
  
## Vedere anche  
 [Caching in UI Automation Clients](../../../docs/framework/ui-automation/caching-in-ui-automation-clients.md)