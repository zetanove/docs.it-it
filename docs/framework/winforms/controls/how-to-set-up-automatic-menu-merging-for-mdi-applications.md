---
title: "Procedura: impostare l&#39;unione automatica dei menu per applicazioni MDI | Microsoft Docs"
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
  - "MenuStrip, unione"
  - "Unione, menu automatico"
ms.assetid: 55e32cad-1141-4a56-aa33-d9543ca3d393
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: impostare l&#39;unione automatica dei menu per applicazioni MDI
Nella procedura seguente vengono forniti i passaggi di base per l'impostazione dell'unione automatica in un'applicazione con interfaccia a documenti multipli \(MDI\) con il controllo <xref:System.Windows.Forms.MenuStrip>.  
  
### Per impostare l'unione automatica dei menu  
  
1.  Creare il form padre MDI impostando la proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A> su `true`.  
  
2.  Aggiungere un controllo <xref:System.Windows.Forms.MenuStrip> al padre MDI, impostando la proprietà <xref:System.Windows.Forms.Form.MainMenuStrip%2A> su tale controllo <xref:System.Windows.Forms.MenuStrip>.  
  
3.  Creare un form figlio MDI e impostare la proprietà <xref:System.Windows.Forms.Form.MdiParent%2A> sul nome del form padre.  
  
4.  Aggiungere un controllo <xref:System.Windows.Forms.MenuStrip> al form figlio MDI.  
  
5.  Nel form figlio impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Visible%2A> del controllo <xref:System.Windows.Forms.MenuStrip> su `false`.  
  
6.  Aggiungere le voci di menu al controllo <xref:System.Windows.Forms.MenuStrip> del form figlio che si desidera unire nel controllo <xref:System.Windows.Forms.MenuStrip> del form padre quando viene attivato il form figlio.  
  
7.  Utilizzare la proprietà <xref:System.Windows.Forms.ToolStripItem.MergeAction%2A> delle voci di menu nel controllo <xref:System.Windows.Forms.MenuStrip> del form figlio per controllare la modalità di unione nel form padre.  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)