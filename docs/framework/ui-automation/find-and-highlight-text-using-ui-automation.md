---
title: "Find and Highlight Text Using UI Automation | Microsoft Docs"
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
  - "text, highlighting"
  - "finding text"
  - "text, finding"
  - "UI automation, highlighting text"
  - "UI automation, finding text"
  - "highlighting text"
ms.assetid: b77693f5-87bb-4b29-a297-05ff882e2044
caps.latest.revision: 15
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 15
---
# Find and Highlight Text Using UI Automation
> [!NOTE]
>  La presente documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare le classi [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gestite definite nello spazio dei nomi <xref:System.Windows.Automation>.  Per informazioni aggiornate sull'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: Automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746) \(la pagina potrebbe essere in inglese\).  
  
 In questo argomento viene illustrato come eseguire ricerche in sequenza ed evidenziare ogni occorrenza di una stringa all'interno del contenuto di un controllo di testo utilizzando [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)].  
  
## Esempio  
 Nell'esempio seguente si ottiene un oggetto <xref:System.Windows.Automation.TextPattern> da un controllo di testo.  Viene quindi creato un oggetto <xref:System.Windows.Automation.Text.TextPatternRange>, che rappresenta il contenuto di testo dell'intero documento, utilizzando la proprietà <xref:System.Windows.Automation.TextPattern.DocumentRange%2A> di questo oggetto <xref:System.Windows.Automation.TextPattern>.  Infine vengono creati due oggetti <xref:System.Windows.Automation.Text.TextPatternRange> aggiuntivi per le funzionalità di ricerca in sequenza ed evidenziazione.  
  
 [!code-csharp[FindText#StartApp](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#startapp)]
 [!code-vb[FindText#StartApp](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#startapp)]  
[!code-csharp[FindText#FindTextProvider](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#findtextprovider)]
[!code-vb[FindText#FindTextProvider](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#findtextprovider)]  
[!code-csharp[FindText#SearchTarget](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#searchtarget)]
[!code-vb[FindText#SearchTarget](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#searchtarget)]  
  
## Vedere anche  
 [Find and Highlight Text Using UI Automation](../../../docs/framework/ui-automation/find-and-highlight-text-using-ui-automation.md)