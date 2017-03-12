---
title: "Troubleshooting the DataRepeater Control (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, troubleshooting"
ms.assetid: c0ab9469-eced-4f52-aa18-4bd8dd4f1a9a
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Troubleshooting the DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo argomento vengono elencati i problemi che possono verificarsi durante l'utilizzo del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
## Mancata generazione di eventi di DataRepeater relativi a tastiera e mouse  
 Alcuni eventi del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, ad esempio quelli relativi a tastiera e mouse, non vengono generati.  Tale comportamento è stato definito in fase di progettazione.  Il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> stesso è un contenitore per oggetti <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> e non è accessibile in fase di esecuzione.  <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> non espone eventi in fase di progettazione.  Facendo clic su un elemento o premendo un tasto quando l'elemento ha lo stato attivo, pertanto, non viene generato alcun evento.  
  
 Fa eccezione il caso in cui la proprietà <xref:System.Windows.Forms.Control.Padding%2A> è impostata su un valore abbastanza grande da esporre i bordi del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  In tal caso, facendo clic sul margine esposto verranno generati eventi relativi al mouse.  
  
 Per risolvere il problema, aggiungere un controllo <xref:System.Windows.Forms.Panel> alla sezione <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, quindi aggiungere i controlli restanti a <xref:System.Windows.Forms.Panel>.  A questo punto è possibile aggiungere codice ai gestori eventi del controllo <xref:System.Windows.Forms.Panel> per eventi relativi a tastiera e mouse.  
  
## Controllo DataRepeater parzialmente nascosto dietro BindingNavigator  
 Quando si aggiunge per la prima volta un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> a un form e successivamente si aggiungono controlli con associazione a dati dalla finestra **Origini dati**, è possibile che il controllo <xref:System.Windows.Forms.BindingNavigator> venga visualizzato sopra il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Si tratta di un limite noto della finestra **Origini dati** ed è coerente con il comportamento di altri controlli, ad esempio il controllo <xref:System.Windows.Forms.DataGridView>.  
  
 È possibile spostare <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> più in basso rispetto al controllo <xref:System.Windows.Forms.BindingNavigator> in fase di progettazione o aggiungere codice simile a quello riportato di seguito nel gestore eventi `Load`.  
  
```vb#  
DataRepeater1.Top = ProductsBindingNavigator.Height  
```  
  
```c#  
dataRepeater1.Top = productsBindingNavigator.Height;  
```  
  
## Visualizzazione non corretta dei controlli in fase di esecuzione  
 In fase di esecuzione, è possibile che alcuni controlli in un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> non vengano visualizzati come previsto.  Il processo utilizzato per duplicare i controlli da <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> a <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> non è sempre in grado di determinare tutte le proprietà di tutti i controlli.  Se, ad esempio, un controllo <xref:System.Windows.Forms.ListBox> non associato viene aggiunto in fase di progettazione a un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> e la relativa raccolta <xref:System.Windows.Forms.ListBox.Items%2A> viene popolata con un elenco di stringhe, in fase di esecuzione l'oggetto <xref:System.Windows.Forms.ListBox> sarà vuoto.  Nel processo di duplicazione, infatti, non è possibile tenere conto della proprietà <xref:System.Windows.Forms.ListBox.Items%2A>.  
  
 Per correggere problemi di questo tipo è possibile ripristinare le proprietà mancanti nell'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemCloned> che si verifica al termine della duplicazione predefinita.  Nell'esempio riportato di seguito viene illustrato come ripristinare la raccolta <xref:System.Windows.Forms.ListBox.Items%2A> di un controllo <xref:System.Windows.Forms.ListBox> nel gestore eventi <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemCloned>.  
  
 [!code-cs[VbPowerPacksDataRepeaterItemCloned#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DataRepeaterItemClonedCS/ItemCloned.cs#1)]
 [!code-vb[VbPowerPacksDataRepeaterItemCloned#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/DataRepeaterItemCloned/ItemCloned.vb#1)]  
  
## Simbolo di selezione mancante nell'intestazione elemento  
 Quando si modifica la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> dell'intestazione elemento in un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, il simbolo di selezione può risultare nascosto a causa di alcune opzioni colore.  Ciò può verificarsi anche in caso di modifica della proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A>.  
  
 Non è possibile modificare il colore e le dimensioni del simbolo di selezione.  
  
-   Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> è impostata su <xref:System.Drawing.Color.White%2A>, il simbolo di selezione non sarà visibile quando un elemento viene selezionato per la prima volta.  
  
-   Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> è impostata su <xref:System.Drawing.Color.Black%2A>, il simbolo di selezione non sarà visibile quando viene selezionato un controllo, mentre il simbolo della matita non sarà visibile quando un controllo è in modalità di modifica.  
  
-   Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> è impostata su un valore minore di 11, i simboli degli indicatori non verranno visualizzati nell'intestazione elemento.  
  
 È possibile fornire un'intestazione elemento e un simbolo di selezione personalizzati utilizzando un controllo <xref:System.Windows.Forms.PictureBox> e monitorando la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem.IsCurrent%2A> di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> nell'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem.IsCurrent%2A>.  
  
## Vedere anche  
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [How to: Display Bound Data in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [How to: Display Unbound Controls in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [How to: Change the Layout of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)   
 [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [How to: Display Item Headers in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)   
 [How to: Disable Adding and Deleting DataRepeater Items](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md)   
 [How to: Search Data in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md)   
 [How to: Create a Master\/Detail Form by Using Two DataRepeater Controls](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)