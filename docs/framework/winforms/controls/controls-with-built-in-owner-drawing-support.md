---
title: "Controlli con supporto incorporato per la creazione da parte del proprietario | Microsoft Docs"
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
  - "disegno, proprietario"
  - "disegno personalizzato"
  - "Modifica dell'aspetto dei controlli [Windows Form]"
  - "disegno personalizzato"
  - "creazione del proprietario"
ms.assetid: 3823d01e-9610-43e6-864d-99f9b7c2b351
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Controlli con supporto incorporato per la creazione da parte del proprietario
Il disegno personalizzato in Windows Form, che è noto anche come il disegno personalizzato, è una tecnica per modificare l'aspetto visivo di alcuni controlli.  
  
> [!NOTE]
>  La parola "controllo" in questo argomento viene utilizzata per indicare le classi che derivano da <xref:System.Windows.Forms.Control> o <xref:System.ComponentModel.Component>.  
  
 In genere, Windows gestisce il disegno automaticamente utilizzando le impostazioni delle proprietà, ad esempio <xref:System.Windows.Forms.Control.BackColor%2A> per determinare l'aspetto di un controllo. Con il disegno personalizzato, si usa il processo di disegno, la modifica di elementi che non sono disponibili tramite le proprietà dell'aspetto. Ad esempio, molti controlli consentono di impostare il colore del testo che viene visualizzato, ma sono limitati a un solo colore. Il disegno personalizzato consente di eseguire operazioni come la visualizzazione di parte del testo nella parte in rosso e nero.  
  
 In pratica, il disegno personalizzato è simile alla creazione di grafica in un form. Ad esempio, è possibile utilizzare metodi grafici in un gestore per il form <xref:System.Windows.Forms.Control.Paint> evento per emulare un `ListBox` controllo, ma si sarebbe necessario scrivere codice personalizzato per gestire tutte le interazioni utente. Con il disegno personalizzato, il controllo utilizza il codice per disegnare il relativo contenuto, ma in caso contrario mantiene tutte le funzionalità intrinseche. È possibile utilizzare metodi grafici per disegnare i singoli elementi nel controllo o per personalizzare alcuni aspetti di ogni elemento mentre si utilizza l'aspetto predefinito per gli altri aspetti di ogni elemento.  
  
## <a name="owner-drawing-in-windows-forms-controls"></a>Controlli di disegno personalizzato nei Windows Form  
 Per eseguire il disegno personalizzato nei controlli che la supportano, si sarà in genere impostare una proprietà e gestire uno o più eventi.  
  
 La maggior parte dei controlli che supportano il disegno dispone un `OwnerDraw` o `DrawMode` proprietà che indica se il controllo genererà l'evento disegno o relativi eventi quando il processo di generazione.  
  
 Controlli che non dispongono di un `OwnerDraw` o `DrawMode` proprietà includono il `DataGridView` controllo, che fornisce eventi di disegno che si verificano automaticamente, e `ToolStrip` controllo, che viene creato utilizzando una classe esterna per il rendering dotata di eventi relativi al disegno.  
  
 Esistono molti tipi diversi di eventi di disegno, ma si verifica un evento di disegno tipico per tracciare un singolo elemento all'interno di un controllo. Il gestore eventi riceve un `EventArgs` oggetto che contiene informazioni sull'elemento da disegnare e gli strumenti possa utilizzare per il disegno. Ad esempio, questo oggetto contiene in genere il numero di indice dell'elemento all'interno della raccolta padre, un <xref:System.Drawing.Rectangle> che indica i limiti di visualizzazione dell'elemento e un <xref:System.Drawing.Graphics> oggetto per la chiamata di metodi di disegno. Per alcuni eventi, il `EventArgs` oggetto fornisce informazioni aggiuntive sull'elemento e i metodi che è possibile chiamare per disegnare alcuni aspetti dell'elemento per impostazione predefinita, ad esempio lo sfondo o un rettangolo di attivazione.  
  
 Per creare un controllo riutilizzabile che contiene le personalizzazioni create dal proprietario, creare una nuova classe che deriva da una classe di controllo che supporta il disegno personalizzato. Anziché sulla gestione degli eventi di disegno, includere il codice del disegno personalizzato in sostituzioni per appropriato `On` *EventName* o più metodi nella nuova classe. Assicurarsi di chiamare la classe di base `On` *EventName* o più metodi in questo caso, in modo che gli utenti del controllo possono gestire gli eventi di disegno personalizzato e fornire personalizzazioni aggiuntive.  
  
 Il seguente di Windows Form controlli supportano il disegno personalizzato in tutte le versioni di .NET Framework:  
  
-   <xref:System.Windows.Forms.ListBox>  
  
-   <xref:System.Windows.Forms.ComboBox>  
  
-   <xref:System.Windows.Forms.MenuItem> (utilizzato da <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu>)  
  
-   <xref:System.Windows.Forms.TabControl>  
  
 I controlli seguenti supportano il disegno personalizzato solo in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]:  
  
-   <xref:System.Windows.Forms.ToolTip>  
  
-   <xref:System.Windows.Forms.ListView>  
  
-   <xref:System.Windows.Forms.TreeView>  
  
 I controlli seguenti supportano il disegno personalizzato e sono nuovi in [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]:  
  
-   <xref:System.Windows.Forms.DataGridView>  
  
-   <xref:System.Windows.Forms.ToolStrip>  
  
 Nelle sezioni seguenti forniscono dettagli aggiuntivi per ognuno di questi controlli.  
  
### <a name="listbox-and-combobox-controls"></a>Controlli ListBox e ComboBox  
 Il <xref:System.Windows.Forms.ListBox> e <xref:System.Windows.Forms.ComboBox> controlli consentono di disegnare singoli elementi nel controllo stessa dimensione o dimensioni variabili.  
  
> [!NOTE]
>  Sebbene il <xref:System.Windows.Forms.CheckedListBox> controllo derivato dal <xref:System.Windows.Forms.ListBox> controllo, non supporta il disegno personalizzato.  
  
 Per disegnare ciascun elemento con la stessa dimensione, impostare il `DrawMode` proprietà <xref:System.Windows.Forms.DrawMode> e gestire il `DrawItem` evento.  
  
 Per disegnare ciascun elemento con dimensioni diverse, impostare il `DrawMode` proprietà <xref:System.Windows.Forms.DrawMode> e gestire entrambi i `MeasureItem` e `DrawItem` gli eventi. Il `MeasureItem` evento consente di indicare le dimensioni di un elemento prima di `DrawItem` si verifica l'evento per quell'elemento.  
  
 Per ulteriori informazioni, inclusi esempi di codice, vedere gli argomenti seguenti:  
  
-   <xref:System.Windows.Forms.ListBox.DrawMode%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListBox.MeasureItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListBox.DrawItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ComboBox.DrawMode%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ComboBox.MeasureItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ComboBox.DrawItem?displayProperty=fullName>  
  
-   [Procedura: creare testo di dimensioni variabili in un controllo ComboBox](../../../../docs/framework/winforms/controls/how-to-create-variable-sized-text-in-a-combobox-control.md)  
  
### <a name="menuitem-component"></a>Componente MenuItem  
 Il <xref:System.Windows.Forms.MenuItem> componente rappresenta una singola voce di menu in un <xref:System.Windows.Forms.MainMenu> o <xref:System.Windows.Forms.ContextMenu> componente.  
  
 Per disegnare un <xref:System.Windows.Forms.MenuItem>, impostare il relativo `OwnerDraw` proprietà `true` e gestire il `DrawItem` evento. Per personalizzare la dimensione della voce di menu prima di `DrawItem` si verifica l'evento, gestire l'elemento `MeasureItem` evento.  
  
 Per ulteriori informazioni, inclusi esempi di codice, vedere gli argomenti di riferimento seguenti:  
  
-   <xref:System.Windows.Forms.MenuItem.OwnerDraw%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.MenuItem.DrawItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.MenuItem.MeasureItem?displayProperty=fullName>  
  
### <a name="tabcontrol-control"></a>Controllo TabControl  
 Il <xref:System.Windows.Forms.TabControl> controllo consente di disegnare singole schede nel controllo. Il disegno personalizzato influisce solo sulle schede. il <xref:System.Windows.Forms.TabPage> contenuto non è interessato.  
  
 Per disegnare ciascuna scheda un <xref:System.Windows.Forms.TabControl>, impostare il `DrawMode` proprietà <xref:System.Windows.Forms.TabDrawMode> e gestire il `DrawItem` evento. Questo evento si verifica una volta per ogni scheda solo quando la scheda è visibile nel controllo.  
  
 Per ulteriori informazioni, inclusi esempi di codice, vedere gli argomenti di riferimento seguenti:  
  
-   <xref:System.Windows.Forms.TabControl.DrawMode%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.TabControl.DrawItem?displayProperty=fullName>  
  
### <a name="tooltip-component"></a>Componente ToolTip  
 Il <xref:System.Windows.Forms.ToolTip> componente consente di disegnare la descrizione comandi quando viene visualizzato.  
  
 Per disegnare un <xref:System.Windows.Forms.ToolTip>, impostare il relativo `OwnerDraw` proprietà `true` e gestire relativo `Draw` evento. Per personalizzare le dimensioni del <xref:System.Windows.Forms.ToolTip> prima di `Draw` si verifica l'evento, gestire il `Popup` eventi e impostare il <xref:System.Windows.Forms.PopupEventArgs.ToolTipSize%2A> proprietà nel gestore eventi.  
  
 Per ulteriori informazioni, inclusi esempi di codice, vedere gli argomenti di riferimento seguenti:  
  
-   <xref:System.Windows.Forms.ToolTip.OwnerDraw%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ToolTip.Draw?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ToolTip.Popup?displayProperty=fullName>  
  
### <a name="listview-control"></a>Controllo ListView  
 Il <xref:System.Windows.Forms.ListView> controllo consente di disegnare singoli elementi, gli elementi secondari e intestazioni di colonna nel controllo.  
  
 Per abilitare il disegno personalizzato nel controllo, impostare il `OwnerDraw` proprietà `true`.  
  
 Per creare ogni elemento nel controllo, gestire il `DrawItem` evento.  
  
 Per disegnare ogni intestazione dell'elemento secondario o di colonna nel controllo quando la <xref:System.Windows.Forms.ListView.View%2A> è impostata su <xref:System.Windows.Forms.View>, gestire il `DrawSubItem` e `DrawColumnHeader` gli eventi.  
  
 Per ulteriori informazioni, inclusi esempi di codice, vedere gli argomenti di riferimento seguenti:  
  
-   <xref:System.Windows.Forms.ListView.OwnerDraw%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListView.DrawItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListView.DrawSubItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListView.DrawColumnHeader?displayProperty=fullName>  
  
### <a name="treeview-control"></a>Controllo TreeView  
 Il <xref:System.Windows.Forms.TreeView> controllo consente di disegnare singoli nodi nel controllo.  
  
 Per disegnare solo il testo visualizzato in ogni nodo, impostare il `DrawMode` proprietà <xref:System.Windows.Forms.TreeViewDrawMode> e gestire il `DrawNode` disegnare il testo dell'evento.  
  
 Per disegnare tutti gli elementi di ogni nodo, impostare il `DrawMode` proprietà <xref:System.Windows.Forms.TreeViewDrawMode> e gestire il `DrawNode` necessari, ad esempio testo, icone, caselle di controllo, segni più e meno e linee che collegano i nodi dell'evento.  
  
 Per ulteriori informazioni, inclusi esempi di codice, vedere gli argomenti di riferimento seguenti:  
  
-   <xref:System.Windows.Forms.TreeView.DrawMode%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.TreeView.DrawNode?displayProperty=fullName>  
  
### <a name="datagridview-control"></a>Controllo DataGridView  
 Il <xref:System.Windows.Forms.DataGridView> controllo consente di disegnare singole celle e righe nel controllo.  
  
 Per disegnare singole celle, gestire il `CellPainting` evento.  
  
 Per disegnare singole righe o elementi di righe, gestire uno o entrambi i `RowPrePaint` e `RowPostPaint` gli eventi. Il `RowPrePaint` evento si verifica prima che vengano generate le celle in una riga e `RowPostPaint` evento si verifica dopo che sono state generate le celle. È possibile gestire entrambi gli eventi e `CellPainting` evento per disegnare sfondo della riga, le singole celle e primo piano delle righe separatamente oppure fornire personalizzazioni specifiche in cui è necessario e utilizzare la visualizzazione predefinita per gli altri elementi della riga.  
  
 Per ulteriori informazioni, inclusi esempi di codice, vedere gli argomenti seguenti:  
  
-   <xref:System.Windows.Forms.DataGridView.CellPainting>  
  
-   <xref:System.Windows.Forms.DataGridView.RowPrePaint>  
  
-   <xref:System.Windows.Forms.DataGridView.RowPostPaint>  
  
-   [Procedura: personalizzare l'aspetto delle celle nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md)  
  
-   [Procedura: personalizzare l'aspetto delle righe nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/customize-the-appearance-of-rows-in-the-datagrid.md)  
  
### <a name="toolstrip-control"></a>Controllo ToolStrip  
 <xref:System.Windows.Forms.ToolStrip> e controlli derivati consentono di personalizzare qualsiasi aspetto dell'aspetto.  
  
 Per fornire il rendering personalizzato <xref:System.Windows.Forms.ToolStrip> i controlli, impostare il `Renderer` proprietà di un <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.ToolStripManager>, <xref:System.Windows.Forms.ToolStripPanel>, o <xref:System.Windows.Forms.ToolStripContentPanel> per un `ToolStripRenderer` dell'oggetto e gestire uno o più dei numerosi eventi di disegno forniti dalla `ToolStripRenderer` classe. In alternativa, impostare un `Renderer` proprietà a un'istanza della classe personalizzata derivata da `ToolStripRenderer`, <xref:System.Windows.Forms.ToolStripProfessionalRenderer>, o <xref:System.Windows.Forms.ToolStripSystemRenderer> che implementa o si esegue l'override specifico `On` *EventName* metodi.  
  
 Per ulteriori informazioni, inclusi esempi di codice, vedere gli argomenti seguenti:  
  
-   <xref:System.Windows.Forms.ToolStripRenderer>  
  
-   [Procedura: creare e impostare un Renderer personalizzato per il controllo ToolStrip in Windows Form](../../../../docs/framework/winforms/controls/create-and-set-a-custom-renderer-for-the-toolstrip-control-in-wf.md)  
  
-   [Procedura: un disegno personalizzato di un controllo ToolStrip](../../../../docs/framework/winforms/controls/how-to-custom-draw-a-toolstrip-control.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Controlli da usare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)