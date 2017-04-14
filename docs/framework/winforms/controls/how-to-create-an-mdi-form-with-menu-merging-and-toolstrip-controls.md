---
title: "Procedura: creare un form MDI con unione di menu e controlli ToolStrip | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "MenuStrip (controllo) [Windows Form]"
  - "barre degli strumenti [Windows Form]"
  - "ToolStrip (controllo) [Windows Form]"
  - "ToolStripPanel (controllo) [Windows Form]"
ms.assetid: 64992ed9-44af-4baf-b45f-863e6ab35711
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: creare un form MDI con unione di menu e controlli ToolStrip
Lo spazio dei nomi <xref:System.Windows.Forms?displayProperty=fullName> supporta le applicazioni MDI \(Multiple Document Interface, interfaccia a documenti multipli\), mentre il controllo <xref:System.Windows.Forms.MenuStrip> supporta l'unione di menu.  I form MDI possono inoltre usare i controlli <xref:System.Windows.Forms.ToolStrip>.  
  
 In [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] è disponibile un supporto completo per questa funzionalità.  
  
 Vedere anche [Procedura dettagliata: Creazione di un form MDI con unione di menu e controlli ToolStrip](http://msdn.microsoft.com/library/ms233676\(v=vs.110\))  
  
## Esempio  
 L'esempio di codice seguente illustra come usare i controlli <xref:System.Windows.Forms.ToolStripPanel> con un form MDI.  Il form supporta anche l'unione dei menu con menu figlio.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.MdiForm#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.MdiForm#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/VB/Form1.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 [Controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)