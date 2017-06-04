---
title: "Considerazioni sul layout per l&#39;elemento WindowsFormsHost | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pixel indipendenti dal dispositivo"
  - "layout dinamico [interoperabilità WPF]"
  - "interoperabilità [WPF], Windows Form"
  - "Windows Form [WPF], interoperabilità con"
  - "Windows Form, interoperabilità WPF"
  - "WindowsFormsHost (considerazioni sul layout di elementi)"
ms.assetid: 3c574597-bbde-440f-95cc-01371f1a5d9d
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Considerazioni sul layout per l&#39;elemento WindowsFormsHost
In questo argomento viene illustrata la modalità di interazione dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> con il sistema di layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] supportano una logica diversa, benché analoga, per il ridimensionamento e il posizionamento degli elementi in un form o in una pagina.  Quando si crea un'interfaccia utente ibrida che ospita controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> integra i due schemi di layout.  
  
## Differenze di layout tra WPF e Windows Form  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza il layout indipendente dalla risoluzione.  Tutte le dimensioni di layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono specificate tramite *pixel indipendenti dal dispositivo*.  Un pixel indipendente dal dispositivo ha le dimensioni di un novantaseiesimo di pollice ed è indipendente dalla risoluzione, pertanto si ottengono risultati simili indipendentemente dal fatto che si esegua il rendering su un monitor a 72 dpi o su una stampante a 19.200 dpi.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] si basa inoltre sul *layout dinamico*.  In questo modo, la disposizione di un elemento dell'interfaccia utente su un form o una pagina avviene in base al contenuto, al contenitore di layout padre e alla dimensione dello schermo disponibile.  Con il layout dinamico il posizionamento è più semplice grazie alla regolazione automatica della dimensione e della posizione degli elementi dell'interfaccia utente nel momento in cui viene modificata la lunghezza delle stringhe che contengono.  
  
 Il layout in [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] è dipendente dal dispositivo e generalmente statico.  In genere, i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] vengono posizionati in modo assoluto su un form tramite dimensioni specificate in pixel hardware.  [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], tuttavia, supporta alcune funzionalità di layout dinamiche, come riepilogato nella tabella riportata di seguito.  
  
|Funzionalità di layout|Descrizione|  
|----------------------------|-----------------|  
|Ridimensionamento automatico|Alcuni controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] vengono ridimensionati automaticamente per visualizzare correttamente il contenuto.  Per ulteriori informazioni, vedere [Cenni preliminari sulla proprietà AutoSize](../../../../docs/framework/winforms/controls/autosize-property-overview.md).|  
|Ancoraggio|I controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] supportano il posizionamento e il ridimensionamento in base al contenitore padre.  Per ulteriori informazioni, vedere <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=fullName> e <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=fullName>.|  
|Ridimensionamento automatico|Controlli contenitore e relativi figli vengono ridimensionati automaticamente in base alla risoluzione del dispositivo di output o della dimensione, nei pixel, del tipo di carattere del contenitore predefinito.  Per ulteriori informazioni, vedere [Ridimensionamento automatico in Windows Form](../../../../docs/framework/winforms/automatic-scaling-in-windows-forms.md).|  
|Contenitori layout|I controlli <xref:System.Windows.Forms.FlowLayoutPanel> e <xref:System.Windows.Forms.TableLayoutPanel> dispongono i controlli figlio e si ridimensionano in base al contenuto.|  
  
## Limitazioni del layout  
 In genere, non è possibile ridimensionare e trasformare i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] nella misura possibile in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Nell'elenco riportato di seguito vengono descritte le limitazioni note quando l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> tenta di integrare il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato nel sistema di layout [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   In alcuni casi non è possibile ridimensionare i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] oppure è possibile ridimensionarli solo in base a dimensioni specifiche.  Ad esempio, un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.ComboBox> supporta una sola altezza definita dalla dimensione del carattere del controllo.  In un layout dinamico di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in cui è possibile allungare gli elementi in verticale, un controllo <xref:System.Windows.Forms.ComboBox> ospitato non verrà allungato nel modo previsto.  
  
-   Non è possibile ruotare o inclinare i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> genera l'evento <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> se si applica una trasformazione di inclinazione o rotazione.  Se non si gestisce l'evento <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError>, viene generato un oggetto <xref:System.InvalidOperationException>.  
  
-   Nella maggior parte dei casi i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non supportano il ridimensionamento proporzionale.  Anche se le dimensioni complessive del controllo vengono ridimensionate, i controlli figlio e gli elementi componente del controllo non possono essere ridimensionati nel modo previsto.  Questa limitazione dipende dalla modalità in cui ogni controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] supporta il ridimensionamento.  In aggiunta, non è possibile ridimensionare i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] fino a una dimensione di 0 pixel.  
  
-   I controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] supportano il ridimensionamento automatico in cui il form e i relativi controlli vengono automaticamente ridimensionati in base alla dimensione del carattere.  In un'interfaccia utente di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la modifica della dimensione del carattere non causa il ridimensionamento dell'intero layout, benché sia possibile che vengano ridimensionati singoli elementi.  
  
### Ordine Z  
 In un'interfaccia utente di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è possibile modificare l'ordine Z degli elementi per controllare il comportamento di sovrapposizione.  Un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato viene tracciato in un elemento HWND separato, in modo che venga disegnato sempre sopra elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Anche un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato viene disegnato sopra qualsiasi elemento <xref:System.Windows.Documents.Adorner>.  
  
## Comportamento di layout  
 Nelle sezioni riportate di seguito vengono descritti aspetti specifici del comportamento di layout quando i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] vengono ospitati in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
### Ridimensionamento, conversione di unità e indipendenza dal dispositivo  
 Le operazioni eseguite mediante l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> che implicano dimensioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] interessano due sistemi di coordinate: pixel indipendenti dal dispositivo per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e pixel hardware per [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  È pertanto necessario applicare le corrette conversioni di unità e ridimensionamento per ottenere un layout coerente.  
  
 La conversione tra sistemi di coordinate dipende dalla risoluzione del dispositivo corrente e da qualsiasi trasformazione di layout o rendering applicata all'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> o ai relativi predecessori.  
  
 Se il dispositivo di output è a 96 dpi e non è stato applicato alcun ridimensionamento all'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>, un pixel indipendente dal dispositivo equivale a un pixel hardware.  
  
 Tutti gli altri casi richiedono il ridimensionamento del sistema di coordinate.  Il controllo ospitato non viene ridimensionato.  Al contrario, l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> tenta di ridimensionare il controllo ospitato e tutti i relativi controlli figlio.  Poiché [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non offre il supporto completo del ridimensionamento, l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> viene ridimensionato secondo il grado supportato da determinati controlli.  
  
 Eseguire l'override del metodo <xref:System.Windows.Forms.Integration.WindowsFormsHost.ScaleChild%2A> per fornire il comportamento di ridimensionamento personalizzato per il controllo [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)] ospitato.  
  
 In aggiunta al ridimensionamento, l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> gestisce casi di arrotondamento e overflow come illustrato nella tabella riportata di seguito.  
  
|Problema di conversione|Descrizione|  
|-----------------------------|-----------------|  
|Arrotondamento|Le dimensioni dei pixel indipendenti dal dispositivo di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono specificate come `double` e le dimensioni dei pixel hardware di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] sono specificate come `int`.  Nei casi in cui le dimensioni basate su `double` vengono convertite in dimensioni basate su `int`, l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> utilizza l'arrotondamento standard, in modo che i valori frazionari minori di 0,5 siano arrotondati per difetto a 0.|  
|Overflow|Quando viene eseguita la conversione di valori `double` in valori `int` tramite l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>, è possibile l'overflow.  I valori maggiori di <xref:System.Int32.MaxValue> vengono impostati su <xref:System.Int32.MaxValue>.|  
  
### Proprietà relative al layout  
 Le proprietà che controllano il comportamento di layout nei controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e negli elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono mappate in modo appropriato dall'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  Per ulteriori informazioni, vedere [Mapping di proprietà di Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md).  
  
### Modifiche del layout nel controllo ospitato  
 Le modifiche del layout nel controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato vengono propagate a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per avviare gli aggiornamenti del layout.  Il metodo <xref:System.Windows.UIElement.InvalidateMeasure%2A> in <xref:System.Windows.Forms.Integration.WindowsFormsHost> garantisce che le modifiche del layout nel controllo ospitato attivino l'esecuzione del motore di layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
### Controlli Windows Form con ridimensionamento continuo  
 I controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che supportano il ridimensionamento continuo interagiscono in modo completo con il sistema di layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> utilizza i metodi <xref:System.Windows.FrameworkElement.MeasureOverride%2A> e <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> nel modo consueto per ridimensionare e disporre il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato.  
  
### Algoritmo di ridimensionamento  
 La procedura descritta di seguito viene utilizzata dall'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> per ridimensionare il controllo ospitato:  
  
1.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> esegue l'overriding dei metodi <xref:System.Windows.FrameworkElement.MeasureOverride%2A> e <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>.  
  
2.  Per determinare la dimensione del controllo ospitato, il metodo <xref:System.Windows.FrameworkElement.MeasureOverride%2A> chiama il metodo <xref:System.Windows.Forms.Control.GetPreferredSize%2A> del controllo ospitato con un vincolo convertito dal vincolo passato al metodo <xref:System.Windows.FrameworkElement.MeasureOverride%2A>.  
  
3.  Il metodo <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> tenta di impostare il controllo ospitato sul vincolo di dimensione specificato.  
  
4.  Se la proprietà <xref:System.Windows.Forms.Control.Size%2A> del controllo ospitato corrisponde al vincolo specificato, il controllo ospitato viene ridimensionato in base al vincolo.  
  
 Se la proprietà <xref:System.Windows.Forms.Control.Size%2A> non corrisponde al vincolo specificato, il controllo ospitato non supporta il ridimensionamento continuo.  Il controllo <xref:System.Windows.Forms.MonthCalendar>, ad esempio, consente unicamente dimensioni discrete.  Le dimensioni consentite per tale controllo sono costituite da numeri interi \(che rappresentano il numero dei mesi\) per l'altezza e per la larghezza.  In casi come questo, l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> si comporta nel modo seguente:  
  
-   Se la proprietà <xref:System.Windows.Forms.Control.Size%2A> restituisce una dimensione maggiore del vincolo specificato, l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> ritaglia il controllo ospitato.  Altezza e larghezza sono gestite separatamente, pertanto il controllo ospitato può essere ritagliato in entrambe le direzioni.  
  
-   Se la proprietà <xref:System.Windows.Forms.Control.Size%2A> restituisce una dimensione minore del vincolo specificato, <xref:System.Windows.Forms.Integration.WindowsFormsHost> accetta questo valore e restituisce il valore al sistema di layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Procedura dettagliata: disposizione di controlli Windows Form in WPF](../../../../docs/framework/wpf/advanced/walkthrough-arranging-windows-forms-controls-in-wpf.md)   
 [Disposizione dei controlli Windows Form in WPF](http://go.microsoft.com/fwlink/?LinkID=159971)   
 [Mapping di proprietà di Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)   
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)