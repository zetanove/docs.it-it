---
title: "Procedura: impostare formati di dati e stili di cella predefiniti per il controllo DataGridView di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "celle, impostazione di stili"
  - "dati [Windows Form], impostazione di formati"
  - "formati di dati"
  - "DataGridView (controllo) [Windows Form], stili della cella"
ms.assetid: fc6da49f-8942-41da-b49f-b2afc38cc656
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: impostare formati di dati e stili di cella predefiniti per il controllo DataGridView di Windows Form utilizzando la finestra di progettazione
Per creare un effetto di tipo registro, il controllo <xref:System.Windows.Forms.DataGridView> consente di specificare gli stili predefiniti e i formati di dati delle celle per l'intero controllo, per specifiche colonne, per intestazioni di righe e colonne e per le righe alterne.  Gli stili predefiniti impostati per le colonne e per le righe alterne hanno la priorità sugli stili predefiniti impostati per l'intero controllo.  Inoltre, gli stili impostati nel codice per singole righe e celle hanno la priorità sugli stili predefiniti.  
  
 Per ulteriori informazioni sugli stili delle celle, vedere [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  Per impostare gli stili per le righe alterne, vedere [Procedura: impostare stili di righe alterne per il controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/set-alternating-row-styles-for-the-datagrid-using-the-designer.md).  
  
 È possibili impostare gli stili anche utilizzando la proprietà <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> per controllare tutte le righe che verranno aggiunte al controllo.  Per ulteriori informazioni sul modello delle righe, vedere [Procedura: utilizzare il modello di riga personalizzare le righe nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/use-the-row-template-to-customize-rows-in-the-datagrid.md).  
  
 Nelle seguenti procedure è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per impostare gli stili predefiniti per tutte le celle del controllo  
  
1.  Selezionare il controllo <xref:System.Windows.Forms.DataGridView> nella finestra di progettazione.  
  
2.  Nella finestra **Proprietà**, fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A>, <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> o <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A>.  Verrà visualizzata la finestra di dialogo **Generatore CellStyle**.  
  
3.  Definire lo stile impostando le proprietà e utilizzando il pannello **Anteprima** per confermare le scelte.  
  
> [!NOTE]
>  Se sono attivati stili di visualizzazione, alle intestazioni di riga e colonna \(ad eccezione della proprietà <xref:System.Windows.Forms.DataGridView.TopLeftHeaderCell%2A>\) viene applicato automaticamente lo stile del tema corrente e viene eseguito l'override dei valori delle proprietà <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> e <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A>.  
>   
>  Nella finestra di progettazione è possibile impostare gli stili delle celle per più controlli <xref:System.Windows.Forms.DataGridView> selezionati, ma solo se prevedono valori identici per la proprietà dello stile delle celle da modificare.  Se gli stili delle celle impostati per la proprietà differiscono, la finestra **Proprietà** del **Generatore CellStyle** sarà vuota.  
  
### Per impostare gli stili predefiniti per le celle in singole colonne  
  
1.  Fare clic con il pulsante destro del mouse sul controllo <xref:System.Windows.Forms.DataGridView> nella finestra di progettazione e scegliere **Modifica colonne**.  
  
2.  Selezionare una colonna dall'elenco **Colonne selezionate**.  
  
3.  Nella griglia **Proprietà colonne**, fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A>.  Verrà visualizzata la finestra di dialogo **Generatore CellStyle**.  
  
4.  Definire lo stile impostando le proprietà e utilizzando il pannello **Anteprima** per confermare le scelte.  
  
### Per impostare il formato dei dati nelle celle  
  
1.  Utilizzare una delle precedenti procedure per visualizzare una finestra di dialogo **Generatore CellStyle** relativa a una proprietà per lo stile predefinito delle celle.  
  
2.  Nella finestra di dialogo **Generatore CellStyle**, fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A>.  Verrà visualizzata la finestra di dialogo **Stringa di formato**.  
  
3.  Selezionare un tipo di formato, quindi modificare i dettagli del tipo, ad esempio il numero delle posizioni decimali da visualizzare, utilizzando la casella **Esempio** per confermare le scelte.  
  
4.  Se il controllo <xref:System.Windows.Forms.DataGridView> deve essere associato a un'origine dati che probabilmente contiene valori null, compilare la casella di testo **Valore null**.  Tale valore viene visualizzato quando il valore della cella è uguale a un riferimento null \(`Nothing` in Visual Basic\) o <xref:System.DBNull.Value?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A?displayProperty=fullName>   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Procedura: impostare stili di righe alterne per il controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/set-alternating-row-styles-for-the-datagrid-using-the-designer.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)