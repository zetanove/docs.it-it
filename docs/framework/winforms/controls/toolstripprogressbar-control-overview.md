---
title: "Cenni preliminari sul controllo ToolStripProgressBar | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ToolStripProgressBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "stato (controlli)"
  - "barre degli strumenti [Windows Form], indicatori di stato"
  - "ToolStripProgressBar (controllo) [Windows Form], informazioni sul controllo ToolStripProgressBar"
ms.assetid: ec3ab522-5fe4-4b4d-a551-bc19e84f4774
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Cenni preliminari sul controllo ToolStripProgressBar
Alle proprie funzionalità tipiche di analisi dei processi, il controllo <xref:System.Windows.Forms.ToolStripProgressBar> associa anche le funzionalità di raggruppamento verticale\/orizzontale e di rendering di tutti i controlli <xref:System.Windows.Forms.ToolStrip>.  Un controllo <xref:System.Windows.Forms.ToolStripProgressBar> è quasi sempre incluso in una classe <xref:System.Windows.Forms.StatusStrip> e meno frequentemente in una classe <xref:System.Windows.Forms.ToolStrip>.  
  
 Benché il controllo <xref:System.Windows.Forms.ToolStripProgressBar> sostituisca il controllo delle versioni precedenti aggiungendo funzionalità, il controllo <xref:System.Windows.Forms.ToolStripProgressBar> viene mantenuto per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  
  
### Membri importanti di ToolStripProgressBar  
  
|Nome|Descrizione|  
|----------|-----------------|  
|<xref:System.Windows.Forms.ToolStripProgressBar.MarqueeAnimationSpeed%2A>|Ottiene o imposta un valore che rappresenta il ritardo, in millisecondi, tra ciascun aggiornamento della visualizzazione di <xref:System.Windows.Forms.ProgressBarStyle>.|  
|<xref:System.Windows.Forms.ProgressBar.Maximum%2A>|Ottiene o imposta il limite superiore dell'intervallo definito per questo oggetto <xref:System.Windows.Forms.ToolStripProgressBar>.|  
|<xref:System.Windows.Forms.ToolStripProgressBar.Minimum%2A>|Ottiene o imposta il limite inferiore dell'intervallo definito per questo oggetto <xref:System.Windows.Forms.ToolStripProgressBar>.|  
|<xref:System.Windows.Forms.ToolStripProgressBar.Style%2A>|Ottiene o imposta lo stile utilizzato dal controllo <xref:System.Windows.Forms.ToolStripProgressBar> per visualizzare lo stato di avanzamento di un'operazione.|  
|<xref:System.Windows.Forms.ToolStripProgressBar.Value%2A>|Ottiene o imposta il valore corrente di <xref:System.Windows.Forms.ToolStripProgressBar>.|  
|<xref:System.Windows.Forms.ToolStripProgressBar.PerformStep%2A>|Sposta in avanti la posizione corrente dell'indicatore di stato in base al valore della proprietà <xref:System.Windows.Forms.ToolStripProgressBar.Step%2A>.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripProgressBar>