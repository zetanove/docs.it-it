---
title: "Unione delle voci di menu nel controllo MenuStrip Windows Form | Microsoft Docs"
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
  - "unione, concetti generali"
ms.assetid: 95e113ba-f362-4dda-8a76-6d95ddc45cee
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Unione delle voci di menu nel controllo MenuStrip Windows Form
Se si dispone di un'applicazione con interfaccia a documenti multipli \(MDI\), è possibile unire voci di menu o interi menu del form figlio nei menu del form padre.  
  
 In questo argomento vengono descritti i concetti di base associati al merging di voci di menu in un'applicazione MDI.  
  
## Concetti generali  
 Le procedure di merging coinvolgono un controllo di destinazione e un controllo di origine:  
  
-   La destinazione è il controllo <xref:System.Windows.Forms.MenuStrip> sul form padre principale o MDI in cui viene eseguito il merge delle voci di menu.  
  
-   L'origine è il controllo <xref:System.Windows.Forms.MenuStrip> sul form figlio MDI che contiene le voci di menu da unire nel menu di destinazione.  
  
 La proprietà <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> identifica la voce di menu nel cui elenco a discesa verranno inseriti i titoli dei figlio MDI del form padre MDI corrente.  Ad esempio, in genere vengono elencati i form figlio MDI che sono attualmente aperti nel menu **Finestra**.  
  
 La proprietà <xref:System.Windows.Forms.ToolStripMenuItem.IsMdiWindowListEntry%2A> identifica quali voci di menu provengono da un controllo <xref:System.Windows.Forms.MenuStrip> in un form figlio MDI.  
  
 È possibile unire le voci di menu manualmente o automaticamente.  Le procedure di unione sono identiche per entrambi i metodi, ma l'unione viene attivata in modo diverso, come descritto nelle sezioni "Unione manuale" e "Unione automatica" più avanti in questo argomento.  Nell'unione manuale e automatica ogni azione di unione influisce sulla successiva.  
  
 Il merging con <xref:System.Windows.Forms.MenuStrip> sposta le voci di menu da un controllo <xref:System.Windows.Forms.ToolStrip> a un altro anziché duplicarle, come avviene invece con <xref:System.Windows.Forms.MainMenu>.  
  
## Valori di MergeAction  
 Per impostare l'azione di unione nelle voci di menu nel controllo <xref:System.Windows.Forms.MenuStrip> di origine, utilizzare la proprietà <xref:System.Windows.Forms.MergeAction>.  
  
 Nella tabella seguente vengono descritti il significato e l'utilizzo tipico delle azioni di unione disponibili.  
  
|Valore di MergeAction|Descrizione|Utilizzo tipico|  
|---------------------------|-----------------|---------------------|  
|<xref:System.Windows.Forms.MergeAction>|\(Impostazione predefinita\) Aggiunge l'elemento di origine alla fine della raccolta dell'elemento di destinazione.|Aggiunta di voci di menu alla fine del menu quando parte del programma viene attivata.|  
|<xref:System.Windows.Forms.MergeAction>|Aggiunge l'elemento di origine alla raccolta dell'elemento di destinazione, nella posizione specificata dalla proprietà <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> impostata nell'elemento di origine.|Aggiunta di voci di menu al centro o all'inizio del menu quando parte del programma viene attivata.<br /><br /> Se il valore di <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> è uguale per entrambe le voci di menu, vengono aggiunte in ordine inverso.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> in modo appropriato per mantenere l'ordine originale.|  
|<xref:System.Windows.Forms.MergeAction>|Cerca una corrispondenza di testo o, se non la trova, utilizza il valore <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> e quindi sostituisce la voce di menu di destinazione corrispondente con la voce di menu di origine.|Sostituzione di una voce di menu di destinazione con una voce di menu di origine con lo stesso nome che ha una funzione diversa.|  
|<xref:System.Windows.Forms.MergeAction>|Cerca una corrispondenza di testo o, se non la trova, utilizza il valore <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> e quindi aggiunge tutti gli elementi a discesa dell'origine nella destinazione.|Compilazione di una struttura di menu che inserisce o aggiunge voci di menu in un sottomenu o rimuove voci di menu da un sottomenu.  Ad esempio, è possibile aggiungere una voce di menu da un figlio MDI a un menu **Salva con nome** del controllo <xref:System.Windows.Forms.MenuStrip> principale.<br /><br /> <xref:System.Windows.Forms.MergeAction> consente di spostarsi nella struttura di menu senza eseguire alcuna azione.  Fornisce un modo per valutare gli elementi successivi.|  
|<xref:System.Windows.Forms.MergeAction>|Cerca una corrispondenza di testo o, se non la trova, utilizza il valore <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> e quindi rimuove l'elemento dalla destinazione.|Rimozione di una voce di menu dal controllo <xref:System.Windows.Forms.MenuStrip> di destinazione.|  
  
## Unione manuale  
 Solo i controlli <xref:System.Windows.Forms.MenuStrip> partecipano all'unione manuale.  Per combinare gli elementi di altri controlli, ad esempio <xref:System.Windows.Forms.ToolStrip> e <xref:System.Windows.Forms.StatusStrip>, è necessario unirli manualmente, eseguendo una chiamata ai metodi <xref:System.Windows.Forms.ToolStripManager.Merge%2A> e <xref:System.Windows.Forms.ToolStripManager.RevertMerge%2A> nel codice secondo necessità.  
  
## Unione automatica  
 È possibile utilizzare l'unione automatica per le applicazioni MDI attivando il form di origine.  Per utilizzare un controllo <xref:System.Windows.Forms.MenuStrip> in un'applicazione MDI, impostare la proprietà <xref:System.Windows.Forms.Form.MainMenuStrip%2A> sul controllo <xref:System.Windows.Forms.MenuStrip> di destinazione in modo che le azioni di unione eseguite sul controllo <xref:System.Windows.Forms.MenuStrip> di origine si riflettano nel controllo <xref:System.Windows.Forms.MenuStrip> di destinazione.  
  
 È possibile generare l'unione automatica attivando il controllo <xref:System.Windows.Forms.MenuStrip> sull'origine MDI.  Dopo l'attivazione, il controllo <xref:System.Windows.Forms.MenuStrip> di origine viene unito nella destinazione MDI.  Quando un nuovo form diventa attivo, l'unione viene annullata sull'ultimo form e generata sul nuovo form.  È possibile controllare questo comportamento impostando la proprietà <xref:System.Windows.Forms.ToolStripItem.MergeAction%2A> secondo necessità in ogni controllo <xref:System.Windows.Forms.ToolStripItem> e impostando la proprietà <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> in ogni controllo <xref:System.Windows.Forms.MenuStrip>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripManager>   
 <xref:System.Windows.Forms.MenuStrip>   
 [Controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)   
 [Procedura: creare un elenco di finestre MDI con MenuStrip](../../../../docs/framework/winforms/controls/how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md)   
 [Procedura: impostare l'unione automatica dei menu per applicazioni MDI](../../../../docs/framework/winforms/controls/how-to-set-up-automatic-menu-merging-for-mdi-applications.md)