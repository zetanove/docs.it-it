---
title: "Add Content to a Text Box Using UI Automation | Microsoft Docs"
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
  - "adding content to text boxes"
  - "text boxes, adding content"
  - "UI Automation, adding content to text boxes"
ms.assetid: 8bdd1a73-1ecb-4a05-a891-a7827ebb767f
caps.latest.revision: 13
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 13
---
# Add Content to a Text Box Using UI Automation
> [!NOTE]
>  La presente documentazione è destinata agli sviluppatori di .NET Framework che desiderano utilizzare le classi [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gestite definite nello spazio dei nomi <xref:System.Windows.Automation>.  Per informazioni aggiornate sull'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: Automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746) \(la pagina potrebbe essere in inglese\).  
  
 Questo argomento contiene un esempio di codice in cui viene illustrato come utilizzare [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] per inserire testo in una casella di testo a riga singola.  Viene fornito un metodo alternativo per i controlli a più righe e rich text, per cui l'[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] non è applicabile.  A scopo di confronto, nell'esempio viene illustrato anche come utilizzare i metodi Win32 per ottenere gli stessi risultati.  
  
## Esempio  
 Nell'esempio seguente viene illustrata una sequenza di controlli di testo in un'applicazione di destinazione.  Ogni controllo di testo viene testato per verificare se è possibile ottenere un oggetto <xref:System.Windows.Automation.ValuePattern> tramite il metodo <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A>.  Se il controllo di testo supporta <xref:System.Windows.Automation.ValuePattern>, viene utilizzato il metodo <xref:System.Windows.Automation.ValuePattern.SetValue%2A> per inserire una stringa definita dall'utente nel controllo di testo.  In caso contrario, viene utilizzato il metodo <xref:System.Windows.Forms.SendKeys.SendWait%2A?displayProperty=fullName>.  
  
 [!code-csharp[InsertText#InsertText](../../../samples/snippets/csharp/VS_Snippets_Wpf/InsertText/CSharp/Window1.xaml.cs#inserttext)]
 [!code-vb[InsertText#InsertText](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InsertText/VisualBasic/Window1.xaml.vb#inserttext)]  
  
## Vedere anche  
 [TextPattern Insert Text Sample](http://msdn.microsoft.com/it-it/67353f93-7ee2-42f2-ab76-5c078cf6ca16)