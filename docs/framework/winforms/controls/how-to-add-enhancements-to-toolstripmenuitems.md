---
title: "Procedura: aggiungere elementi per il perfezionamento di ToolStripMenuItems | Microsoft Docs"
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
  - "segni di spunta, aggiunta a menu"
  - "comandi [Windows Form], raggruppamento nei menu"
  - "immagini [Windows Form], aggiunta a menu"
  - "tasti di scelta rapida, visualizzazione nei menu"
  - "voci di menu, aggiunta di segni di spunta"
  - "voci di menu, aggiunta di immagini"
  - "voci di menu, visualizzazione di tasti di scelta"
  - "voci di menu, visualizzazione di tasti di scelta rapida"
  - "voci di menu, visualizzazione di separatori"
  - "menu, raggruppamento di comandi"
  - "separatori, visualizzazione nei menu"
  - "ToolStripMenuItems"
  - "ToolStripMenuItems, aggiunta di segni di spunta"
  - "ToolStripMenuItems, aggiunta di immagini"
  - "ToolStripMenuItems, visualizzazione di tasti di scelta"
  - "ToolStripMenuItems, visualizzazione di tasti di scelta rapida"
  - "ToolStripMenuItems, visualizzazione di barre di separazione"
  - "ToolStripSeparators, visualizzazione in MenuStrips"
ms.assetid: aa5f19bb-b545-4378-bfa6-36ba592f0d7c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: aggiungere elementi per il perfezionamento di ToolStripMenuItems
È possibile migliorare l'utilizzabilità dei controlli <xref:System.Windows.Forms.MenuStrip> e <xref:System.Windows.Forms.ContextMenuStrip> nei modi seguenti.  
  
-   Aggiungere segni di spunta per specificare se una funzionalità è attivata o meno, ad esempio se un righello è visualizzato lungo il margine di un'applicazione di elaborazione testi, o per indicare quali file sono visualizzati all'interno di un elenco, ad esempio in un menu **Finestra**.  
  
-   Aggiungere immagini che rappresentano visivamente i comandi di menu.  
  
-   Visualizzare i tasti di scelta rapida per fornire un'alternativa all'esecuzione dei comandi tramite il mouse.  Ad esempio, la combinazione di tasti CTRL\+C consente di eseguire il comando **Copy**.  
  
-   Visualizzare i tasti di scelta per fornire un'alternativa alla navigazione dei menu tramite il mouse.  Ad esempio, la combinazione di tasti ALT\+F consente di selezionare il menu **File**.  
  
-   Mostrare le barre di separazione per raggruppare i comandi correlati e facilitare l'utilizzo dei menu.  
  
### Per visualizzare un segno di spunta accanto a un comando di menu  
  
-   Impostarne la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> su `true`.  
  
     In questo modo si imposta anche la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.CheckState%2A> su `true`.  Seguire questa procedura solo se si desidera che il comando di menu sia selezionato per impostazione predefinita.  
  
### Per visualizzare un segno di spunta che modifichi lo stato con ogni clic  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> del comando di menu su `true`.  
  
### Per aggiungere un'immagine a un comando di menu  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Image%2A> del comando di menu sul nome dell'immagine.  Se la proprietà <xref:System.Windows.Forms.ToolStripItemDisplayStyle> di questo comando di menu è impostata su <xref:System.Windows.Forms.ToolStripItemDisplayStyle> o <xref:System.Windows.Forms.ToolStripItemDisplayStyle>, non è possibile visualizzare l'immagine.  
  
> [!NOTE]
>  È inoltre possibile visualizzare un segno di spunta sul margine dell'immagine.  È altresì possibile impostare la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> dell'immagine su `true`. L'immagine verrà visualizzata con un bordo tratteggiato in fase di esecuzione.  
  
### Per visualizzare i tasti di scelta rapida per un comando di menu  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A> del comando di menu sulla combinazione di tasti desiderata, ad esempio CTRL\+O per il comando di menu **Open**, e la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A> su `true`.  
  
### Per visualizzare i tasti di scelta personalizzati per un comando di menu  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeyDisplayString%2A> del comando di menu sulla combinazione di tasti desiderata, ad esempio CTRL\+MAIUSC\+O invece di MAIUSC\+CTRL\+O, e la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A> su `true`.  
  
### Per visualizzare un tasto di scelta per un comando di menu  
  
-   Quando si imposta la proprietà <xref:System.Windows.Forms.ToolStripItem.Text%2A> per il comando di menu, immettere una e commerciale \(&\) prima della lettera che costituirà il tasto di scelta.  Ad esempio, se si digita  `&Open` come proprietà <xref:System.Windows.Forms.ToolStripItem.Text%2A> di un comando di menu, il comando di menu visualizzato sarà **O**pen.  
  
     Per passare a questo comando di menu, premere ALT per attivare la classe <xref:System.Windows.Forms.MenuStrip>, quindi premere il tasto di scelta corrispondente al nome del menu.  Verrà visualizzato il menu con le voci di menu e i relativi tasti di scelta. A questo punto è sufficiente premere il tasto di scelta appropriato per scegliere il comando di menu desiderato.  
  
> [!NOTE]
>  Evitare di definire tasti di scelta doppi, ad esempio definire ALT\+F due volte nello stesso menu di sistema.  L'ordine di selezione dei tasti di scelta doppi non può essere garantito.  
  
### Per visualizzare una barra di separazione tra i comandi di menu  
  
-   Dopo avere definito la classe <xref:System.Windows.Forms.MenuStrip> e i relativi elementi, utilizzare il metodo <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A> o <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> per aggiungere i comandi di menu e i controlli <xref:System.Windows.Forms.ToolStripSeparator> alla classe <xref:System.Windows.Forms.MenuStrip> nell'ordine desiderato.  
  
     \[Visual Basic\]  
  
    ```  
    ' This code adds a top-level File menu to the MenuStrip.  
    Me.menuStrip1.Items.Add(New ToolStripMenuItem() _  
    {Me.fileToolStripMenuItem})  
  
    ' This code adds the New and Open menu commands, a separator bar,   
    ' and the Save and Exit menu commands to the top-level File menu,   
    ' in that order.  
    Me.fileToolStripMenuItem.DropDownItems.AddRange(New _  
    ToolStripMenuItem() {Me.newToolStripMenuItem, _  
    Me.openToolStripMenuItem, Me.toolStripSeparator1, _  
    Me.saveToolStripMenuItem, Me.exitToolStripMenuItem})  
  
    ```  
  
     \[C\#\]  
  
    ```  
    // This code adds a top-level File menu to the MenuStrip.  
    this.menuStrip1.Items.Add(new ToolStripItem[]_  
    {this.fileToolStripMenuItem});  
  
    // This code adds the New and Open menu commands, a separator bar,   
    // and the Save and Exit menu commands to the top-level File menu,   
    // in that order.  
    this.fileToolStripMenuItem.DropDownItems.AddRange(new _  
    ToolStripItem[] {  
    this.newToolStripMenuItem,  
    this.openToolStripMenuItem,  
    this.toolStripSeparator1,  
    this.saveToolStripMenuItem,  
    this.exitToolStripMenuItem});  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)