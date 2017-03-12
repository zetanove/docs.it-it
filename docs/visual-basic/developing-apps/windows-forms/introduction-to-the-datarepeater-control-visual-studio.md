---
title: "Introduction to the DataRepeater Control (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "repeating data"
  - "DataRepeater, overview"
  - "DataRepeater"
ms.assetid: 78a52a1d-65f0-4ecb-97ff-53bc114300c5
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Introduction to the DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> di Visual Basic Power Pack 1.1 è un contenitore scorrevole di controlli per la visualizzazione di dati ripetuti quali, ad esempio, le righe di una tabella di database.  Può essere utilizzato in alternativa al controllo <xref:System.Windows.Forms.DataGridView> quando è necessario maggiore controllo sul layout dei dati.  <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> "ripete" un gruppo di controlli correlati mediante la creazione di più istanze in una visualizzazione a scorrimento.  In tal modo gli utenti sono in grado di visualizzare più record contemporaneamente.  
  
## Panoramica  
 In fase di progettazione, il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> è composto da due sezioni.  La sezione esterna è il *riquadro di visualizzazione*, in cui in fase di esecuzione vengono visualizzati i dati di scorrimento.  La sezione interna \(superiore\), nota come *modello di elemento*, è il punto in cui vengono posizionati i controlli che verranno ripetuti in fase di esecuzione, in genere un controllo per ciascun campo dell'origine dati.  Le proprietà e i controlli del modello di elemento vengono incapsulati nella proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>.  
  
 In fase di esecuzione, la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> viene copiata in un oggetto <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> virtuale, utilizzato per visualizzare i dati quando ciascun record viene scorso nella visualizzazione.  È possibile personalizzare la visualizzazione di record singoli nell'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>, ad esempio, evidenziando un campo in base al valore in esso contenuto.  Per ulteriori informazioni, vedere la classe [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md).  
  
 Il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> viene generalmente utilizzato per visualizzare dati provenienti da una tabella di database o da un'altra origine dati associata.  In aggiunta a oggetti dati [!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado-md.md)], il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> è in grado di eseguire l'associazione a qualsiasi classe che implementi le interfacce <xref:System.Collections.IList> \(matrici incluse\), <xref:System.ComponentModel.IListSource>, <xref:System.ComponentModel.IBindingList> o <xref:System.ComponentModel.IBindingListView>.  
  
### Associazione dati  
 L'associazione dati si ottiene in genere trascinando campi dalla finestra **Origini dati** al controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Per ulteriori informazioni, vedere la classe [How to: Display Bound Data in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md).  
  
 Quando si utilizzano grandi quantità di dati, è possibile impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> su `True` per visualizzare un sottoinsieme dei dati disponibili.  In modalità virtuale è richiesta l'implementazione di una cache di dati da cui popolare <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> ed è necessario controllare in fase di esecuzione tutte le interazioni con la cache di dati.  Per ulteriori informazioni, vedere la classe [Virtual Mode in the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/virtual-mode-in-the-datarepeater-control-visual-studio.md).  
  
 È inoltre possibile visualizzare controlli non associati in un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Ad esempio, è possibile visualizzare un'immagine ripetuta su ciascun elemento.  Per ulteriori informazioni, vedere la classe [How to: Display Unbound Controls in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md).  
  
### Eventi  
 Gli eventi più importanti per il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> sono l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>, generato quando vengono scorsi nuovi elementi nella visualizzazione, e l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged>, generato quando viene selezionato un elemento.  È possibile utilizzare l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> per modificare l'aspetto dell'elemento.  Ad esempio, è possibile evidenziare i valori negativi.  Per accedere ai valori dei controlli quando viene selezionato un elemento, utilizzare l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndexChanged>.  
  
 Il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> espone tutti gli eventi di controllo standard nell'editor di codice.  Tuttavia, alcuni degli eventi non devono essere utilizzati.  Eventi relativi a tastiera e mouse quali `KeyDown`, `Click` e `MouseDown` non verranno generati in fase di esecuzione, perché il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> stesso non ha mai lo stato attivo.  
  
 L'oggetto <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> non espone eventi in fase di progettazione perché viene creato soltanto in fase di esecuzione.  Per gestire eventi relativi a tastiera e mouse, è possibile aggiungere un controllo <xref:System.Windows.Forms.Panel> a <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> in fase di progettazione e quindi gestire gli eventi per <xref:System.Windows.Forms.Panel>.  Per ulteriori informazioni, vedere la classe [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md).  
  
### Personalizzazioni  
 Esistono diversi modi per personalizzare l'aspetto e il comportamento del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, sia in fase di esecuzione che in fase di progettazione.  L'impostazione delle proprietà consente di modificare i colori, nascondere o modificare le intestazioni di elementi, modificare l'orientamento da verticale a orizzontale e così via.  Per ulteriori informazioni, vedere [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md), [How to: Display Item Headers in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md) e [How to: Change the Layout of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md).  
  
 Si noti che alcune proprietà sono valide per il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> stesso mentre altre sono valide soltanto per <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>.  Prima di impostare le proprietà, assicurarsi che sia stata selezionata la sezione corretta del controllo.  Per ulteriori informazioni, vedere la classe [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md).  
  
 Le altre personalizzazioni disponibili includono il controllo della possibilità di aggiungere o eliminare record, l'aggiunta di funzionalità di ricerca e la visualizzazione di dati correlati in formato master e dettaglio.  Per ulteriori informazioni, vedere [How to: Disable Adding and Deleting DataRepeater Items](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md), [How to: Search Data in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md) e [How to: Create a Master\/Detail Form by Using Two DataRepeater Controls](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md).  
  
## Vedere anche  
 [DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/datarepeater-control-visual-studio.md)   
 [Procedura dettagliata: visualizzazione di dati in un controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/walkthrough-displaying-data-in-a-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)