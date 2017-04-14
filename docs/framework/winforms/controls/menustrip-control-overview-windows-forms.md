---
title: "Cenni preliminari sul controllo MenuStrip (Windows Form) | Microsoft Docs"
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
  - "MenuStrip"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "menu, creazione"
  - "MenuStrip (controllo) [Windows Form], informazioni sul controllo MenuStrip"
ms.assetid: f45516e5-bf01-4468-b851-d45f4c33c055
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sul controllo MenuStrip (Windows Form)
I menu espongono funzionalità agli utenti contenendo comandi raggruppati in base a un argomento comune.  
  
 Il controllo <xref:System.Windows.Forms.MenuStrip> è una novità della presente versione di Visual Studio e di .NET Framework.  Consente di creare con facilità menu simili a quelli di Microsoft Office.  
  
 Il controllo <xref:System.Windows.Forms.MenuStrip> supporta l'interfaccia a documenti multipli \(MDI, Multiple\-Document Interface\) e l'unione di menu, le descrizioni comandi e l'overflow.  È possibile migliorare le potenzialità di utilizzo e leggibilità dei menu aggiungendo tasti di scelta, tasti di scelta rapida, segni di spunta, immagini e barre di separazione.  
  
 Benché il controllo <xref:System.Windows.Forms.MenuStrip> sostituisca il controllo <xref:System.Windows.Forms.MainMenu> delle versioni precedenti aggiungendo funzionalità, il controllo <xref:System.Windows.Forms.MainMenu> viene mantenuto per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  
  
## Modalità di utilizzo del controllo MenuStrip  
 Utilizzare il controllo <xref:System.Windows.Forms.MenuStrip> per:  
  
-   Creare menu facilmente personalizzabili e di impiego frequente che supportino funzioni avanzate di interfaccia utente e layout, ad esempio ordinamento e allineamento di testo e immagini, operazioni di trascinamento della selezione, MDI, overflow e modalità alternative di accesso ai comandi di menu.  
  
-   Supportare l'aspetto e il comportamento tipici del sistema operativo.  
  
-   Gestire eventi in modo coerente per tutti i contenitori e gli elementi contenuti, nello stesso modo in cui si gestiscono eventi per altri controlli.  
  
 Nella tabella riportata di seguito sono indicate alcune proprietà particolarmente importanti di <xref:System.Windows.Forms.MenuStrip> e delle classi associate.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A>|Ottiene o imposta la classe <xref:System.Windows.Forms.ToolStripMenuItem> utilizzata per visualizzare un elenco di form figlio MDI.|  
|<xref:System.Windows.Forms.ToolStripItem.MergeAction%2A?displayProperty=fullName>|Ottiene o imposta la modalità di unione tra i menu del figlio e i menu del padre in applicazioni MDI.|  
|<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A?displayProperty=fullName>|Ottiene o imposta la posizione di un elemento unito all'interno di un menu in applicazioni MDI.|  
|<xref:System.Windows.Forms.Form.IsMdiContainer%2A?displayProperty=fullName>|Ottiene o imposta un valore che indica se il form è un contenitore di form figlio MDI.|  
|<xref:System.Windows.Forms.MenuStrip.ShowItemToolTips%2A>|Ottiene o imposta un valore che indica se le descrizioni comandi sono visualizzate per il controllo <xref:System.Windows.Forms.MenuStrip>.|  
|<xref:System.Windows.Forms.MenuStrip.CanOverflow%2A>|Ottiene o imposta un valore che indica se il controllo <xref:System.Windows.Forms.MenuStrip> supporta la funzionalità di overflow.|  
|<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A>|Ottiene o imposta i tasti di scelta rapida associati alla classe <xref:System.Windows.Forms.ToolStripMenuItem>.|  
|<xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A>|Ottiene o imposta un valore che indica se i tasti di scelta rapida associati alla classe <xref:System.Windows.Forms.ToolStripMenuItem> sono visualizzati accanto alla classe <xref:System.Windows.Forms.ToolStripMenuItem>.|  
  
 Nella tabella riportata di seguito sono elencate classi importanti correlate al controllo <xref:System.Windows.Forms.MenuStrip>.  
  
|Classe|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.Forms.ToolStripMenuItem>|Rappresenta un'opzione selezionabile visualizzata in un oggetto <xref:System.Windows.Forms.MenuStrip> o <xref:System.Windows.Forms.ContextMenuStrip>.|  
|<xref:System.Windows.Forms.ContextMenuStrip>|Viene visualizzato un menu di scelta rapida.|  
|<xref:System.Windows.Forms.ToolStripDropDown>|Rappresenta un controllo che consente all'utente di selezionare un singolo elemento da un elenco visualizzato quando fa clic su una classe <xref:System.Windows.Forms.ToolStripDropDownButton> o su una voce di menu di livello superiore.|  
|<xref:System.Windows.Forms.ToolStripDropDownItem>|Fornisce funzionalità di base per i controlli derivati dalla classe <xref:System.Windows.Forms.ToolStripItem> che, quando selezionati, visualizzano elementi a discesa.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ContextMenuStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 <xref:System.Windows.Forms.ToolStripItem>   
 <xref:System.Windows.Forms.ToolStripDropDown>