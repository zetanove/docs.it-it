---
title: "Sicurezza con attendibilit&#224; parziale in WPF | Microsoft Docs"
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
  - "debug di applicazioni ad attendibilità parziale"
  - "rilevamento di autorizzazioni"
  - "requisiti di sicurezza delle funzioni"
  - "gestione delle autorizzazioni"
  - "applicazioni parzialmente attendibili, debug"
  - "sicurezza dell'attendibilità parziale"
  - "autorizzazioni, rilevamento"
  - "autorizzazioni, gestione"
  - "impostazioni di sicurezza per Internet Explorer"
ms.assetid: ef2c0810-1dbf-4511-babd-1fab95b523b5
caps.latest.revision: 40
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 36
---
# Sicurezza con attendibilit&#224; parziale in WPF
<a name="introduction"></a> In generale, sarebbe opportuno limitare l'accesso diretto alle risorse critiche del sistema da parte delle applicazioni Internet in modo da impedire qualsiasi danno.  Per impostazione predefinita, i linguaggi di scripting [!INCLUDE[TLA#tla_html](../../../includes/tlasharptla-html-md.md)] e lato client non sono in grado di accedere alle risorse critiche del sistema.  Dal momento che le applicazioni [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)] ospitate dal browser possono essere avviate dal browser, devono essere conformi a una serie di limitazioni dello stesso tipo.  Per attivare queste limitazioni, [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] si basa su [!INCLUDE[TLA#tla_cas](../../../includes/tlasharptla-cas-md.md)] e su [!INCLUDE[TLA#tla_clickonce](../../../includes/tlasharptla-clickonce-md.md)] \(vedere [Strategia di sicurezza di WPF \- Sicurezza della piattaforma](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)\).  Per impostazione predefinita, le applicazioni ospitate dal browser richiedono il set di autorizzazioni [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] dell'area Internet, a prescindere dal fatto che vengano avviate da Internet, dalla Intranet locale o dal computer locale.  Le applicazioni in esecuzione con un set di autorizzazioni incompleto vengono definite come applicazioni in esecuzione con attendibilità parziale.  
  
 In [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] viene fornito ampio supporto per garantire l'utilizzo del maggior numero possibile di funzionalità in modo sicuro con attendibilità parziale e, tramite [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)], supporto aggiuntivo per la programmazione con attendibilità parziale.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Supporto con attendibilità parziale della funzionalità WPF](#WPF_Feature_Partial_Trust_Support)  
  
-   [Programmazione con attendibilità parziale](#Partial_Trust_Programming)  
  
-   [Gestione delle autorizzazioni](#Managing_Permissions)  
  
<a name="WPF_Feature_Partial_Trust_Support"></a>   
## Supporto con attendibilità parziale della funzionalità WPF  
 Nella tabella seguente sono elencate le funzionalità di livello elevato di [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)] che è possibile utilizzare in modo sicuro entro i limiti del set di autorizzazioni dell'area Internet.  
  
 Tabella 1: Funzionalità WPF sicure in attendibilità parziale  
  
|Area funzionalità|Funzionalità|  
|-----------------------|------------------|  
|Generale|Finestra del browser<br /><br /> Accesso al sito di origine<br /><br /> IsolatedStorage \(limite di 512 KB\)<br /><br /> Provider UIAutomation<br /><br /> Esecuzione di comandi<br /><br /> IME \(Input Method Editor\)<br /><br /> Stilo e input penna di Tablet PC<br /><br /> Trascinamento della selezione simulato mediante eventi del mouse capture e move<br /><br /> OpenFileDialog<br /><br /> Deserializzazione XAML \(mediante XamlReader.Load\)|  
|Integrazione Web|Finestra di dialogo di download del browser<br /><br /> Navigazione di primo livello avviata dall'utente<br /><br /> mailto:links<br /><br /> Parametri URI \(Uniform Resource Identifier\)<br /><br /> HTTPWebRequest<br /><br /> Contenuto WPF ospitato in IFRAME<br /><br /> Hosting di pagine HTML dello stesso sito utilizzando Frame<br /><br /> Hosting di pagine HTML dello stesso sito utilizzando WebBrowser<br /><br /> Servizi Web \(ASMX\)<br /><br /> Servizi Web \(mediante Windows Communication Foundation\)<br /><br /> Scripting<br /><br /> DOM \(Document Object Model\)|  
|Visiva|2D e 3D<br /><br /> Animazione<br /><br /> Elementi multimediali \(sito di origine e tra domini\)<br /><br /> Immagini\/Audio\/Video|  
|Lettura|Oggetti FlowDocuments<br /><br /> Documenti XPS<br /><br /> Tipi di carattere incorporati e di sistema<br /><br /> Caratteri CFF e TrueType|  
|Modifica|Controllo ortografico<br /><br /> RichTextBox<br /><br /> Supporto Appunti per testo non crittografato e input penna<br /><br /> Operazione Incolla avviata dall'utente<br /><br /> Copia di contenuto selezionato|  
|Controlli|Controlli generici|  
  
 Nella tabella sono incluse le funzionalità [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] di livello elevato.  Per informazioni più dettagliate, consultare la documentazione disponibile in [!INCLUDE[TLA#tla_lhsdk](../../../includes/tlasharptla-lhsdk-md.md)] sulle autorizzazioni necessarie per ciascun membro di [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)].  Inoltre, le seguenti funzionalità contengono informazioni più dettagliate sull'esecuzione in situazioni di attendibilità parziale, con alcune considerazioni speciali.  
  
-   [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] \(vedere [Cenni preliminari su XAML \(WPF\)](../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)\).  
  
-   Popup \(vedere <xref:System.Windows.Controls.Primitives.Popup?displayProperty=fullName>\).  
  
-   Trascinamento della selezione \(vedere [Cenni preliminari sul trascinamento della selezione](../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)\).  
  
-   Appunti \(vedere <xref:System.Windows.Clipboard?displayProperty=fullName>\).  
  
-   Immagini \(vedere <xref:System.Windows.Controls.Image?displayProperty=fullName>\).  
  
-   Serializzazione \(vedere <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=fullName>, <xref:System.Windows.Markup.XamlWriter.Save%2A?displayProperty=fullName>\).  
  
-   Finestra di dialogo Apri file \(vedere <xref:Microsoft.Win32.OpenFileDialog?displayProperty=fullName>\).  
  
 Nella tabella seguente sono elencate le funzionalità [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] che non è possibile utilizzare in modo sicuro entro i limiti del set di autorizzazioni dell'area Internet.  
  
 Tabella 2: Funzionalità WPF non sicure in attendibilità parziale  
  
|Area funzionalità|Funzionalità|  
|-----------------------|------------------|  
|Generale|Finestra \(finestre e finestre di dialogo definite dall'applicazione\)<br /><br /> SaveFileDialog<br /><br /> File system<br /><br /> Accesso al Registro di sistema<br /><br /> Trascinamento della selezione<br /><br /> Serializzazione XAML \(mediante XamlWriter.Save\)<br /><br /> Client UIAutomation<br /><br /> Accesso alla finestra di origine \(HwndHost\)<br /><br /> Supporto vocale completo<br /><br /> Interoperabilità con Windows Form|  
|Visiva|Effetti bitmap<br /><br /> Codifica delle immagini|  
|Modifica|Appunti RTF \(Rich\-Text Format\)<br /><br /> Supporto XAML completo|  
  
<a name="Partial_Trust_Programming"></a>   
## Programmazione con attendibilità parziale  
 Per applicazioni [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)], il codice che supera il set di autorizzazioni predefinito avrà un comportamento diverso a seconda dell'area di sicurezza.  In alcuni casi, l'utente riceverà un avviso quando si tenta di installare il codice.  L'utente potrà scegliere se continuare o annullare l'installazione.  Nella tabella che segue viene descritto il comportamento dell'applicazione per ogni area di sicurezza e le azioni necessarie relative all'applicazione per acquisire attendibilità totale.  
  
|Area di sicurezza|Comportamento|Acquisizione di attendibilità totale|  
|-----------------------|-------------------|------------------------------------------|  
|Computer locale|Attendibilità totale automatica|Nessuna azione necessaria.|  
|Intranet e siti attendibili|Richiesta di attendibilità totale|Firma dell'applicazione XBAP con un certificato in modo che l'utente veda l'origine nel prompt.|  
|Internet|Esito negativo con Attendibilità non concessa|Firma dell'applicazione XBAP con un certificato.|  
  
> [!NOTE]
>  Il comportamento descritto nella tabella precedente è relativo alle applicazioni XBAP con attendibilità totale che non seguono il modello di distribuzione attendibile di ClickOnce.  
  
 In genere, è probabile che il codice che richiede autorizzazioni ulteriori rispetto a quelle consentite sia codice comune condiviso dalle applicazioni autonome e da quelle ospitate dal browser.  In [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] e in [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] vengono fornite varie tecniche per la gestione di uno scenario di questo tipo.  
  
<a name="Detecting_Permissions_using_CAS"></a>   
### Rilevamento delle autorizzazioni tramite CAS  
 In alcune situazioni, è possibile che il codice condiviso degli assembly di librerie sia utilizzato dalle applicazioni autonome e dalle [!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)].  In questi casi, è possibile che il codice esegua funzionalità che potrebbero richiedere un numero di autorizzazioni maggiore rispetto al set assegnato all'applicazione.  L'applicazione consente di rilevare automaticamente se sono disponibili determinate autorizzazioni utilizzando le funzionalità di sicurezza di [!INCLUDE[TLA#tla_winfx](../../../includes/tlasharptla-winfx-md.md)].  In modo specifico, è possibile verificare la disponibilità di una determinata autorizzazione chiamando il metodo <xref:System.Security.CodeAccessPermission.Demand%2A> sull'istanza dell'autorizzazione desiderata.  Tale procedura viene mostrata nell'esempio seguente, in cui il codice esegue una query per verificare la disponibilità dell'autorizzazione a salvare un file sul disco locale:  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](../../../samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](../../../samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode2)]  
  
 Se un'applicazione non dispone dell'autorizzazione desiderata, la chiamata al metodo <xref:System.Security.CodeAccessPermission.Demand%2A> genera un'eccezione di sicurezza.  In caso contrario, l'autorizzazione è disponibile.  `IsPermissionGranted` incapsula questo comportamento e restituisce `true` o `false` a seconda dei casi.  
  
<a name="Graceful_Degradation_of_Functionality"></a>   
### Riduzione normale delle prestazioni della funzionalità  
 La capacità del codice di rilevare le autorizzazioni di cui dispone risulta particolarmente interessante nel caso in cui il codice può essere eseguito da aree diverse.  Sebbene il rilevamento dell'area sia importante, è meglio fornire un'alternativa all'utente, se possibile.  Ad esempio, di solito un'applicazione con attendibilità totale consente agli utenti di creare file in qualsiasi posizione, mentre un'applicazione con attendibilità parziale consente di creare file unicamente in uno spazio di memorizzazione isolato.  Se il codice per la creazione di un file è contenuto in un assembly condiviso da applicazioni con attendibilità totale \(autonome\) e applicazioni con attendibilità parziale \(ospitate dal browser\) e si desidera che entrambi i tipi di applicazioni consentano la creazione di file, il codice condiviso dovrà rilevare se viene eseguito in attendibilità parziale o totale prima di creare un file nel percorso appropriato.  I due casi sono illustrati nel codice riportato di seguito.  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](../../../samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](../../../samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode2)]  
  
 In molte situazioni è possibile trovare un'alternativa all'attendibilità parziale.  
  
 In un ambiente controllato, ad esempio una Intranet, è possibile installare framework gestiti personalizzati nella base client in [!INCLUDE[TLA#tla_gac](../../../includes/tlasharptla-gac-md.md)].  Queste librerie possono eseguire codice che richiede attendibilità totale e possono essere oggetto di riferimento da parte di applicazioni alle quali è consentita unicamente l'attendibilità parziale tramite <xref:System.Security.AllowPartiallyTrustedCallersAttribute>. Per ulteriori informazioni, vedere [Sicurezza](../../../docs/framework/wpf/security-wpf.md) e [Strategia di sicurezza di WPF \- Sicurezza della piattaforma](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md).  
  
<a name="Browser_Host_Detection"></a>   
### Rilevamento host del browser  
 L'utilizzo di [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] per la verifica delle autorizzazioni è una tecnica appropriata se è necessaria una verifica per singola autorizzazione.  Tuttavia, tale tecnica dipende dal rilevamento di eccezioni durante la normale elaborazione, operazione che in genere non è consigliata e che può causare problemi di prestazioni.  Al contrario, se l'[!INCLUDE[TLA#tla_xbap](../../../includes/tlasharptla-xbap-md.md)] viene eseguita solo nella sandbox dell'area Internet, è possibile utilizzare la proprietà <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A?displayProperty=fullName>, che restituisce true per le [!INCLUDE[TLA#tla_xbap#plural](../../../includes/tlasharptla-xbapsharpplural-md.md)].  
  
> [!NOTE]
>  La proprietà <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A> consente unicamente di stabilire se un'applicazione è eseguita in un browser, non il set di autorizzazioni utilizzato dall'applicazione.  
  
<a name="Managing_Permissions"></a>   
## Gestione delle autorizzazioni  
 Per impostazione predefinita, le applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)] vengono eseguite con attendibilità parziale \(set di autorizzazioni dell'area Internet predefinito\).  Tuttavia, a seconda dei requisiti dell'applicazione, questo set predefinito può essere modificato.  Se, ad esempio, un'applicazione [!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)] viene avviata da una Intranet locale, può usufruire di un set di autorizzazioni più esteso, illustrato nella tabella seguente.  
  
 Tabella 3: Autorizzazioni LocalIntranet e Internet  
  
|Autorizzazione|Attributo|LocalIntranet|Internet|  
|--------------------|---------------|-------------------|--------------|  
|DNS|Accesso ai server DNS|Sì|No|  
|Variabili di ambiente|Lettura|Sì|No|  
|Finestre di dialogo file|Aprire|Sì|Sì|  
|Finestre di dialogo file|Illimitato|Sì|No|  
|Archiviazione isolata|Isolamento assembly in base all'utente|Sì|No|  
|Archiviazione isolata|Isolamento sconosciuto|Sì|Sì|  
|Archiviazione isolata|Quota utenti illimitata|Sì|No|  
|Supporti multimediali|Audio, video e immagini sicure|Sì|Sì|  
|Stampa|Stampa predefinita|Sì|No|  
|Stampa|Stampa sicura|Sì|Sì|  
|Reflection|Emissione|Sì|No|  
|Sicurezza|Esecuzione del codice gestito|Sì|Sì|  
|Sicurezza|Asserzione autorizzazioni concesse|Sì|No|  
|Interfaccia utente|Illimitato|Sì|No|  
|Interfaccia utente|Finestre di primo livello sicure|Sì|Sì|  
|Interfaccia utente|Appunti personali|Sì|Sì|  
|Browser|Navigazione sicura dei frame in HTML|Sì|Sì|  
  
> [!NOTE]
>  L'operazione di taglia e incolla, se avviata dall'utente, è consentita solo con l'attendibilità parziale.  
  
 Per aumentare il numero di autorizzazioni, è necessario modificare le impostazioni del progetto e il manifesto dell'applicazione ClickOnce.  Per ulteriori informazioni, vedere [Panoramica delle applicazioni browser XAML di WPF](../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md).  Anche i seguenti documenti possono rivelarsi utili.  
  
-   [Mage.exe \(Strumento per la generazione e la modifica di manifesti\)](../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md).  
  
-   [MageUI.exe \(Strumento per la generazione e la modifica di manifesti, client grafico\)](../../../docs/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md).  
  
-   [Protezione di applicazioni ClickOnce](../Topic/Securing%20ClickOnce%20Applications.md).  
  
 Se l'applicazione [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)] in uso richiede l'attendibilità totale, è possibile utilizzare gli stessi strumenti per aumentare le autorizzazioni necessarie.  Tuttavia l'attendibilità totale verrà ottenuta solo se un'applicazione [!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)] viene installata o avviata dal computer locale, dalla Intranet o da un URL incluso nell'elenco dei siti attendibili o consentiti del browser.  Se l'applicazione viene installata dalla Intranet o da un sito attendibile, verrà visualizzato all'utente il prompt standard di ClickOnce con la notifica relativa alle autorizzazioni elevate.  L'utente potrà scegliere se continuare o annullare l'installazione.  
  
 In alternativa, è possibile utilizzare il modello di distribuzione attendibile di ClickOnce per una distribuzione con attendibilità totale da qualsiasi area di sicurezza.  Per ulteriori informazioni, vedere [Cenni preliminari sulla distribuzione di applicazioni attendibili](../Topic/Trusted%20Application%20Deployment%20Overview.md) e [Sicurezza](../../../docs/framework/wpf/security-wpf.md).  
  
## Vedere anche  
 [Sicurezza](../../../docs/framework/wpf/security-wpf.md)   
 [Strategia di sicurezza di WPF \- Sicurezza della piattaforma](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)   
 [Strategia di sicurezza WPF \- Progettazione di sicurezza](../../../docs/framework/wpf/wpf-security-strategy-security-engineering.md)