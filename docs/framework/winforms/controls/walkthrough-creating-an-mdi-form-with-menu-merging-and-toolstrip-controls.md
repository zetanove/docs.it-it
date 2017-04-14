---
title: "Procedura dettagliata: creazione di un form MDI con unione di menu e controlli ToolStrip | Microsoft Docs"
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
  - "MDI (form)"
  - "MDI (form), creazione"
  - "MDI (form), procedure dettagliate"
  - "MDI, creazione di form"
  - "form con interfaccia a documenti multipli"
  - "barre degli strumenti [Windows Form]"
  - "ToolStrip (controllo) [Windows Form]"
  - "ToolStripPanel (controllo) [Windows Form]"
ms.assetid: fbab4221-74af-42d0-bbf4-3c97f7b2e544
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura dettagliata: creazione di un form MDI con unione di menu e controlli ToolStrip
Lo spazio dei nomi <xref:System.Windows.Forms?displayProperty=fullName> supporta le applicazioni MDI \(Multiple Document Interface, interfaccia a documenti multipli\), mentre il controllo <xref:System.Windows.Forms.MenuStrip> supporta l'unione di menu.  I form MDI possono inoltre utilizzare i controlli <xref:System.Windows.Forms.ToolStrip>.  
  
 In questa procedura dettagliata viene illustrato come utilizzare i controlli <xref:System.Windows.Forms.ToolStripPanel> con un form MDI.  Il form supporta anche l'unione di menu con i menu figlio.  Nella procedura dettagliata verranno illustrate le seguenti attività:  
  
-   Creazione di un progetto Windows Form  
  
-   Creazione del menu principale del form.  Il nome effettivo del menu potrà variare  
  
-   Aggiunta del controllo <xref:System.Windows.Forms.ToolStripPanel> alla **Casella degli strumenti**  
  
-   Creazione di un form figlio  
  
-   Disposizione dei controlli <xref:System.Windows.Forms.ToolStripPanel> in base all'ordine Z  
  
 Al termine, si otterrà un form MDI che supporta l'unione dei menu e l'utilizzo di controlli <xref:System.Windows.Forms.ToolStrip> mobili.  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [Procedura: creare un form MDI con unione di menu e controlli ToolStrip](../../../../docs/framework/winforms/controls/how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Disporre di autorizzazioni sufficienti per creare ed eseguire progetti di applicazioni Windows Form sul computer sul quale è installato [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
## Creazione del progetto  
 Il primo passaggio indica come creare il progetto e impostare il form.  
  
#### Per creare il progetto  
  
1.  Creare un progetto Applicazione Windows denominato MdiForm.  
  
     Per ulteriori informazioni, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  In Progettazione Windows Form selezionare il form.  
  
3.  Nella finestra Proprietà impostare il valore della proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A> su `true`.  
  
## Creazione del menu principale  
 Il form MDI padre contiene il menu principale.  Il menu principale presenta un'unica voce di menu denominata **Finestra**,  che può essere utilizzata per creare form figlio.  Le voci di menu dei form figlio vengono unite nel menu principale.  
  
#### Per creare il menu principale  
  
1.  Dalla **Casella degli strumenti** trascinare un controllo <xref:System.Windows.Forms.MenuStrip> nel form.  
  
2.  Aggiungere un oggetto <xref:System.Windows.Forms.ToolStripMenuItem> al controllo <xref:System.Windows.Forms.MenuStrip> e denominarlo Finestra.  
  
3.  Fare clic sul controllo <xref:System.Windows.Forms.MenuStrip>.  
  
4.  Nella finestra Proprietà impostare il valore della proprietà <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> su `ToolStripMenuItem1`.  
  
5.  Aggiungere un elemento secondario alla voce di menu **Finestra** e denominarlo Nuova.  
  
6.  Nella finestra Proprietà fare clic su **Eventi**.  
  
7.  Fare doppio clic sull'evento <xref:System.Windows.Forms.ToolStripItem.Click>.  
  
     In Progettazione Windows Form verrà generato un gestore eventi per l'evento <xref:System.Windows.Forms.ToolStripItem.Click>.  
  
8.  Inserire il codice riportato di seguito nel gestore eventi.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.MdiForm#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.MdiForm#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/VB/Form1.vb#2)]  
  
## Aggiunta del controllo ToolStripPanel alla Casella degli strumenti  
 Quando si utilizzano controlli <xref:System.Windows.Forms.MenuStrip> con un form MDI è necessario disporre del controllo <xref:System.Windows.Forms.ToolStripPanel>.  Per compilare il form MDI in Progettazione Windows Form occorre aggiungere il controllo <xref:System.Windows.Forms.ToolStripPanel> alla **Casella degli strumenti**.  
  
#### Per aggiungere il controllo ToolStripPanel alla Casella degli strumenti  
  
1.  Aprire la **Casella degli strumenti** e scegliere la scheda **Tutti i Windows Form** per visualizzare i controlli Windows Form disponibili.  
  
2.  Fare clic con il pulsante destro del mouse per aprire il menu di scelta rapida, quindi scegliere **Scegli elementi**.  
  
3.  Nella finestra di dialogo **Scegli elementi della Casella degli strumenti** scorrere in basso nella colonna **Nome** finché non viene individuato **ToolStripPanel**.  
  
4.  Selezionare la casella di controllo accanto a **ToolStripPanel**, quindi scegliere **OK**.  
  
     Il controllo <xref:System.Windows.Forms.ToolStripPanel> verrà visualizzato nella **Casella degli strumenti**.  
  
## Creazione di un form figlio  
 In questa procedura verrà definita una classe separata per il form figlio con un proprio controllo <xref:System.Windows.Forms.MenuStrip>.  Le voci di menu di questo form vengono unite a quelle del form padre.  
  
#### Per definire un form figlio  
  
1.  Aggiungere al progetto un nuovo form denominato `ChildForm`.  
  
     Per ulteriori informazioni, vedere [How to: Add Windows Forms to a Project](http://msdn.microsoft.com/it-it/3d7bb25f-fd90-47cf-9378-fa0d764686c1).  
  
2.  Dalla **Casella degli strumenti** trascinare un controllo <xref:System.Windows.Forms.MenuStrip> nel form figlio.  
  
3.  Fare clic sul glifo dello smart tag del controllo <xref:System.Windows.Forms.MenuStrip> \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) e quindi selezionare **Modifica elementi**.  
  
4.  Nella finestra di dialogo **Editor della raccolta Items** aggiungere un nuovo oggetto <xref:System.Windows.Forms.ToolStripMenuItem> denominato ChildMenuItem al menu figlio.  
  
     Per ulteriori informazioni, vedere [ToolStrip Items Collection Editor](http://msdn.microsoft.com/it-it/e681f3ab-94ba-4b2b-ac64-1dfad46caa25).  
  
## Test del form  
  
#### Per eseguire il test del form  
  
1.  Premere F5 per compilare ed eseguire il form.  
  
2.  Scegliere **Nuovo** dal menu **Finestra**.  
  
     Nell'area client MDI del form verrà creato un nuovo form figlio.  Il menu del form figlio verrà unito al menu principale.  
  
3.  Chiudere il form figlio.  
  
     Il menu del form figlio verrà rimosso dal menu principale.  
  
4.  Fare clic più volte su **Nuova**.  
  
     I form figlio verranno elencati automaticamente all'interno del menu **Finestra** perché viene assegnata la proprietà <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> del controllo <xref:System.Windows.Forms.MenuStrip>.  
  
## Aggiunta del supporto ToolStrip  
 In questa procedura verranno aggiunti quattro controlli <xref:System.Windows.Forms.ToolStrip> al form MDI padre.  Ciascun controllo <xref:System.Windows.Forms.ToolStrip> verrà aggiunto all'interno di un controllo <xref:System.Windows.Forms.ToolStripPanel>, ancorato al bordo del form.  
  
#### Per aggiungere controlli ToolStrip al form MDI padre  
  
1.  Dalla **Casella degli strumenti** trascinare un controllo <xref:System.Windows.Forms.ToolStripPanel> nel form.  
  
2.  Dopo aver selezionato il controllo <xref:System.Windows.Forms.ToolStripPanel>, fare doppio clic sul controllo <xref:System.Windows.Forms.ToolStrip> nella **Casella degli strumenti**.  
  
     Verrà creato un controllo <xref:System.Windows.Forms.ToolStrip> nel controllo <xref:System.Windows.Forms.ToolStripPanel>.  
  
3.  Fare clic sul controllo <xref:System.Windows.Forms.ToolStripPanel>.  
  
4.  Nella finestra Proprietà impostare il valore della proprietà <xref:System.Windows.Forms.Control.Dock%2A> del controllo su <xref:System.Windows.Forms.DockStyle>.  
  
     Il controllo <xref:System.Windows.Forms.ToolStripPanel> verrà ancorato al bordo sinistro del form, al di sotto del menu principale.  L'area client MDI verrà ridimensionata per adattarla al controllo <xref:System.Windows.Forms.ToolStripPanel>.  
  
5.  Ripetere i passaggi da 1 a 4.  
  
     Ancorare il nuovo controllo <xref:System.Windows.Forms.ToolStripPanel> alla parte superiore del form.  
  
     Il controllo <xref:System.Windows.Forms.ToolStripPanel> verrà ancorato al di sotto del menu principale, ma a destra del primo controllo <xref:System.Windows.Forms.ToolStripPanel>.  Questo passaggio dimostra l'importanza dell'ordine Z per il corretto posizionamento dei controlli <xref:System.Windows.Forms.ToolStripPanel>.  
  
6.  Ripetere i passaggi da 1 a 4 per due o più controlli <xref:System.Windows.Forms.ToolStripPanel>.  
  
     Ancorare i nuovi controlli <xref:System.Windows.Forms.ToolStripPanel> al bordo destro e al bordo inferiore del form.  
  
## Disposizione dei controlli ToolStripPanel in base all'ordine Z  
 La posizione di un controllo <xref:System.Windows.Forms.ToolStripPanel> ancorato nel form MDI è determinata dalla posizione del controllo nell'ordine Z.  È possibile definire facilmente l'ordine Z dei controlli nella finestra Struttura documento.  
  
#### Per disporre i controlli ToolStripPanel in base all'ordine Z  
  
1.  Scegliere **Altre finestre** dal menu **Visualizza**, quindi fare clic su **Struttura documento**.  
  
     La disposizione dei controlli <xref:System.Windows.Forms.ToolStripPanel> ottenuta dalla procedura precedente non è quella standard,  perché l'ordine Z non è corretto.  Utilizzare la finestra Struttura documento per cambiare l'ordine Z dei controlli.  
  
2.  Nella finestra Struttura documento selezionare **ToolStripPanel4**.  
  
3.  Fare clic ripetutamente sulla freccia verso il basso finché **ToolStripPanel4** non sarà spostato alla fine dell'elenco.  
  
     Il controllo **ToolStripPanel4** verrà ancorato al bordo inferiore del form, al di sotto degli altri controlli.  
  
4.  Selezionare **ToolStripPanel2**.  
  
5.  Fare clic una sola volta sul pulsante della freccia in basso per collocare il controllo in terza posizione nell'elenco.  
  
     Il controllo **ToolStripPanel2** verrà ancorato al bordo superiore del form, al di sotto del menu principale e al di sopra degli altri controlli.  
  
6.  Selezionare alcuni controlli nella finestra **Struttura documento** e spostarli in posizioni diverse nell'ordine Z.  Notare l'effetto dell'ordine Z sul posizionamento dei controlli ancorati.  Premere CTRL\-Z o scegliere **Annulla** dal menu **Modifica** per annullare le modifiche.  
  
## Verifica  
  
#### Per eseguire il test del form  
  
1.  Premere F5 per compilare ed eseguire il form.  
  
2.  Fare clic sul riquadro di ridimensionamento di un controllo <xref:System.Windows.Forms.ToolStrip> e trascinare il controllo in posizioni diverse sul form.  
  
     È possibile trascinare un controllo <xref:System.Windows.Forms.ToolStrip> da un controllo <xref:System.Windows.Forms.ToolStripPanel> all'altro.  
  
## Passaggi successivi  
 In questa procedura dettagliata è stato creato un form MDI padre con controlli <xref:System.Windows.Forms.ToolStrip> e unione di menu.  È possibile utilizzare la famiglia di controlli <xref:System.Windows.Forms.ToolStrip> per molte altre finalità:  
  
-   Creazione di menu di scelta rapida per i controlli con la classe <xref:System.Windows.Forms.ContextMenuStrip>.  Per ulteriori informazioni, vedere [Cenni preliminari sul componente ContextMenu](../../../../docs/framework/winforms/controls/contextmenu-component-overview-windows-forms.md).  
  
-   Creazione di un form con un menu standard a compilazione automatica.  Per ulteriori informazioni, vedere [Procedura dettagliata: inserimento di voci di menu standard in un form](../../../../docs/framework/winforms/controls/walkthrough-providing-standard-menu-items-to-a-form.md).  
  
-   Attribuzione di un aspetto professionale ai controlli <xref:System.Windows.Forms.ToolStrip>.  Per ulteriori informazioni, vedere [Procedura: impostare il renderer ToolStrip per un'applicazione](../../../../docs/framework/winforms/controls/how-to-set-the-toolstrip-renderer-for-an-application.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 [Procedura: creare form padre MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [Procedura: creare form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [Procedura: inserire un MenuStrip in un menu a discesa MDI](../../../../docs/framework/winforms/controls/how-to-insert-a-menustrip-into-an-mdi-drop-down-menu-windows-forms.md)   
 [Controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)