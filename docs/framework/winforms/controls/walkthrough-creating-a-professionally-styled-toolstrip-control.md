---
title: "Procedura dettagliata: creazione di un controllo ToolStrip professionale | Microsoft Docs"
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
  - "barre degli strumenti [Windows Form], procedure dettagliate"
  - "ToolStrip (controllo) [Windows Form], creazione di controlli professionali"
  - "ToolStripProfessionalRenderer (classe) [Windows Form]"
  - "ToolStripRenderer (classe) [Windows Form]"
ms.assetid: b52339ae-f1d3-494e-996e-eb455614098a
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura dettagliata: creazione di un controllo ToolStrip professionale
Per assegnare un aspetto professionale ai controlli <xref:System.Windows.Forms.ToolStrip> dell'applicazione è possibile scrivere una classe personalizzata derivata dal tipo <xref:System.Windows.Forms.ToolStripProfessionalRenderer>.  
  
 In questa procedura dettagliata viene illustrato come utilizzare i controlli <xref:System.Windows.Forms.ToolStrip> per creare un controllo composito in grado di simulare il **riquadro di navigazione** fornito da Microsoft® Outlook®.  Nella procedura dettagliata verranno illustrate le seguenti attività:  
  
-   Creazione di un progetto di libreria di controlli Windows  
  
-   Progettazione del controllo StackView  
  
-   Implementazione di un renderer personalizzato  
  
 Al termine, si otterrà un controllo client personalizzato riutilizzabile con l'aspetto professionale di un controllo di Microsoft Office® XP.  
  
 Per copiare il codice nell'argomento corrente come un elenco singolo, vedere [Procedura: creare un controllo ToolStrip professionale](../../../../docs/framework/winforms/controls/how-to-create-a-professionally-styled-toolstrip-control.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Disporre di autorizzazioni sufficienti per creare ed eseguire progetti di applicazioni Windows Form sul computer sul quale è installato [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
## Creazione di un progetto di libreria di controlli Windows  
 Il primo passaggio consiste nella creazione di un progetto di libreria di controlli.  
  
#### Per creare il progetto di libreria di controlli  
  
1.  Creare un nuovo progetto Libreria di controlli Windows denominato `StackViewLibrary`.  
  
2.  In **Esplora soluzioni** eliminare il controllo predefinito del progetto rimuovendo il file di origine "UserControl1.cs" o "UserControl1.vb", a seconda del linguaggio scelto.  
  
     Per ulteriori informazioni, vedere [NIB:How to: Remove, Delete, and Exclude Items](http://msdn.microsoft.com/it-it/6dffdc86-29c8-4eff-bcd8-e3a0dd9e9a73).  
  
3.  Aggiungere un nuovo elemento <xref:System.Windows.Forms.UserControl> al progetto **StackViewLibrary**.  Assegnare al nuovo file di origine il nome di base `StackView`.  
  
## Progettazione del controllo StackView  
 `StackView` è un controllo composito con un unico controllo <xref:System.Windows.Forms.ToolStrip> figlio.  Per ulteriori informazioni sui controlli compositi, vedere [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md).  
  
#### Per progettare il controllo StackView  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.ToolStrip> dalla **Casella degli strumenti** all'area di progettazione.  
  
2.  Nella finestra **Proprietà** impostare le proprietà del controllo <xref:System.Windows.Forms.ToolStrip> in base alla tabella riportata di seguito.  
  
    |Proprietà|Valore|  
    |---------------|------------|  
    |Nome|`stackStrip`|  
    |CanOverflow|`false`|  
    |Dock|<xref:System.Windows.Forms.DockStyle>|  
    |Tipo di carattere|`Tahoma, 10pt, style=Bold`|  
    |GripStyle|<xref:System.Windows.Forms.ToolStripGripStyle>|  
    |LayoutStyle|<xref:System.Windows.Forms.ToolStripLayoutStyle>|  
    |Riempimento|`0, 7, 0, 0`|  
    |RenderMode|<xref:System.Windows.Forms.ToolStripRenderMode>|  
  
3.  In Progettazione Windows Form fare clic sul pulsante **Add** del controllo <xref:System.Windows.Forms.ToolStrip> e aggiungere un oggetto <xref:System.Windows.Forms.ToolStripButton> al controllo `stackStrip`.  
  
4.  Nella finestra **Proprietà** impostare le proprietà del controllo <xref:System.Windows.Forms.ToolStripButton> in base alla tabella riportata di seguito.  
  
    |Proprietà|Valore|  
    |---------------|------------|  
    |Nome|`mailStackButton`|  
    |CheckOnClick|true|  
    |CheckState|<xref:System.Windows.Forms.CheckState>|  
    |DisplayStyle|<xref:System.Windows.Forms.ToolStripItemDisplayStyle>|  
    |ImageAlign|<xref:System.Drawing.ContentAlignment>|  
    |ImageScaling|<xref:System.Windows.Forms.ToolStripItemImageScaling>|  
    |ImageTransparentColor|`238, 238, 238`|  
    |Margin|`0, 0, 0, 0`|  
    |Riempimento|`3, 3, 3, 3`|  
    |Text|Mail|  
    |TextAlign|<xref:System.Drawing.ContentAlignment>|  
  
5.  Ripetere il passaggio 7 per altri tre controlli <xref:System.Windows.Forms.ToolStripButton>.  
  
     Assegnare il nome ai controlli `calendarStackButton`, `contactsStackButton` e `tasksStackButton`.  Impostare il valore della proprietà <xref:System.Windows.Forms.Control.Text%2A> rispettivamente su Calendar, Contacts e Tasks.  
  
## Gestione degli eventi  
 Il comportamento corretto del controllo `StackView` dipende da due eventi.  Gestire l'evento <xref:System.Windows.Forms.UserControl.Load> per posizionare correttamente il controllo  e l'evento <xref:System.Windows.Forms.ToolStripItem.Click> per ciascun <xref:System.Windows.Forms.ToolStripButton> in modo da assegnare al controllo `StackView` un comportamento simile a quello del controllo <xref:System.Windows.Forms.RadioButton>.  
  
#### Per gestire gli eventi  
  
1.  In Progettazione Windows Form selezionare il controllo `StackView`.  
  
2.  Nella finestra **Proprietà** fare clic su **Eventi**.  
  
3.  Fare doppio clic sull'evento Load per generare il gestore eventi `StackView_Load`.  
  
4.  Nel gestore eventi `StackView_Load` copiare il codice riportato di seguito.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#3)]  
  
5.  In Progettazione Windows Form selezionare il controllo `mailStackButton`.  
  
6.  Nella finestra **Proprietà** fare clic su **Eventi**.  
  
7.  Fare doppio clic sull'evento Click.  
  
     In Progettazione Windows Form viene generato il gestore eventi `mailStackButton_Click`.  
  
8.  Rinominare il gestore eventi `mailStackButton_Click` in `stackButton_Click`.  
  
     Per ulteriori informazioni, vedere [How to: Rename an Identifier \(Visual Basic\)](http://msdn.microsoft.com/it-it/e5a5edf8-3dba-4119-81f4-fc2aba180e0c).  
  
9. Inserire il codice riportato di seguito nel gestore eventi `stackButton_Click`.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#4)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#4)]  
  
10. In Progettazione Windows Form selezionare il controllo `calendarStackButton`.  
  
11. Nella finestra **Proprietà**, impostare l'evento Clic sul gestore evento `stackButton_Click`.  
  
12. Ripetere i passaggi 10 e 11 per i controlli `contactsStackButton` e `tasksStackButton`.  
  
## Definizione delle icone  
 A ciascun pulsante `StackView` è associata un'icona.  Per comodità, ogni icona è rappresentata come una stringa Base 64, che deve essere deserializzata prima di poter essere utilizzata per la creazione di un oggetto <xref:System.Drawing.Bitmap>.  In un ambiente di produzione, i dati delle bitmap vengono memorizzati come risorsa e le icone vengono visualizzate in Progettazione Windows Form.  Per ulteriori informazioni, vedere [How to: Add Background Images to Windows Forms](http://msdn.microsoft.com/it-it/7a509ba2-055c-4ae6-b88a-54625c6d9aff).  
  
#### Per definire le icone  
  
1.  Nell'editor di codice inserire il codice riportato di seguito nella definizione della classe `StackView`.  In questo codice viene eseguita l'inizializzazione delle bitmap relative alle icone di <xref:System.Windows.Forms.ToolStripButton>.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#2)]  
  
2.  Aggiungere una chiamata al metodo `InitializeImages` nel costruttore della classe `StackView`.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]  
  
## Implementazione di un renderer personalizzato  
 È possibile personalizzare la maggior parte degli elementi del controllo `StackView` mediante l'implementazione di una classe che deriva da <xref:System.Windows.Forms.ToolStripRenderer>.  In questa procedura verrà implementata una classe <xref:System.Windows.Forms.ToolStripProfessionalRenderer> che consente di personalizzare il riquadro e di disegnare sfondi sfumati per i controlli <xref:System.Windows.Forms.ToolStripButton>.  
  
#### Per implementare un renderer personalizzato  
  
1.  Inserire il codice riportato di seguito nella definizione del controllo `StackView`.  
  
     Questo corrisponde alla definizione della classe `StackRenderer`, che esegue l'override dei metodi <xref:System.Windows.Forms.ToolStripRenderer.RenderGrip>, <xref:System.Windows.Forms.ToolStripRenderer.RenderToolStripBorder> e <xref:System.Windows.Forms.ToolStripRenderer.RenderButtonBackground> per produrre un aspetto personalizzato.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#10)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#10)]  
  
2.  Nel costruttore del controllo `StackView` creare una nuova istanza della classe `StackRenderer` e assegnarla alla proprietà <xref:System.Windows.Forms.ToolStrip.Renderer%2A> del controllo `stackStrip`.  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]  
  
## Test del controllo StackView  
 Il controllo `StackView` deriva dalla classe <xref:System.Windows.Forms.UserControl>.  È possibile quindi testare il controllo con **UserControl Test Container**.  Per ulteriori informazioni, vedere [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
#### Per testare il controllo StackView  
  
1.  Premere F5 per compilare il progetto e avviare **UserControl Test Container**.  
  
2.  Spostare il puntatore sui pulsanti del controllo `StackView`, quindi fare clic su un pulsante per visualizzare l'aspetto del relativo stato selezionato.  
  
## Passaggi successivi  
 In questa procedura dettagliata è stato creato un controllo client personalizzato riutilizzabile con l'aspetto professionale di un controllo di Office XP.  È possibile utilizzare la famiglia di controlli <xref:System.Windows.Forms.ToolStrip> per molte altre finalità:  
  
-   Creazione di menu di scelta rapida per i controlli con la classe <xref:System.Windows.Forms.ContextMenuStrip>.  Per ulteriori informazioni, vedere [Cenni preliminari sul componente ContextMenu](../../../../docs/framework/winforms/controls/contextmenu-component-overview-windows-forms.md).  
  
-   Creazione di un form con un menu standard a compilazione automatica.  Per ulteriori informazioni, vedere [Procedura dettagliata: inserimento di voci di menu standard in un form](../../../../docs/framework/winforms/controls/walkthrough-providing-standard-menu-items-to-a-form.md).  
  
-   Creazione di un form MDI \(Multiple Document Interface, interfaccia a documenti multipli\) con controlli <xref:System.Windows.Forms.ToolStrip> ancorati.  Per ulteriori informazioni, vedere [Procedura: creare un form MDI con unione di menu e controlli ToolStrip](../../../../docs/framework/winforms/controls/how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.StatusStrip>   
 [Controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)   
 [Procedura: specificare voci di menu standard in un form](../../../../docs/framework/winforms/controls/how-to-provide-standard-menu-items-to-a-form.md)