---
title: "Distribuzione di un&#39;applicazione WPF (WPF) | Microsoft Docs"
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
  - "distribuzione [WPF], applicazioni"
  - "WPF (applicazioni), distribuzione"
ms.assetid: 12cadca0-b32c-4064-9a56-e6a306dcc76d
caps.latest.revision: 27
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# Distribuzione di un&#39;applicazione WPF (WPF)
Dopo la compilazione, è necessario distribuire le applicazioni [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)].  [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] e [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] includono diverse tecnologie di distribuzione.  La tecnologia di distribuzione utilizzata per distribuire un'applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] dipende dal tipo di applicazione.  In questo argomento vengono forniti alcuni cenni preliminari su ogni tecnologia di distribuzione e sul relativo utilizzo in relazione ai requisiti di distribuzione di ogni tipo di applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
   
  
<a name="Deployment_Technologies"></a>   
## Tecnologie di distribuzione  
 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] e [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] includono varie tecnologie di distribuzione, tra le quali:  
  
-   Distribuzione tramite XCopy.  
  
-   Distribuzione [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)].  
  
-   Distribuzione [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)].  
  
<a name="XCopy_Deployment"></a>   
### Distribuzione tramite XCopy  
 La distribuzione tramite XCopy fa riferimento all'utilizzo del programma della riga di comando XCopy per copiare file da un percorso a un altro.  La distribuzione tramite XCopy è appropriata nelle seguenti circostanze:  
  
-   L'applicazione è indipendente.  Non è necessario aggiornare il client per l'esecuzione.  
  
-   I file dell'applicazione devono essere spostati da un percorso a un altro, ad esempio da un percorso di compilazione \(disco locale, condivisione file [!INCLUDE[TLA2#tla_unc](../../../../includes/tla2sharptla-unc-md.md)] e così via\) a un percorso di pubblicazione \(sito Web, condivisione file [!INCLUDE[TLA2#tla_unc](../../../../includes/tla2sharptla-unc-md.md)] e così via\).  
  
-   L'applicazione non richiede l'integrazione della shell \(collegamento del menu Start, icona del desktop e così via\).  
  
 XCopy è appropriato per scenari di distribuzione semplici e risulta limitato quando sono richieste funzionalità di distribuzione più complesse.  In particolare, l'utilizzo di XCopy comporta spesso un sovraccarico dovuto alla creazione, all'esecuzione e al mantenimento di script per garantire una gestione affidabile della distribuzione.  XCopy, inoltre, non supporta il controllo della versione, la disinstallazione o il rollback.  
  
<a name="Windows_Installer"></a>   
### Windows Installer  
 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] consente di assemblare le applicazioni come eseguibili autonomi di facile distribuzione ai client e di altrettanto facile esecuzione.  [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] viene installato con [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] e consente l'integrazione con il desktop, il menu Start e il pannello di controllo Programmi.  
  
 [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)] semplifica l'installazione e la disinstallazione delle applicazioni, ma non offre alcuna possibilità di assicurare che le applicazioni installate siano mantenute aggiornate dal punto di vista del controllo della versione.  
  
 Per ulteriori informazioni su [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)], vedere [Windows Installer Deployment](http://msdn.microsoft.com/it-it/121be21b-b916-43e2-8f10-8b080516d2a0).  
  
<a name="ClickOnce_Deployment"></a>   
### Distribuzione ClickOnce  
 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] consente di distribuire le applicazioni non Web come applicazioni Web. Le applicazioni vengono pubblicate e distribuite da server Web o da file server.  La distribuzione [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] non supporta la gamma completa di funzionalità client delle applicazioni installate tramite [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)], tuttavia supporta le funzionalità seguenti:  
  
-   Integrazione con il menu Start e con il pannello di controllo Programmi.  
  
-   Controllo della versione, rollback e disinstallazione.  
  
-   Modalità di installazione online che implica sempre l'avvio di un'applicazione dal percorso di distribuzione.  
  
-   Aggiornamento automatico al rilascio di nuove versioni.  
  
-   Registrazione di estensioni di file.  
  
 Per ulteriori informazioni su [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)], vedere [Sicurezza e distribuzione di ClickOnce](../Topic/ClickOnce%20Security%20and%20Deployment.md).  
  
<a name="Deploying_WPF_Applications"></a>   
## Distribuzione di applicazioni WPF  
 Le opzioni di distribuzione per un'applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] dipendono dal tipo di applicazione.  Dal punto di vista della distribuzione, in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] sono disponibili tre tipi di applicazione significativi:  
  
-   applicazioni autonome  
  
-   applicazioni [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] solo markup  
  
-   [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)].  
  
<a name="Deploying_Standalone_Applications"></a>   
### Distribuzione di applicazioni autonome  
 Le applicazioni autonome vengono distribuite utilizzando [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] o [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)].  In entrambi i casi, l'esecuzione delle applicazioni autonome richiede l'attendibilità totale.  L'attendibilità totale viene concessa automaticamente alle applicazioni autonome distribuite tramite [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)].  Alle applicazioni autonome distribuite tramite [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] non viene automaticamente concessa l'attendibilità totale.  Con la distribuzione [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] viene invece visualizzata una finestra di dialogo contenente un avviso di sicurezza che gli utenti devono accettare prima di installare un'applicazione autonoma.  Se questo avviso viene accettato, all'applicazione autonoma installata viene concessa l'attendibilità totale.  In caso contrario, l'applicazione autonoma non viene installata.  
  
<a name="Deploying_Markup_Only_XAML_Applications"></a>   
### Distribuzione di applicazioni XAML solo markup  
 Analogamente alle pagine [!INCLUDE[TLA2#tla_html](../../../../includes/tla2sharptla-html-md.md)], le pagine [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] solo markup vengono generalmente pubblicate in un server Web e possono essere visualizzate tramite [!INCLUDE[TLA2#tla_iegeneric](../../../../includes/tla2sharptla-iegeneric-md.md)].  Le pagine [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] solo markup vengono eseguite in un sandbox di sicurezza con attendibilità parziale e con restrizioni definite dal set di autorizzazioni dell'area Internet.  In questo modo, viene fornito un sandbox di sicurezza equivalente alle applicazioni Web basate su [!INCLUDE[TLA2#tla_html](../../../../includes/tla2sharptla-html-md.md)].  
  
 Per ulteriori informazioni sulla sicurezza per le applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], vedere [Sicurezza](../../../../docs/framework/wpf/security-wpf.md).  
  
 Le pagine [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] solo markup possono essere installate nel file system locale utilizzando XCopy o [!INCLUDE[TLA2#tla_wininstall](../../../../includes/tla2sharptla-wininstall-md.md)].  È possibile visualizzare queste pagine mediante [!INCLUDE[TLA2#tla_iegeneric](../../../../includes/tla2sharptla-iegeneric-md.md)], [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] o Esplora risorse.  
  
 Per ulteriori informazioni su XAML, vedere [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md).  
  
<a name="Deploying_XAML_Browser_Applications"></a>   
### Distribuzione di applicazioni browser XAML  
 Le [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] sono applicazioni compilate la cui distribuzione richiede i tre file elencati di seguito:  
  
-   *NomeApplicazione*.exe: il file dell'applicazione dell'assembly eseguibile.  
  
-   *NomeApplicazione*.xbap: il manifesto di distribuzione.  
  
-   *NomeApplicazione*.exe.manifest: il manifesto dell'applicazione.  
  
> [!NOTE]
>  Per ulteriori informazioni sulla distribuzione e sui manifesti dell'applicazione, vedere [Compilazione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md).  
  
 Questi file vengono prodotti quando un'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] viene compilata.  Per ulteriori informazioni, vedere [Procedura: creare un nuovo progetto di applicazione browser WPF](http://msdn.microsoft.com/it-it/72ef4d90-e163-42a1-8df0-ea7ccfd1901f).  Analogamente alle pagine [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] solo markup, le applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] vengono generalmente pubblicate in un server Web e visualizzate tramite [!INCLUDE[TLA2#tla_iegeneric](../../../../includes/tla2sharptla-iegeneric-md.md)].  
  
 È possibile distribuire [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] ai client utilizzando qualsiasi tecnica di distribuzione.  Tuttavia, è consigliato l'utilizzo di [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] in quanto fornisce le funzionalità seguenti:  
  
1.  Aggiornamenti automatici alla pubblicazione di una nuova versione.  
  
2.  Elevazione dei privilegi per [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] in esecuzione con attendibilità totale.  
  
 Per impostazione predefinita, ClickOnce pubblica i file dell'applicazione con l'estensione deploy.  Tale funzionalità può risultare di difficile gestione, ma è possibile disabilitarla.  Per ulteriori informazioni, vedere [Problemi relativi alla configurazione del server e del client nelle distribuzioni ClickOnce](../Topic/Server%20and%20Client%20Configuration%20Issues%20in%20ClickOnce%20Deployments.md).  
  
 Per ulteriori informazioni sulla distribuzione di un'[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)], vedere [Panoramica delle applicazioni browser XAML di WPF](../../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md).  
  
<a name="Installing__NET_Framework_3_0"></a>   
## Installazione di .NET Framework  
 Per eseguire un'applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], è necessario installare [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] nel client.  [!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] rileva automaticamente se i client dispongono di [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] quando vengono visualizzate applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ospitate dal browser.  Se [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] non è installato, [!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] ne richiede l'installazione.  
  
 Per verificare se [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] è installato, in [!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] è inclusa un'applicazione di avvio automatico registrata come gestore [!INCLUDE[TLA#tla_mime](../../../../includes/tlasharptla-mime-md.md)] di fallback per i file di dati con le seguenti estensioni: xaml, xps, xbap e application.  Quando si passa a questi tipi di file e [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] non è installato nel client, l'applicazione di avvio automatico richiede l'autorizzazione per installarlo.  Se l'autorizzazione non viene concessa, non viene installato né [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)], né l'applicazione.  
  
 Se l'autorizzazione viene concessa, [!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] scarica e installa [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] utilizzando [!INCLUDE[TLA#tla_bits](../../../../includes/tlasharptla-bits-md.md)].  Al termine dell'installazione di [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)], il file richiesto viene aperto in una nuova finestra del browser.  
  
 Il rilevamento automatico dell'installazione di [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] è disponibile nei client [!INCLUDE[TLA#tla_longhorn](../../../../includes/tlasharptla-longhorn-md.md)], [!INCLUDE[TLA#tla_winxpsp2](../../../../includes/tlasharptla-winxpsp2-md.md)] e [!INCLUDE[TLA#tla_winnetsvrfamsp1](../../../../includes/tlasharptla-winnetsvrfamsp1-md.md)] con [!INCLUDE[TLA2#tla_ie7](../../../../includes/tla2sharptla-ie7-md.md)] o versione successiva installata.  
  
 Per ulteriori informazioni, vedere [Distribuzione di .NET Framework e delle applicazioni](../../../../docs/framework/deployment/net-framework-and-applications.md).  
  
## Vedere anche  
 [Compilazione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)   
 [Sicurezza](../../../../docs/framework/wpf/security-wpf.md)