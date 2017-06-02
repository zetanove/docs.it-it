---
title: "Procedura: creare un&#39;interfaccia utente a pi&#249; riquadri con Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "interfaccia utente a riquadri multipli"
  - "SplitContainer (controllo) [Windows Form], utilizzo della finestra di progettazione"
  - "interfaccia utente, riquadri multipli"
ms.assetid: c3f9294d-a26c-4198-9242-f237f55f7573
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: creare un&#39;interfaccia utente a pi&#249; riquadri con Windows Form utilizzando la finestra di progettazione
La procedura descritta di seguito consente di creare un'interfaccia utente a più riquadri simile all'interfaccia di Microsoft Outlook, che include l'elenco cartelle, un riquadro per i messaggi e il riquadro di anteprima.  Questa disposizione viene ottenuta principalmente tramite l'ancoraggio dei controlli al form.  
  
 Per ancorare un controllo, è necessario determinare a quale bordo del contenitore padre deve essere fissato.  Se pertanto si imposta la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> su <xref:System.Windows.Forms.DockStyle>, il bordo destro del controllo verrà ancorato al bordo destro del controllo padre.  Il bordo ancorato del controllo viene inoltre ridimensionato in modo da combaciare con il bordo del controllo contenitore.  Per ulteriori informazioni sul funzionamento della proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A>, vedere [Procedura: ancorare i controlli in Windows Form](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md).  
  
 Questa procedura illustra la disposizione del controllo <xref:System.Windows.Forms.SplitContainer> e degli altri controlli sul form, ma non spiega come aggiungere le funzionalità necessarie affinché l'applicazione si comporti in modo analogo a Microsoft Outlook.  
  
 Per creare questa interfaccia utente, inserire i controlli all'interno del controllo <xref:System.Windows.Forms.SplitContainer>, che contiene il controllo <xref:System.Windows.Forms.TreeView> nel pannello sinistro.  Il pannello destro del controllo <xref:System.Windows.Forms.SplitContainer> contiene un secondo controllo <xref:System.Windows.Forms.SplitContainer> con un controllo <xref:System.Windows.Forms.ListView> sopra un controllo <xref:System.Windows.Forms.RichTextBox>.  Tali controlli <xref:System.Windows.Forms.SplitContainer> consentono di ridimensionare in modo indipendente gli altri controlli del form.  Le tecniche illustrate in questa procedura possono essere adattate in modo da realizzare interfacce utente personalizzate.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un'interfaccia utente nello stile di Outlook in fase di progettazione  
  
1.  Creare un nuovo progetto applicazione Windows.  Per informazioni dettagliate, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Trascinare un controllo <xref:System.Windows.Forms.SplitContainer> dalla **Casella degli strumenti** al form.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> su <xref:System.Windows.Forms.DockStyle>.  
  
3.  Trascinare un controllo <xref:System.Windows.Forms.TreeView> dalla **Casella degli strumenti** al pannello sinistro del controllo <xref:System.Windows.Forms.SplitContainer>.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> su <xref:System.Windows.Forms.DockStyle> facendo clic nel pannello sinistro dell'editor del valore, visualizzato quando si fa clic sulla freccia verso il basso.  
  
4.  Trascinare un altro controllo <xref:System.Windows.Forms.SplitContainer> dalla **Casella degli strumenti** al pannello destro del controllo <xref:System.Windows.Forms.SplitContainer> aggiunto al form.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> su <xref:System.Windows.Forms.DockStyle> e la proprietà <xref:System.Windows.Forms.SplitContainer.Orientation%2A> su <xref:System.Windows.Forms.Orientation>.  
  
5.  Trascinare un controllo <xref:System.Windows.Forms.ListView> dalla **Casella degli strumenti** al pannello superiore del secondo controllo <xref:System.Windows.Forms.SplitContainer> aggiunto al form.  Impostare la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> del controllo <xref:System.Windows.Forms.ListView> su <xref:System.Windows.Forms.DockStyle>.  
  
6.  Trascinare un controllo <xref:System.Windows.Forms.RichTextBox> dalla **Casella degli strumenti** al pannello inferiore del secondo controllo <xref:System.Windows.Forms.SplitContainer>.  Impostare la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> del controllo <xref:System.Windows.Forms.RichTextBox> su <xref:System.Windows.Forms.DockStyle>.  
  
     Se ora si preme F5 per eseguire l'applicazione, nel form viene visualizzata un'interfaccia in tre parti, analoga a quella di Microsoft Outlook.  
  
    > [!NOTE]
    >  Quando si posiziona il puntatore del mouse su una delle barre di divisione all'interno dei controlli <xref:System.Windows.Forms.SplitContainer>, è possibile ridimensionare le dimensioni interne.  
  
     A questo punto dello sviluppo l'applicazione dispone di un'interfaccia utente sofisticata.  Il passaggio successivo consisterà nella programmazione dell'applicazione stessa, ad esempio collegando il controllo <xref:System.Windows.Forms.TreeView> e i controlli <xref:System.Windows.Forms.ListView> a un'origine dati.  Per ulteriori informazioni sulla connessione dei controlli ai dati, vedere [Associazione dati e Windows Form](../../../../docs/framework/winforms/data-binding-and-windows-forms.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.SplitContainer>   
 [Controllo SplitContainer](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)