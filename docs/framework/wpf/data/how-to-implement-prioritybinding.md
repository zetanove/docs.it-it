---
title: "Procedura: implementare un oggetto PriorityBinding | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "classi, PriorityBinding"
  - "associazione dati, PriorityBinding (classe)"
  - "PriorityBinding (classe)"
ms.assetid: d63b65ab-b3e9-4322-9aa8-1450f8d89532
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: implementare un oggetto PriorityBinding
Il funzionamento di <xref:System.Windows.Data.PriorityBinding> in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] è basato sulla specifica di un elenco di associazioni.  L'elenco di associazioni è ordinato dalla priorità più elevata a quella meno elevata.  Se l'associazione con la priorità più elevata restituisce correttamente un valore durante la relativa elaborazione, non sarà necessario elaborare le altre associazioni in elenco.  Nel caso in cui l'associazione con la priorità più elevata richieda tempi lunghi per la relativa valutazione, verrà utilizzata la priorità immediatamente successiva che restituisce correttamente un valore, finché un'associazione con priorità più elevata non restituisce a sua volta un valore corretto.  
  
## Esempio  
 Per mostrare il funzionamento di <xref:System.Windows.Data.PriorityBinding>, è stato creato l'oggetto `AsyncDataSource` con le seguenti tre proprietà: `FastDP`, `SlowerDP` e `SlowestDP`.  
  
 La funzione di accesso get di `FastDP` restituisce il valore del membro dati `_fastDP`.  
  
 La funzione di accesso get di `SlowerDP` rimane in attesa per 3 secondi prima di restituire il valore del membro dati `_slowerDP`.  
  
 La funzione di accesso get di `SlowestDP` rimane in attesa per 5 secondi prima di restituire il valore del membro dati `_slowestDP`.  
  
> [!NOTE]
>  Questo esempio viene riportato a scopo puramente dimostrativo.  Nelle linee guida di [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] si consiglia di non definire le proprietà che risultino notevolmente più lente rispetto a un insieme di campi.  Per ulteriori informazioni, vedere [NIB: Choosing Between Properties and Methods](http://msdn.microsoft.com/it-it/55825e8f-7e2e-448a-9505-7217cc91b1af).  
  
 [!code-csharp[PriorityBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml.cs#1)]
 [!code-vb[PriorityBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PriorityBinding/VisualBasic/AsyncDataSource.vb#1)]  
  
 La proprietà <xref:System.Windows.Controls.TextBlock.Text%2A> viene associata all'oggetto `AsyncDS` indicato in precedenza tramite <xref:System.Windows.Data.PriorityBinding>:  
  
 [!code-xml[PriorityBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml#2)]  
  
 Quando il motore di associazione elabora gli oggetti <xref:System.Windows.Data.Binding>, inizia dal primo oggetto <xref:System.Windows.Data.Binding> associato alla proprietà `SlowestDP`.  Durante l'elaborazione, tale oggetto <xref:System.Windows.Data.Binding> non restituisce correttamente alcun valore perché rimane inattivo per 5 secondi; viene quindi elaborato l'elemento <xref:System.Windows.Data.Binding> successivo.  L'oggetto <xref:System.Windows.Data.Binding> successivo, a sua volta, non restituisce correttamente alcun valore, perché rimane inattivo per 3 secondi.  Il motore di associazione passa quindi all'elemento <xref:System.Windows.Data.Binding> successivo, associato alla proprietà `FastDP`.  Tale oggetto <xref:System.Windows.Data.Binding> restituisce il valore "Fast Value".  Nell'oggetto <xref:System.Windows.Controls.TextBlock> viene ora visualizzato il valore "Fast Value".  
  
 Trascorsi 3 secondi, la proprietà `SlowerDP` restituisce il valore "Slower Value".  Nell'oggetto <xref:System.Windows.Controls.TextBlock> viene quindi visualizzato il valore "Slower Value".  
  
 Trascorsi 5 secondi, la proprietà `SlowestDP` restituisce il valore "Slowest Value".  Tale associazione ha la priorità più elevata perché viene visualizzata per prima nell'elenco.  Nell'oggetto <xref:System.Windows.Controls.TextBlock> viene ora visualizzato il valore "Slowest Value".  
  
 Per informazioni sulla definizione di valore restituito correttamente da un'associazione, vedere <xref:System.Windows.Data.PriorityBinding>.  
  
## Vedere anche  
 <xref:System.Windows.Data.Binding.IsAsync%2A?displayProperty=fullName>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)