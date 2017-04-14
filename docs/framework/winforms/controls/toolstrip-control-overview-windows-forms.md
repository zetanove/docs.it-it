---
title: "Cenni preliminari sul controllo ToolStrip (Windows Form) | Microsoft Docs"
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
  - "Toolstrip"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "barre degli strumenti [Windows Form]"
  - "barre degli strumenti [Windows Form], novità in Windows Form"
  - "ToolStrip (controllo) [Windows Form], informazioni sul controllo ToolStrip"
  - "novità [Windows Form], barre degli strumenti"
ms.assetid: 81d067ed-297c-4dad-90de-1bcac15336ec
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Cenni preliminari sul controllo ToolStrip (Windows Form)
Il controllo <xref:System.Windows.Forms.ToolStrip> Windows Form e le relative classi associate forniscono un framework comune per combinare elementi dell'interfaccia utente nelle barre degli strumenti, nelle barre di stato e nei menu  I controlli <xref:System.Windows.Forms.ToolStrip> offrono molteplici funzionalità in fase di progettazione tra cui l'attivazione e la modifica sul posto, il layout personalizzato e il raggruppamento verticale\/orizzontale, ovvero la possibilità per le barre degli strumenti di condividere uno spazio orizzontale o verticale.  
  
 Benché il controllo <xref:System.Windows.Forms.ToolStrip> sostituisca il controllo delle versioni precedenti aggiungendo funzionalità, il controllo <xref:System.Windows.Forms.ToolBar> viene mantenuto per compatibilità con le versioni precedenti e per utilizzo futuro se lo si desidera.  
  
## Funzionalità dei controlli ToolStrip  
 Utilizzare il controllo <xref:System.Windows.Forms.ToolStrip> per:  
  
-   Presentare un'interfaccia utente comune tra tutti i contenitori.  
  
-   Creare barre degli strumenti di facile personalizzazione e di impiego frequente che supportino funzioni avanzate di interfaccia utente e layout, ad esempio ancoraggio, raggruppamento verticale\/orizzontale, pulsanti con testo e immagini, pulsanti e controlli a discesa, pulsanti di overflow e riordino di elementi <xref:System.Windows.Forms.ToolStrip> in fase di esecuzione.  
  
-   Supportare l'overflow e il riordino degli elementi in fase di esecuzione.  La funzionalità di overflow sposta gli elementi in un menu a discesa quando lo spazio disponibile non è sufficiente per visualizzarli in un <xref:System.Windows.Forms.ToolStrip>.  
  
-   Supportare l'aspetto e il comportamento tipici del sistema operativo tramite un modello di rendering comune.  
  
-   Gestire eventi in modo coerente per tutti i contenitori e gli elementi contenuti, nello stesso modo in cui si gestiscono eventi per altri controlli.  
  
-   Trascinare elementi da un <xref:System.Windows.Forms.ToolStrip> a un altro o all'interno di un <xref:System.Windows.Forms.ToolStrip>.  
  
-   Creare controlli a discesa ed editor di tipi con interfaccia utente con layout avanzati in una classe <xref:System.Windows.Forms.ToolStripDropDown>.  
  
 Utilizzare la classe <xref:System.Windows.Forms.ToolStripControlHost> per servirsi di altri controlli in un <xref:System.Windows.Forms.ToolStrip> e ottenere le funzionalità di <xref:System.Windows.Forms.ToolStrip> per essi.  
  
 È possibile estendere le funzionalità e modificare l'aspetto e il comportamento utilizzando le classi <xref:System.Windows.Forms.ToolStripRenderer>, <xref:System.Windows.Forms.ToolStripProfessionalRenderer> e <xref:System.Windows.Forms.ToolStripManager> insieme alle enumerazioni <xref:System.Windows.Forms.ToolStripRenderMode> e <xref:System.Windows.Forms.ToolStripManagerRenderMode>.  
  
 Il controllo <xref:System.Windows.Forms.ToolStrip> è particolarmente configurabile ed estendibile e fornisce un gran numero di proprietà, metodi ed eventi per la personalizzazione di aspetto e comportamento.  Di seguito sono riportati alcuni membri di una certa rilevanza:  
  
### Membri di ToolStrip importanti  
  
|Nome|Descrizione|  
|----------|-----------------|  
|<xref:System.Windows.Forms.ToolStrip.Dock%2A>|Ottiene o imposta il bordo del contenitore padre al quale è fissato un <xref:System.Windows.Forms.ToolStrip>.|  
|<xref:System.Windows.Forms.ToolStrip.AllowItemReorder%2A>|Ottiene o imposta un valore che indica se il trascinamento della selezione e il riordino di elementi sono gestiti in modo privato dalla classe <xref:System.Windows.Forms.ToolStrip>.|  
|<xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A>|Ottiene o imposta un valore che indica il modo in cui il <xref:System.Windows.Forms.ToolStrip> definisce i relativi elementi.|  
|<xref:System.Windows.Forms.ToolStripItem.Overflow%2A>|Ottiene o imposta un valore che indica se una classe <xref:System.Windows.Forms.ToolStripItem> è collegata al <xref:System.Windows.Forms.ToolStrip> o alla classe <xref:System.Windows.Forms.ToolStripOverflowButton> oppure se è mobile tra i due.|  
|<xref:System.Windows.Forms.ToolStrip.IsDropDown%2A>|Ottiene un valore che indica se una classe <xref:System.Windows.Forms.ToolStripItem> visualizza altri elementi in un elenco a discesa quando si fa clic su <xref:System.Windows.Forms.ToolStripItem>.|  
|<xref:System.Windows.Forms.ToolStrip.OverflowButton%2A>|Ottiene la classe <xref:System.Windows.Forms.ToolStripItem> che rappresenta il pulsante di overflow di un <xref:System.Windows.Forms.ToolStrip> in cui l'overflow è attivato.|  
|<xref:System.Windows.Forms.ToolStrip.Renderer%2A>|Ottiene o imposta un <xref:System.Windows.Forms.ToolStripRenderer> utilizzato per personalizzare l'aspetto e il comportamento di un <xref:System.Windows.Forms.ToolStrip>.|  
|<xref:System.Windows.Forms.ToolStrip.RenderMode%2A>|Ottiene o imposta gli stili di disegno da applicare al <xref:System.Windows.Forms.ToolStrip>.|  
|<xref:System.Windows.Forms.ToolStrip.RendererChanged>|Generato quando la proprietà <xref:System.Windows.Forms.ToolStrip.Renderer%2A> viene modificata.|  
  
 La flessibilità del controllo <xref:System.Windows.Forms.ToolStrip> è possibile grazie all'utilizzo di diverse classi correlate.  Di seguito ne sono riportate alcune di una certa rilevanza:  
  
### Classi importanti correlate a ToolStrip  
  
|Nome|Descrizione|  
|----------|-----------------|  
|<xref:System.Windows.Forms.MenuStrip>|Sostituisce la classe <xref:System.Windows.Forms.MainMenu> aggiungendo funzionalità.|  
|<xref:System.Windows.Forms.StatusStrip>|Sostituisce la classe <xref:System.Windows.Forms.StatusBar> aggiungendo funzionalità.|  
|<xref:System.Windows.Forms.ContextMenuStrip>|Sostituisce la classe <xref:System.Windows.Forms.ContextMenu> aggiungendo funzionalità.|  
|<xref:System.Windows.Forms.ToolStripItem>|Classe base astratta che gestisce eventi e layout per tutti gli elementi che possono essere contenuti in un <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.ToolStripControlHost> o <xref:System.Windows.Forms.ToolStripDropDown>.|  
|<xref:System.Windows.Forms.ToolStripContainer>|Fornisce un pannello a un contenitore su ogni lato del form in cui è possibile disporre i controlli in vari modi.|  
|<xref:System.Windows.Forms.ToolStripRenderer>|Gestisce la funzionalità di disegno per gli oggetti <xref:System.Windows.Forms.ToolStrip>.|  
|<xref:System.Windows.Forms.ToolStripProfessionalRenderer>|Attribuisce un aspetto in stile Microsoft Office.|  
|<xref:System.Windows.Forms.ToolStripManager>|Controlla il rendering e il raggruppamento verticale\/orizzontale dei controlli <xref:System.Windows.Forms.ToolStrip> nonché l'unione degli oggetti <xref:System.Windows.Forms.MenuStrip>, <xref:System.Windows.Forms.ToolStripDropDownMenu> e <xref:System.Windows.Forms.ToolStripMenuItem>.|  
|<xref:System.Windows.Forms.ToolStripManagerRenderMode>|Specifica lo stile di disegno \(personalizzato, Windows XP o Microsoft Office Professional\) applicato a più oggetti <xref:System.Windows.Forms.ToolStrip> contenuti in un form.|  
|<xref:System.Windows.Forms.ToolStripRenderMode>|Specifica lo stile di disegno \(personalizzato, Windows XP o Microsoft Office Professional\) applicato a un oggetto <xref:System.Windows.Forms.ToolStrip> contenuto in un form.|  
|<xref:System.Windows.Forms.ToolStripControlHost>|Include altri controlli che non sono controlli <xref:System.Windows.Forms.ToolStrip> in modo specifico ma per i quali si desidera disporre delle funzionalità di <xref:System.Windows.Forms.ToolStrip>.|  
|<xref:System.Windows.Forms.ToolStripItemPlacement>|Specifica se è necessario disporre una classe <xref:System.Windows.Forms.ToolStripItem> sul <xref:System.Windows.Forms.ToolStrip> principale, sul <xref:System.Windows.Forms.ToolStrip> di overflow o su nessuno dei due.|  
  
 Per ulteriori informazioni, vedere [Riepilogo della tecnologia ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md) e [Architettura del controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ContextMenuStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 <xref:System.Windows.Forms.ToolStripItem>   
 <xref:System.Windows.Forms.ToolStripDropDown>