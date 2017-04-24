---
title: "Risoluzione dei problemi relativi ad applicazioni ibride | Microsoft Docs"
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
  - "applicazioni ibride [interoperabilità WPF]"
  - "interoperabilità [WPF], Windows Form"
  - "cicli di messaggi [WPF]"
  - "sovrapposizione di controlli"
  - "Windows Form [WPF], interoperabilità con"
  - "Windows Form, interoperabilità WPF"
ms.assetid: f440c23f-fa5d-4d5a-852f-ba61150e6405
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# Risoluzione dei problemi relativi ad applicazioni ibride
<a name="introduction"></a> In questo argomento vengono elencati alcuni problemi comuni che possono verificarsi durante la creazione di applicazioni che utilizzano tecnologie sia [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], sia [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
   
  
<a name="overlapping_controls"></a>   
## Sovrapposizione di controlli  
 I controlli potrebbero sovrapporsi in maniera imprevista.  [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] utilizza un HWND per ciascun controllo.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza un HWND per tutto il contenuto di una pagina.  Questa differenza di implementazione provoca comportamenti di sovrapposizione imprevisti.  
  
 Un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene visualizzato sempre al di sopra del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitato in un controllo <xref:System.Windows.Forms.Integration.ElementHost> viene visualizzato in corrispondenza dell'ordine Z del controllo <xref:System.Windows.Forms.Integration.ElementHost>.  È possibile far coincidere i controlli <xref:System.Windows.Forms.Integration.ElementHost>, ma il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitato non consente la combinazione o l'interazione.  
  
<a name="child_property"></a>   
## Proprietà Child  
 Le classi <xref:System.Windows.Forms.Integration.WindowsFormsHost> e <xref:System.Windows.Forms.Integration.ElementHost> possono ospitare solo un singolo controllo o elemento figlio.  Per ospitarne più di uno, è necessario utilizzare un contenitore come contenuto figlio.  Ad esempio, è possibile aggiungere controlli pulsante e casella di controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] in un controllo <xref:System.Windows.Forms.Panel?displayProperty=fullName> e assegnare quindi il pannello a una proprietà <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A> del controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  Tuttavia, non è possibile aggiungere controlli pulsante e casella di controllo separatamente allo stesso controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
<a name="scaling"></a>   
## Ridimensionamento  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] sono disponibili modelli di ridimensionamento diversi.  Alcune trasformazioni di ridimensionamento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] hanno valore per i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], ma non tutte.  Ad esempio, è possibile ridimensionare un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] fino a 0, ma se si tenta di riportare lo stesso controllo su un valore di ridimensionamento diverso da 0, le dimensioni del controllo rimarranno invariate.  Per ulteriori informazioni, vedere [Considerazioni sul layout per l'elemento WindowsFormsHost](../../../../docs/framework/wpf/advanced/layout-considerations-for-the-windowsformshost-element.md).  
  
<a name="adapter"></a>   
## Adattatore  
 L'utilizzo delle classi <xref:System.Windows.Forms.Integration.WindowsFormsHost> e <xref:System.Windows.Forms.Integration.ElementHost> può creare confusione, perché tali classi includono un contenitore nascosto.  Entrambe le classi <xref:System.Windows.Forms.Integration.WindowsFormsHost> e <xref:System.Windows.Forms.Integration.ElementHost> dispongono di un contenitore nascosto, chiamato*adattatore* e utilizzato per ospitare il contenuto.  Per l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>, l'adattatore deriva dalla classe <xref:System.Windows.Forms.ContainerControl?displayProperty=fullName>.  Per il controllo <xref:System.Windows.Forms.Integration.ElementHost>, l'adattatore deriva dall'elemento <xref:System.Windows.Controls.DockPanel>.  I riferimenti all'adattatore presenti in altri argomenti sull'interoperabilità alludono a tale contenitore.  
  
<a name="nesting"></a>   
## Annidamento  
 L'annidamento di un elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> all'interno di un controllo <xref:System.Windows.Forms.Integration.ElementHost> non è supportato.  Parimenti, non è supportato l'annidamento di un controllo <xref:System.Windows.Forms.Integration.ElementHost> all'interno di un elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
<a name="focus"></a>   
## Focus  
 Lo stato attivo funziona in maniera diversa in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]; pertanto, in un'applicazione ibrida possono verificarsi dei problemi in relazione allo stato attivo.  Ad esempio, se in un elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> è impostato lo stato attivo, una riduzione a icona o un ripristino della pagina oppure la visualizzazione di una finestra di dialogo modale potrebbero determinare la perdita dello stato attivo all'interno dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> ha ancora lo stato attivo, ma il controllo all'interno potrebbe averlo perso.  
  
 Lo stato attivo influisce anche sulla convalida dati.  La convalida funziona all'interno di un elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>, ma non quando si esce dall'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>, né tra due elementi <xref:System.Windows.Forms.Integration.WindowsFormsHost> diversi.  
  
<a name="property_mapping"></a>   
## Mapping di proprietà  
 Alcuni mapping di proprietà richiedono un'interpretazione estensiva per integrare differenti implementazioni tra le tecnologie [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  I mapping di proprietà consentono al codice di rispondere alle modifiche apportate ai tipi di carattere, ai colori e ad altre proprietà.  In generale, i mapping di proprietà funzionano rimanendo in ascolto di eventi *Property*Changed o chiamate On*Property*Changed e impostando le proprietà adeguate sul controllo figlio o sul relativo adattatore.  Per ulteriori informazioni, vedere [Mapping di proprietà di Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md).  
  
<a name="layoutrelated_properties_on_hosted_content"></a>   
## Proprietà relative al layout nel contenuto ospitato  
 Quando viene assegnata la proprietà <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A?displayProperty=fullName> o <xref:System.Windows.Forms.Integration.ElementHost.Child%2A?displayProperty=fullName>, diverse proprietà del contenuto ospitato relative al layout vengono impostate automaticamente.  La modifica di queste proprietà di contenuto può determinare comportamenti di layout imprevisti.  
  
 Il contenuto ospitato è ancorato in modo da riempire gli elementi padre <xref:System.Windows.Forms.Integration.WindowsFormsHost> e <xref:System.Windows.Forms.Integration.ElementHost>.  Al fine di abilitare tale comportamento di riempimento, durante l'impostazione della proprietà figlio vengono impostate varie proprietà.  Nella tabella seguente sono indicate le proprietà del contenuto impostate dalle classi <xref:System.Windows.Forms.Integration.ElementHost> e <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
|Classe host|Proprietà di contenuto|  
|-----------------|----------------------------|  
|<xref:System.Windows.Forms.Integration.ElementHost>|<xref:System.Windows.FrameworkElement.Height%2A><br /><br /> <xref:System.Windows.FrameworkElement.Width%2A><br /><br /> <xref:System.Windows.FrameworkElement.Margin%2A><br /><br /> <xref:System.Windows.FrameworkElement.VerticalAlignment%2A><br /><br /> <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>|  
|<xref:System.Windows.Forms.Integration.WindowsFormsHost>|<xref:System.Windows.Forms.Control.Margin%2A><br /><br /> <xref:System.Windows.Forms.Control.Dock%2A><br /><br /> <xref:System.Windows.Forms.Control.AutoSize%2A><br /><br /> <xref:System.Windows.Forms.Control.Location%2A><br /><br /> <xref:System.Windows.Forms.Control.MaximumSize%2A>|  
  
 Non impostare queste proprietà direttamente nel contenuto ospitato.  Per ulteriori informazioni, vedere [Considerazioni sul layout per l'elemento WindowsFormsHost](../../../../docs/framework/wpf/advanced/layout-considerations-for-the-windowsformshost-element.md).  
  
<a name="navigation_applications"></a>   
## Applicazioni per la navigazione  
 Talvolta le applicazioni per la navigazione non garantiscono che lo stato dell'utente sarà mantenuto.  L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> ricrea i propri controlli se utilizzato in un'applicazione per la navigazione.  I controlli figlio vengono ricreati quando l'utente si sposta dalla pagina che ospita l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> e vi ritorna in un secondo momento.  Qualsiasi contenuto immesso dall'utente andrà perduto.  
  
<a name="message_loop_interoperation"></a>   
## Interoperabilità del ciclo di messaggi  
 I messaggi potrebbero essere elaborati in maniera diversa da quella prevista , quando si utilizzano i relativi cicli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  Il metodo <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> viene chiamato dal costruttore <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  Tale metodo aggiunge un filtro messaggi al ciclo di messaggi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Questo filtro chiama il metodo <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=fullName> nel caso in cui la destinazione del messaggio fosse <xref:System.Windows.Forms.Control?displayProperty=fullName> e quindi converte e invia il messaggio.  
  
 Se si visualizza un oggetto <xref:System.Windows.Window> in un ciclo di messaggi [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] con <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName>, sarà impossibile digitare qualsiasi carattere a meno che non si chiami il metodo <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A>.  Il metodo <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> accetta <xref:System.Windows.Window> e aggiunge un oggetto <xref:System.Windows.Forms.IMessageFilter?displayProperty=fullName> che reindirizza i messaggi relativi alla chiave al ciclo di messaggi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Per ulteriori informazioni, vedere [Architettura di input per l'interoperabilità tra Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-interoperability-input-architecture.md).  
  
<a name="opacity_and_layering"></a>   
## Opacità e sovrapposizione  
 La classe <xref:System.Windows.Interop.HwndHost> non supporta la sovrapposizione.  Pertanto, l'impostazione della proprietà <xref:System.Windows.UIElement.Opacity%2A> dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> non avrà effetto e non ci sarà fusione con altre finestre [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in cui <xref:System.Windows.Window.AllowsTransparency%2A> è impostato su `true`.  
  
<a name="dispose"></a>   
## Dispose  
 Un'eliminazione non corretta delle classi può determinare una perdita di risorse.  Nelle applicazioni ibride, verificare che le classi <xref:System.Windows.Forms.Integration.WindowsFormsHost> e <xref:System.Windows.Forms.Integration.ElementHost> vengano eliminate, altrimenti potrebbero verificarsi perdite di risorse.  [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] elimina i controlli <xref:System.Windows.Forms.Integration.ElementHost> alla chiusura dell'elemento padre non modale <xref:System.Windows.Forms.Form>. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elimina gli elementi <xref:System.Windows.Forms.Integration.WindowsFormsHost> alla chiusura dell'applicazione.  È possibile visualizzare un elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> di un oggetto <xref:System.Windows.Window> in un ciclo di messaggi [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  In questo caso, è possibile che il codice non riceva notifica della chiusura dell'applicazione.  
  
<a name="enabling_visual_styles"></a>   
## Abilitazione degli stili visivi  
 Gli stili visivi [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] di un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] possono non essere abilitati.  Il metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> viene chiamato nel modello per un'applicazione [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  Sebbene questo metodo non venga chiamato per impostazione predefinita, se si utilizza [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] per creare un progetto, si otterrà gli stili di visualizzazione [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] per i controlli, se è disponibile la versione 6,0 di Comctl32.dll. È necessario chiamare il metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> prima che un handle vengano create nel thread.  Per ulteriori informazioni, vedere [Procedura: attivare stili di visualizzazione in un'applicazione ibrida](../../../../docs/framework/wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md).  
  
<a name="licensed_controls"></a>   
## Controlli con licenza  
 I controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] con licenza che consentono all'utente di visualizzare in una finestra di messaggio le informazioni relative alla licenza potrebbero determinare comportamenti imprevisti in un'applicazione ibrida.  Per alcuni controlli con licenza viene visualizzata una finestra di dialogo in seguito alla creazione di handle.  Ad esempio, un controllo con licenza potrebbe inviare una segnalazione all'utente quando è richiesta una licenza oppure quando sono consentiti ancora tre utilizzi del controllo a scopo di valutazione.  
  
 L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> deriva dalla classe <xref:System.Windows.Interop.HwndHost> e l'handle del controllo figlio viene creato all'interno del metodo <xref:System.Windows.Forms.Integration.WindowsFormsHost.BuildWindowCore%2A>.  La classe <xref:System.Windows.Interop.HwndHost> non consente l'elaborazione di messaggi nel metodo <xref:System.Windows.Forms.Integration.WindowsFormsHost.BuildWindowCore%2A>; tuttavia, la visualizzazione di una finestra di messaggio determina l'invio dei messaggi.  Per abilitare questo scenario di gestione delle licenze, chiamare il metodo <xref:System.Windows.Forms.Control.CreateControl%2A?displayProperty=fullName> del controllo prima di assegnarlo come elemento figlio <xref:System.Windows.Forms.Integration.WindowsFormsHost> dell'elemento.  
  
<a name="wpf_designer"></a>   
## Progettazione WPF  
 È possibile progettare contenuto WPF utilizzando [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)].  Nelle sezioni seguenti sono riportati alcuni problemi comuni che possono verificarsi durante la creazione di applicazioni ibride con [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
### Proprietà BackColorTransparent ignorata in fase di progettazione  
 La proprietà <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> potrebbe non funzionare come previsto in fase di progettazione.  
  
 Se un controllo WPF non si trova su un elemento padre visibile, il runtime WPF ignora il valore di <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A>.  La proprietà <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> potrebbe essere ignorata perché l'oggetto <xref:System.Windows.Forms.Integration.ElementHost> viene creato in un oggetto <xref:System.AppDomain> distinto.  Tuttavia, quando si esegue l'applicazione, <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> funziona come previsto.  
  
### Visualizzazione dell'elenco errori in fase di progettazione quando viene eliminata la cartella obj  
 Se la cartella obj viene eliminata, viene visualizzato l'elenco errori in fase di progettazione.  
  
 Quando si progetta utilizzando <xref:System.Windows.Forms.Integration.ElementHost>, in Progettazione Windows Form vengono utilizzati file generati nella cartella Debug o Release all'interno della cartella obj del progetto.  Se tali file vengono eliminati, verrà visualizzato l'elenco errori in fase di progettazione.  Per risolvere questo problema, ricompilare il progetto.  Per ulteriori informazioni, vedere [Errori in fase di progettazione in Progettazione Windows Form](../../../../docs/framework/winforms/controls/design-time-errors-in-the-windows-forms-designer.md).  
  
<a name="elementhost_and_ime"></a>   
## ElementHost e IME  
 I controlli WPF contenuti in un oggetto <xref:System.Windows.Forms.Integration.ElementHost> attualmente non supportano la proprietà <xref:System.Windows.Forms.Control.ImeMode%2A>.  Le modifiche apportate a <xref:System.Windows.Forms.Control.ImeMode%2A> verranno ignorate dai controlli contenuti.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Interoperabilità in Progettazione WPF](http://msdn.microsoft.com/it-it/2cb7c1ca-2a75-463b-8801-fba81e2b7042)   
 [Architettura di input per l'interoperabilità tra Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-interoperability-input-architecture.md)   
 [Procedura: attivare stili di visualizzazione in un'applicazione ibrida](../../../../docs/framework/wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md)   
 [Considerazioni sul layout per l'elemento WindowsFormsHost](../../../../docs/framework/wpf/advanced/layout-considerations-for-the-windowsformshost-element.md)   
 [Mapping di proprietà di Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)   
 [Errori in fase di progettazione in Progettazione Windows Form](../../../../docs/framework/winforms/controls/design-time-errors-in-the-windows-forms-designer.md)   
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)