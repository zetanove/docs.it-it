---
title: "Cenni preliminari sul controllo ToolStripContainer | Microsoft Docs"
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
  - "ToolStripContainer"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "barre degli strumenti [Windows Form], raggruppamento verticale/orizzontale incorporato"
  - "ToolStripContainer (controllo) [Windows Form], informazioni sul controllo ToolStripContainer"
ms.assetid: c7d63bff-64e2-4a63-bd89-d31bc96dacb8
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Cenni preliminari sul controllo ToolStripContainer
Un controllo <xref:System.Windows.Forms.ToolStripContainer> dispone di pannelli sul lato sinistro, destro, superiore e inferiore per il posizionamento e il raggruppamento verticale\/orizzontale di controlli <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip> e <xref:System.Windows.Forms.StatusStrip>.  Più controlli <xref:System.Windows.Forms.ToolStrip> vengono disposti in verticale se inseriti nel controllo <xref:System.Windows.Forms.ToolStripContainer> di sinistra o di destra.  Vengono disposti in orizzontale se inseriti nel controllo <xref:System.Windows.Forms.ToolStripContainer> superiore o inferiore.  È possibile utilizzare l'oggetto <xref:System.Windows.Forms.ToolStripContentPanel> centrale di <xref:System.Windows.Forms.ToolStripContainer> per posizionare controlli tradizionali nel form.  
  
 Alcuni o tutti i controlli <xref:System.Windows.Forms.ToolStripContainer> possono essere selezionati direttamente in fase di progettazione e possono essere eliminati.  Tutti i pannelli di un controllo <xref:System.Windows.Forms.ToolStripContainer> sono espandibili e comprimibili e vengono ridimensionati in funzione dei controlli che contengono.  
  
### Membri di ToolStripContainer importanti  
  
|Nome|Descrizione|  
|----------|-----------------|  
|<xref:System.Windows.Forms.ToolStripContainer.BottomToolStripPanel%2A>|Ottiene il pannello inferiore dell'oggetto <xref:System.Windows.Forms.ToolStripContainer>.|  
|<xref:System.Windows.Forms.ToolStripContainer.BottomToolStripPanelVisible%2A>|Ottiene o imposta un valore che indica se il pannello inferiore dell'oggetto <xref:System.Windows.Forms.ToolStripContainer> è visibile.|  
|<xref:System.Windows.Forms.ToolStripContainer.LeftToolStripPanel%2A>|Ottiene il pannello sinistro dell'oggetto <xref:System.Windows.Forms.ToolStripContainer>.|  
|<xref:System.Windows.Forms.ToolStripContainer.LeftToolStripPanelVisible%2A>|Ottiene o imposta un valore che indica se il pannello sinistro di <xref:System.Windows.Forms.ToolStripContainer> è visibile.|  
|<xref:System.Windows.Forms.ToolStripContainer.RightToolStripPanel%2A>|Ottiene il pannello destro di <xref:System.Windows.Forms.ToolStripContainer>.|  
|<xref:System.Windows.Forms.ToolStripContainer.RightToolStripPanelVisible%2A>|Ottiene o imposta un valore che indica se il pannello destro di <xref:System.Windows.Forms.ToolStripContainer> è visibile.|  
|<xref:System.Windows.Forms.ToolStripContainer.TopToolStripPanel%2A>|Ottiene il pannello superiore di <xref:System.Windows.Forms.ToolStripContainer>.|  
|<xref:System.Windows.Forms.ToolStripContainer.TopToolStripPanelVisible%2A>|Ottiene o imposta un valore che indica se il pannello superiore di <xref:System.Windows.Forms.ToolStripContainer> è visibile.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripContainer>   
 <xref:System.Windows.Forms.ToolStripContentPanel>