---
title: "Obtain Mixed Text Attribute Details Using UI Automation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d0e4c005-abd1-42bb-92a4-5faf87097311
caps.latest.revision: 11
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 11
---
# Obtain Mixed Text Attribute Details Using UI Automation
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 In questo argomento viene illustrato come usare [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] per ottenere dettagli sugli attributi di testo da un intervallo di testo che si estende su più valori di attributo. Un intervallo di testo può corrispondere alla posizione corrente del punto di inserimento \(o selezione degenere\) all'interno di un documento, una selezione contigua di testo, un insieme di selezioni di testo non contigue o l'intero contenuto testuale di un documento.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come ottenere <xref:System.Windows.Automation.TextPattern.FontNameAttribute> da un intervallo di testo, dove <xref:System.Windows.Automation.Text.TextPatternRange.GetAttributeValue%2A> restituisce un oggetto <xref:System.Windows.Automation.TextPattern.MixedAttributeValue>.  
  
 [!code-csharp[FindText#RetrieveMixedAttributes](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#retrievemixedattributes)]
 [!code-vb[FindText#RetrieveMixedAttributes](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#retrievemixedattributes)]  
  
 Il pattern di controllo <xref:System.Windows.Automation.TextPattern>, in combinazione con la classe <xref:System.Windows.Automation.Text.TextPatternRange>, supporta gli attributi, le proprietà e i metodi di base del testo. Per la funzionalità specifica del controllo non supportata da <xref:System.Windows.Automation.TextPattern> o <xref:System.Windows.Automation.Text.TextPatternRange>, la classe <xref:System.Windows.Automation.AutomationElement> implementa metodi per un client di automazione interfaccia utente per accedere al corrispondente modello a oggetti nativo.  
  
## Vedere anche  
 [UI Automation TextPattern Overview](../../../docs/framework/ui-automation/ui-automation-textpattern-overview.md)   
 [Add Content to a Text Box Using UI Automation](../../../docs/framework/ui-automation/add-content-to-a-text-box-using-ui-automation.md)   
 [Find and Highlight Text Using UI Automation](../../../docs/framework/ui-automation/find-and-highlight-text-using-ui-automation.md)   
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Obtain Text Attributes Using UI Automation](../../../docs/framework/ui-automation/obtain-text-attributes-using-ui-automation.md)