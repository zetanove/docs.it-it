---
title: "Procedura: impostare stili di righe alterne per il controllo DataGridView di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "dati [Windows Form], visualizzazione"
  - "DataGridView (controllo) [Windows Form], alternanza di stili delle righe"
  - "formati di tipo registro"
  - "righe, alterne"
  - "Windows Form, righe"
ms.assetid: 02373442-bf94-4470-9f8a-e44c4a9d5b88
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: impostare stili di righe alterne per il controllo DataGridView di Windows Form utilizzando la finestra di progettazione
I dati tabulari sono spesso presentati in un formato di tipo registro, con differenti colori di sfondo a righe alterne.  Questo formato rende più semplice l'individuazione delle celle appartenenti ad ogni riga, specialmente per le tabelle di grandi dimensioni con molte colonne.  
  
 Il controllo <xref:System.Windows.Forms.DataGridView> consente di specificare informazioni complete sullo stile delle righe alterne.  Oltre al colore di sfondo, per differenziare le righe alterne è possibile utilizzare caratteristiche di stile quali colore di primo piano e tipo di carattere.  Per ulteriori informazioni, vedere [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Definizione degli stili delle righe alterne  
  
1.  Selezionare il controllo <xref:System.Windows.Forms.DataGridView> nella finestra di progettazione.  
  
2.  Nella finestra **Proprietà** fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A>.  
  
3.  Nella finestra di dialogo **Generatore CellStyle** definire lo stile impostando le proprietà e utilizzare il riquadro **Anteprima** per verificare le scelte effettuate.  Gli stili specificati verranno utilizzati in maniera alternata per le righe visualizzate nel controllo, a partire dalla seconda.  
  
4.  Per definire gli stili per le rimanenti righe, ripetere i passaggi 2 e 3 utilizzando la proprietà <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A>.  
  
    > [!NOTE]
    >  Le celle vengono visualizzate utilizzando gli stili ereditati da più proprietà.  Per ulteriori informazioni sull'ereditarietà dello stile, vedere [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Stili della cella nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Formattazione e stile di base nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Utilizzo della finestra di progettazione con il controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/using-the-designer-with-the-windows-forms-datagridview-control.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)