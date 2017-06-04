---
title: "Cenni preliminari sul controllo StatusStrip | Microsoft Docs"
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
  - "StatusStrip"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "barre di stato, informazioni sulle barre di stato"
  - "StatusStrip (controllo) [Windows Form], informazioni sul controllo StatusStrip"
ms.assetid: c0d9bcbb-f8b8-46ef-bae2-4146b8c8ce99
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Cenni preliminari sul controllo StatusStrip
In un controllo <xref:System.Windows.Forms.StatusStrip> sono in genere presenti informazioni su un oggetto visualizzato su un <xref:System.Windows.Forms.Form>, sui componenti dell'oggetto o informazioni contestuali collegate alle operazioni di tale oggetto all'interno dell'applicazione.  In genere, un controllo <xref:System.Windows.Forms.StatusStrip> è composto da oggetti <xref:System.Windows.Forms.ToolStripStatusLabel>, in ciascuno dei quali è visualizzato un testo e\/o un'icona.  Il controllo <xref:System.Windows.Forms.StatusStrip> può contenere anche controlli <xref:System.Windows.Forms.ToolStripDropDownButton>, <xref:System.Windows.Forms.ToolStripSplitButton> e <xref:System.Windows.Forms.ToolStripProgressBar>.  
  
 Il valore predefinito <xref:System.Windows.Forms.StatusStrip> non ha pannelli.  Per aggiungere pannelli a un controllo <xref:System.Windows.Forms.StatusStrip> usare il metodo <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A?displayProperty=fullName>.  
  
 Esiste supporto completo per la gestione di elementi e comandi comuni di <xref:System.Windows.Forms.StatusStrip> in Visual Studio.  
  
 Vedere anche [StatusStrip \(editor della raccolta Items\)](http://msdn.microsoft.com/library/ms233631\(v=vs.110\)), [Finestra di dialogo Attività di StatusStrip](http://msdn.microsoft.com/library/ms233642\(v=vs.110\)).  
  
 Benché il controllo <xref:System.Windows.Forms.StatusStrip> sostituisca ed estenda il controllo <xref:System.Windows.Forms.StatusBar> delle versioni precedenti, il controllo <xref:System.Windows.Forms.StatusBar> viene mantenuto per compatibilità con le versioni precedenti e per eventuale uso futuro.  
  
### Membri importanti di StatusStrip  
  
|Nome|Descrizione|  
|----------|-----------------|  
|<xref:System.Windows.Forms.StatusStrip.CanOverflow%2A>|Ottiene o imposta un valore che indica se il controllo <xref:System.Windows.Forms.StatusStrip> supporta la funzionalità di overflow.|  
|<xref:System.Windows.Forms.StatusStrip.Stretch%2A>|Ottiene o imposta un valore che indica se il controllo <xref:System.Windows.Forms.StatusStrip> si estende da un'estremità all'altra nella propria classe <xref:System.Windows.Forms.ToolStripContainer>.|  
  
### Classi importanti correlate a StatusStrip  
  
|Nome|Descrizione|  
|----------|-----------------|  
|<xref:System.Windows.Forms.ToolStripStatusLabel>|Rappresenta un pannello in un controllo <xref:System.Windows.Forms.StatusStrip>.|  
|<xref:System.Windows.Forms.ToolStripDropDownButton>|Visualizza un oggetto <xref:System.Windows.Forms.ToolStripDropDown> associato dal quale l'utente può selezionare un singolo elemento.|  
|<xref:System.Windows.Forms.ToolStripSplitButton>|Rappresenta un controllo in due parti con un pulsante standard e un menu a discesa.|  
|<xref:System.Windows.Forms.ToolStripProgressBar>|Visualizza lo stato di completamento di un processo.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.StatusStrip>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A>