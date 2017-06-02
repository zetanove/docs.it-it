---
title: "Procedura dettagliata: creazione di un&#39;interfaccia di tipo Esplora risorse con i controlli ListView e TreeView utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "applicazioni di tipo Esplora risorse"
  - "applicazioni di tipo Esplora risorse, procedure dettagliate"
  - "ListView (controllo) [Windows Form], interfaccia di tipo Esplora risorse"
  - "ListView (controllo) [Windows Form], interfaccia di tipo Esplora risorse"
  - "ListView (controllo) [Windows Form], TreeView (controlli) utilizzati con"
  - "TreeView (controllo) [Windows Form], ListView (controlli) utilizzati con"
  - "TreeView (controllo) [Windows Form], utilizzo per interfaccia di tipo Esplora risorse"
ms.assetid: 9e5e7721-19e2-4890-b273-a43589fe99ff
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura dettagliata: creazione di un&#39;interfaccia di tipo Esplora risorse con i controlli ListView e TreeView utilizzando la finestra di progettazione
Uno dei vantaggi di Visual Studio consiste nella capacità di creare rapidamente applicazioni Windows Form a livello professionale.  Uno scenario comune consiste nella creazione di un'interfaccia utente \(UI, User Interface\) con i controlli <xref:System.Windows.Forms.ListView> e <xref:System.Windows.Forms.TreeView> simile alla funzionalità Esplora risorse dei sistemi operativi Windows.  Esplora risorse consente di visualizzare la struttura gerarchica dei file e delle cartelle di un computer.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare il form contenente i controlli ListView e TreeView  
  
1.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
2.  Nella finestra di dialogo **Nuovo progetto** attenersi alla seguente procedura:  
  
    1.  Nelle categorie scegliere **Visual Basic** o **Visual C\#**.  
  
    2.  Nell'elenco di modelli scegliere **Applicazione Windows Form**.  
  
3.  Scegliere **OK**.  Verrà creato un nuovo progetto Windows Form.  
  
4.  Aggiungere un controllo <xref:System.Windows.Forms.SplitContainer> nel form e impostare la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  
  
5.  Aggiungere un oggetto <xref:System.Windows.Forms.ImageList> denominato `imageList1` nel form e utilizzare la finestra Proprietà per aggiungere due immagini, l'immagine di una cartella e l'immagine di un documento, in quest'ordine.  
  
6.  Aggiungere un controllo <xref:System.Windows.Forms.TreeView> denominato `treeview1` nel form e posizionarlo sul lato sinistro del controllo <xref:System.Windows.Forms.SplitContainer>.  Nella finestra Proprietà per `treeView1` effettuare le operazioni seguenti:  
  
    1.  Impostare la proprietà <xref:System.Windows.Forms.Control.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  
  
    2.  Impostare la proprietà <xref:System.Windows.Forms.TreeView.ImageList%2A> su `imagelist1.`.  
  
7.  Aggiungere un controllo <xref:System.Windows.Forms.ListView> denominato `listView1` nel form e posizionarlo sul lato destro del controllo <xref:System.Windows.Forms.SplitContainer>.  Nella finestra Proprietà per `listview1` effettuare le operazioni seguenti:  
  
    1.  Impostare la proprietà <xref:System.Windows.Forms.Control.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  
  
    2.  Impostare la proprietà <xref:System.Windows.Forms.ListView.View%2A> su <xref:System.Windows.Forms.View>.  
  
    3.  Aprire l'editor della raccolta ColumnHeader facendo clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) nella proprietà <xref:System.Windows.Forms.ListView.Columns%2A>**.** Aggiungere tre colonne e impostare la proprietà <xref:System.Windows.Forms.ColumnHeader.Text%2A> su `Name`, `Type` e `Last Modified`, rispettivamente.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
    4.  Impostare la proprietà <xref:System.Windows.Forms.ListView.SmallImageList%2A> su `imageList1.`.  
  
8.  Implementare il codice per inserire nodi principali e secondari in <xref:System.Windows.Forms.TreeView>.  Aggiungere questo codice alla classe `Form1`.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#1)]  
  
9. Poiché nel codice precedente viene utilizzato lo spazio dei nomi System.IO, aggiungere l'istruzione using o import appropriata nella parte superiore del form.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#4)]  
  
10. Chiamare il metodo di configurazione del passaggio precedente nel costruttore del form o il metodo per la gestione dell'evento <xref:System.Windows.Forms.Form.Load>.  Aggiungere questo codice al costruttore del form.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#2)]  
  
11. Gestire l'evento <xref:System.Windows.Forms.TreeView.NodeMouseClick> per `treeview1` **e** implementare il codice per inserire in`listview1`il contenuto di un nodo quando viene fatto clic su di esso.  Aggiungere questo codice alla classe `Form1`.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#3)]  
  
     Se si utilizza C\#, assicurarsi che l'evento <xref:System.Windows.Forms.TreeView.NodeMouseClick> sia associato al relativo metodo di gestione degli eventi.  Aggiungere questo codice al costruttore del form.  
  
     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#5)]  
  
## Verifica dell'applicazione  
 È ora possibile verificare il form per assicurarsi che funzioni correttamente.  
  
#### Per eseguire il test del form  
  
-   ‎Premere F5 per eseguire l'applicazione.  
  
     Verrà visualizzato un form suddiviso contenente un controllo <xref:System.Windows.Forms.TreeView> che visualizza la directory di progetto nel lato sinistro e un controllo <xref:System.Windows.Forms.ListView> nel lato destro con tre colonne.  È possibile scorrere <xref:System.Windows.Forms.TreeView> selezionando i nodi di directory. In <xref:System.Windows.Forms.ListView> viene inserito il contenuto della directory selezionata.  
  
## Passaggi successivi  
 L'applicazione fornisce un esempio di come si possono utilizzare insieme i controlli <xref:System.Windows.Forms.TreeView> e <xref:System.Windows.Forms.ListView>.  Per ulteriori informazioni sui controlli, vedere gli argomenti seguenti:  
  
-   [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)  
  
-   [Procedura: aggiungere funzionalità di ricerca a un controllo ListView](../../../../docs/framework/winforms/controls/how-to-add-search-capabilities-to-a-listview-control.md)  
  
-   [Procedura: associare un menu di scelta rapida a un nodo di TreeView](../../../../docs/framework/winforms/controls/how-to-attach-a-shortcut-menu-to-a-treeview-node.md)  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListView>   
 <xref:System.Windows.Forms.TreeView>   
 [Controllo ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [Procedura: aggiungere e rimuovere nodi tramite il controllo TreeView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)   
 [Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [Procedura: aggiungere colonne al controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)