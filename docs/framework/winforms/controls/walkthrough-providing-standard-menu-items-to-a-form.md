---
title: "Procedura dettagliata: inserimento di voci di menu standard in un form | Microsoft Docs"
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
  - "voci di menu, standard"
  - "StatusStrip (controllo) [Windows Form]"
  - "barre degli strumenti [Windows Form], procedure dettagliate"
  - "ToolStrip (controllo) [Windows Form]"
ms.assetid: dac37d98-589e-4d6d-9673-6437e8943122
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura dettagliata: inserimento di voci di menu standard in un form
È possibile inserire un menu standard nei form con il controllo <xref:System.Windows.Forms.MenuStrip>.  
  
 In questa procedura dettagliata verrà illustrato come utilizzare un controllo <xref:System.Windows.Forms.MenuStrip> per creare un menu standard.  Il form inoltre sarà in grado di fornire una risposta alla selezione di una voce di menu.  Nella procedura dettagliata verranno illustrate le seguenti attività:  
  
-   Creazione di un progetto Windows Form  
  
-   Creazione di un menu standard  
  
-   Creazione di un controllo <xref:System.Windows.Forms.StatusStrip>  
  
-   Gestione della selezione delle voci di menu.  
  
 Al termine, si disporrà di un form con un menu standard dove le voci di menu selezionate saranno visualizzate in un controllo <xref:System.Windows.Forms.StatusStrip>.  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [Procedura: specificare voci di menu standard in un form](../../../../docs/framework/winforms/controls/how-to-provide-standard-menu-items-to-a-form.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Disporre di autorizzazioni sufficienti per creare ed eseguire progetti di applicazioni Windows Form sul computer sul quale è installato [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
## Creazione del progetto  
 Il primo passaggio indica come creare il progetto e impostare il form.  
  
#### Per creare il progetto  
  
1.  Creare un progetto Applicazione Windows denominato StandardMenuForm.  
  
     Per ulteriori informazioni, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  In Progettazione Windows Form selezionare il form.  
  
## Creazione di un menu standard  
 In Progettazione Windows Form è possibile popolare automaticamente un controllo <xref:System.Windows.Forms.MenuStrip> con voci di menu standard.  
  
#### Per creare un menu standard  
  
1.  Dalla **Casella degli strumenti** trascinare un controllo <xref:System.Windows.Forms.MenuStrip> nel form.  
  
2.  Fare clic sul glifo dello smart tag del controllo <xref:System.Windows.Forms.MenuStrip> \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) e selezionare **Inserisci elementi standard**.  
  
     Il controllo <xref:System.Windows.Forms.MenuStrip> verrà popolato con le voci di menu standard.  
  
3.  Fare clic su **File** per visualizzare le relative voci di menu predefinite e le icone corrispondenti.  
  
## Creazione di un controllo StatusStrip  
 Utilizzare il controllo <xref:System.Windows.Forms.StatusStrip> per visualizzare lo stato delle applicazioni Windows Form.  Nell'esempio corrente, le voci di menu selezionate dall'utente vengono visualizzate in un controllo <xref:System.Windows.Forms.StatusStrip>.  
  
#### Per creare un controllo StatusStrip  
  
1.  Dalla **Casella degli strumenti** trascinare un controllo <xref:System.Windows.Forms.StatusStrip> nel form.  
  
     Il controllo <xref:System.Windows.Forms.StatusStrip> verrà ancorato automaticamente al bordo inferiore del form.  
  
2.  Fare clic sul pulsante a discesa del controllo <xref:System.Windows.Forms.StatusStrip> e scegliere **StatusLabel** per aggiungere un controllo <xref:System.Windows.Forms.ToolStripStatusLabel> al controllo <xref:System.Windows.Forms.StatusStrip>.  
  
## Gestione della selezione delle voci  
 Gestire l'evento <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked> in risposta alla selezione di una voce di menu.  
  
#### Per gestire la selezione delle voci  
  
1.  Scegliere la voce di menu **File** creata nella sezione Creazione di un menu standard.  
  
2.  Nella finestra **Proprietà** fare clic su **Eventi**.  
  
3.  Fare doppio clic sull'evento <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked>.  
  
     In Progettazione Windows Form verrà generato un gestore eventi per l'evento <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked>.  
  
4.  Inserire il codice riportato di seguito nel gestore eventi.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StandardMenu#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StandardMenu#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/VB/Form1.vb#3)]  
  
5.  Inserire la definizione del metodo di utilità `UpdateStatus` nel form.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StandardMenu#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StandardMenu#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/VB/Form1.vb#2)]  
  
## Verifica  
  
#### Per eseguire il test del form  
  
1.  Premere F5 per compilare ed eseguire il form.  
  
2.  Fare clic sulla voce di menu **File** per aprire il menu.  
  
3.  Fare clic su una delle voci del menu **File** per selezionarla.  
  
     Nel controllo <xref:System.Windows.Forms.StatusStrip> verrà visualizzata la voce selezionata.  
  
## Passaggi successivi  
 In questa procedura dettagliata è stato creato un form con un menu standard.  È possibile utilizzare la famiglia di controlli <xref:System.Windows.Forms.ToolStrip> per molte altre finalità:  
  
-   Creazione di menu di scelta rapida per i controlli con la classe <xref:System.Windows.Forms.ContextMenuStrip>.  Per ulteriori informazioni, vedere [Cenni preliminari sul componente ContextMenu](../../../../docs/framework/winforms/controls/contextmenu-component-overview-windows-forms.md).  
  
-   Creazione di un form MDI \(Multiple Document Interface, interfaccia a documenti multipli\) con controlli <xref:System.Windows.Forms.ToolStrip> ancorati.  Per ulteriori informazioni, vedere [Procedura dettagliata: creazione di un form MDI con unione di menu e controlli ToolStrip](../../../../docs/framework/winforms/controls/walkthrough-creating-an-mdi-form-with-menu-merging-and-toolstrip-controls.md).  
  
-   Attribuzione di un aspetto professionale ai controlli <xref:System.Windows.Forms.ToolStrip>.  Per ulteriori informazioni, vedere [Procedura: impostare il renderer ToolStrip per un'applicazione](../../../../docs/framework/winforms/controls/how-to-set-the-toolstrip-renderer-for-an-application.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 [Controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)