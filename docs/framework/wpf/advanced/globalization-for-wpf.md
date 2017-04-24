---
title: "Globalizzazione per WPF | Microsoft Docs"
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
  - "globalizzazione"
  - "interfaccia utente internazionale, XAML"
  - "XAML, globalizzazione"
  - "XAML, interfaccia utente internazionale"
ms.assetid: 4571ccfe-8a60-4f06-9b37-7ac0b1c2d10f
caps.latest.revision: 35
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 31
---
# Globalizzazione per WPF
In questo argomento vengono presentati i problemi da considerare per la scrittura di applicazioni [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] per il mercato globale.  Gli elementi di programmazione per la globalizzazione sono definiti in [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] in `System.Globalization`.  
  
   
  
<a name="xaml_globalization"></a>   
## Globalizzazione XAML  
 [!INCLUDE[TLA#tla_xaml#initcap](../../../../includes/tlasharptla-xamlsharpinitcap-md.md)] si basa su [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] e sfrutta i vantaggi del supporto della globalizzazione definito nella specifica [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)].  Nelle sezioni riportate di seguito vengono descritte alcune funzionalità [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] da tenere presenti.  
  
<a name="char_reference"></a>   
### Riferimenti a carattere  
 Un riferimento a carattere fornisce il numero del carattere [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] specifico che rappresenta, decimale o esadecimale.  Nell'esempio riportato di seguito viene illustrato un riferimento a carattere decimale.  
  
```  
Ϩ  
```  
  
 Nell'esempio viene illustrato un riferimento a carattere esadecimale.  Si noti che è presente una **x** davanti al numero esadecimale.  
  
```  
Ϩ  
```  
  
<a name="encoding"></a>   
### Codifica  
 Le codifiche supportate da [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] sono [!INCLUDE[TLA#tla_ascii](../../../../includes/tlasharptla-ascii-md.md)], [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] UTF\-16 e UTF\-8.  L'istruzione di codifica si trova all'inizio del documento [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Se non è presente alcun attributo di codifica né un ordine dei byte, verrà utilizzato il valore predefinito UTF\-8.  UTF\-8 e UTF\-16 sono le codifiche preferite.  UTF\-7 non è supportata.  Nell'esempio riportato di seguito viene illustrato come specificare una codifica UTF\-8 in un file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
```  
?xml encoding="UTF-8"?  
```  
  
<a name="lang_attrib"></a>   
### Attributo Language  
 In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] viene utilizzato [xml:lang](../../../../docs/framework/xaml-services/xml-lang-handling-in-xaml.md) per rappresentare l'attributo Language di un elemento.  Per sfruttare al meglio la classe <xref:System.Globalization.CultureInfo>, è necessario che il valore dell'attributo Language sia uno dei nomi di impostazioni cultura predefiniti da <xref:System.Globalization.CultureInfo>.  [xml:lang](../../../../docs/framework/xaml-services/xml-lang-handling-in-xaml.md) è ereditabile nella struttura ad albero dell'elemento, in base alle regole XML, non necessariamente per l'ereditarietà della proprietà di dipendenza, e l'impostazione predefinita è una stringa vuota se non viene assegnato esplicitamente un valore.  
  
 L'attributo Language è utile per la specifica di sottolinguaggi.  Ad esempio, la lingua francese ha ortografia, vocabolario e pronuncia diverse in Francia, Quebec, Belgio e Svizzera.  Anche il cinese, il giapponese e il coreano condividono elementi di codice in [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)], ma le forme ideografiche sono diverse e utilizzano tipi di carattere diversi.  
  
 Nell'esempio [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] riportato di seguito viene utilizzato l'attributo Language `fr-CA` per specificare la lingua francese canadese.  
  
```  
<TextBlock xml:lang="fr-CA">Découvrir la France</TextBlock>  
```  
  
<a name="unicode"></a>   
### Unicode  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] supporta tutte le funzionalità [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)], inclusi i sostituti.  Il set di caratteri è supportato purché sia possibile mapparlo a [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)].  Ad esempio, GB18030 presenta alcuni caratteri mappati all'estensione A e B e alle coppie sostitutive di cinese, giapponese e coreano \(CFK\), pertanto è completamente supportato.  Un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] può utilizzare <xref:System.Globalization.StringInfo> per modificare le stringhe senza capire se queste dispongano di coppie sostitutive o segni di unione.  
  
<a name="design_intl_ui_with_xaml"></a>   
## Progettazione di un'interfaccia utente internazionale con XAML  
 In questa sezione vengono illustrate le funzionalità dell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] da considerare per la scrittura di un'applicazione.  
  
<a name="intl_text"></a>   
### Testo internazionale  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] include l'elaborazione predefinita per tutti i sistemi di scrittura [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] supportati.  
  
 Attualmente sono supportati i seguenti script:  
  
-   Arabo  
  
-   Bengali  
  
-   Devanagari  
  
-   Cirillico  
  
-   Greco  
  
-   Gujarati  
  
-   Gurmukhi  
  
-   Ebraico  
  
-   Script ideografici  
  
-   Kannada  
  
-   Lao  
  
-   Latino  
  
-   Malayalam  
  
-   Mongolo  
  
-   Odia  
  
-   Siriano  
  
-   Tamil  
  
-   Telugu  
  
-   Thaana  
  
-   Thai\*  
  
-   Tibetano  
  
 \*In questa versione è supportata la visualizzazione e la modifica del testo thai, ma non l'interruzione di parola.  
  
 Attualmente gli script riportati di seguito non sono supportati:  
  
-   Khmer  
  
-   Coreano Hangul antico  
  
-   Birmano  
  
-   Singalese  
  
 Tutti i motori dei sistemi di scrittura supportano i tipi di carattere [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)].  I tipi di carattere [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] possono includere le tabelle di layout [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] che consentono ai creatori dei tipi di carattere di progettare in modo ottimale caratteri tipografici internazionali e di alto livello.  Le tabelle di layout dei tipi di carattere [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] contengono informazioni sulle sostituzioni e sul posizionamento dei glifi, sulla giustificazione e sul posizionamento di base, consentendo alle applicazioni di elaborazione testi di migliorare il layout del testo.  
  
 I tipi di carattere [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] consentono la gestione di grandi set di glifi tramite la codifica [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)].  Tale codifica garantisce un ampio supporto internazionale nonché il supporto delle varianti di glifo tipografiche.  
  
 Il rendering del testo di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] si basa sulla tecnologia dei subpixel [!INCLUDE[TLA#tla_ct](../../../../includes/tlasharptla-ct-md.md)] che supporta l'indipendenza dalla risoluzione.  Viene in tal modo migliorata significativamente la leggibilità e viene offerta la capacità di supportare documenti di alta qualità per tutti gli script.  
  
<a name="intl_layout"></a>   
### Layout internazionale  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] offre un modo pratico per supportare layout orizzontali, bidirezionali e verticali.  Nel framework della presentazione è possibile utilizzare la proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A> per definire il layout.  I modelli di direzione del testo sono:  
  
-   *LeftToRight*: layout orizzontale per l'alfabeto latino, asiatico e così via.  
  
-   *RightToLeft*: bidirezionale per arabo, ebraico e così via.  
  
<a name="developing_localizable_apps"></a>   
## Sviluppo di applicazioni localizzabili  
 Quando si scrive un'applicazione per il mercato globale è opportuno tenere presente che l'applicazione deve essere localizzabile.  Negli argomenti riportati di seguito vengono evidenziati i punti da considerare.  
  
<a name="mui"></a>   
### Interfaccia utente multilingue  
 Le interfacce utente multilingue \(MUI, Multilingual User Interface\) è un supporto [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] per il passaggio tra [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] in lingue diverse.  Un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza il modello di assembly per supportare le interfacce MUI.  Un'applicazione contiene sia assembly indipendenti dalla lingua sia assembly di risorse satellite dipendenti dalla lingua.  Il punto di ingresso è un file exe gestito nell'assembly principale.  Il caricatore di risorse [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sfrutta la gestione risorse di [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)] per supportare la ricerca e il fallback delle risorse.  Gli assembly satellite multilingue funzionano con lo stesso assembly principale.  L'assembly di risorse caricato dipende dalla proprietà <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> del thread corrente.  
  
<a name="localizable_ui"></a>   
### Interfaccia utente localizzabile  
 Le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizzano [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] per definire la propria [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)].  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] consente agli sviluppatori di specificare una gerarchia di oggetti con un set di proprietà e logica.  L'utilizzo principale del linguaggio [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è quello di sviluppare applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], ma può anche essere utilizzato per specificare una gerarchia di oggetti [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  La maggior parte degli sviluppatori utilizza il linguaggio [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] per specificare l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dell'applicazione e un linguaggio di programmazione quale [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] per rispondere all'interazione dell'utente.  
  
 Dal punto di vista della risorsa, un file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] progettato per descrivere un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dipendente dal linguaggio è un elemento risorsa, pertanto il formato di distribuzione finale deve essere localizzabile per supportare lingue internazionali.  Poiché il linguaggio [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] non consente di gestire eventi, molte applicazioni [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] contengono blocchi di codice per tale scopo.  Per ulteriori informazioni, vedere [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md).  Il codice viene rimosso e compilato in binari diversi quando un file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] viene suddiviso in token nel form BAML di XAML. File, le immagini e altri tipi di oggetti di risorse gestite del form BALM di XAML sono incorporati nell'assembly di risorse satellite, che può essere localizzato in altre lingue o nell'assembly principale quando la localizzazione non è necessaria.  
  
> [!NOTE]
>  Le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] supportano tutte le risorse [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] di [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)], incluse tabelle di stringhe, immagini e così via.  
  
<a name="building_localizable_apps"></a>   
### Compilazione di applicazioni localizzabili  
 Per localizzazione si intende l'adattamento di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] a impostazioni cultura diverse.  Per rendere localizzabile un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario che gli sviluppatori compilino tutte le risorse localizzabili in un assembly di risorse.  L'assembly di risorse viene localizzato in lingue diverse e il code\-behind utilizza l'[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] di gestione risorse per il caricamento.  Uno dei file necessari per un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è un file di progetto \(proj\).  Tutte le risorse utilizzate nell'applicazione devono essere incluse nel file di progetto.  Nell'esempio di file csproj riportato di seguito viene illustrato come procedere.  
  
```  
<Resource Include="data\picture1.jpg"/>  
<EmbeddedResource Include="data\stringtable.en-US.restext"/>  
```  
  
 Per utilizzare una risorsa nell'applicazione, creare un'istanza dell'oggetto <xref:System.Resources.ResourceManager> e caricare la risorsa che si desidera utilizzare.  Nell'esempio riportato di seguito viene illustrato come procedere.  
  
 [!code-csharp[LocalizationResources#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]  
  
<a name="using_clickonce"></a>   
## Utilizzo di ClickOnce con applicazioni localizzate  
 ClickOnce è una nuova tecnologia di distribuzione di Windows Form fornita con [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)].  Consente l'installazione e l'aggiornamento di applicazioni Web.  Quando un'applicazione distribuita con ClickOnce viene localizzata, può essere visualizzata solo in base alle impostazioni cultura in cui è localizzata.  Se ad esempio un'applicazione distribuita viene localizzata in giapponese, può essere visualizzato solo nella versione giapponese di [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)], non in quella inglese.  Questa condizione costituisce un problema poiché gli utenti giapponesi utilizzano solitamente una versione inglese di [!INCLUDE[TLA2#tla_win](../../../../includes/tla2sharptla-win-md.md)].  
  
 La soluzione a questo problema consiste nell'impostare l'attributo di fallback della lingua di sistema.  Uno sviluppatore di applicazioni può rimuovere facoltativamente le risorse dall'assembly principale e specificare che tali risorse sono disponibili in un assembly satellite corrispondente a impostazioni cultura specifiche.  A tale scopo, utilizzare l'oggetto <xref:System.Resources.NeutralResourcesLanguageAttribute>.  Il costruttore della classe <xref:System.Resources.NeutralResourcesLanguageAttribute> presenta due firme, una che accetta un parametro <xref:System.Resources.UltimateResourceFallbackLocation> per specificare il percorso in cui l'oggetto <xref:System.Resources.ResourceManager> estrae le risorse di fallback, assembly principale o satellite.  Nell'esempio riportato di seguito viene illustrato come utilizzare l'attributo.  Per il percorso di fallback finale, nel codice viene specificato che l'oggetto <xref:System.Resources.ResourceManager> cerchi le risorse nella sottodirectory "de" della directory dell'assembly attualmente in esecuzione.  
  
```  
[assembly: NeutralResourcesLanguageAttribute(  
    "de" , UltimateResourceFallbackLocation.Satellite)]  
  
```  
  
## Vedere anche  
 [Cenni preliminari sulla globalizzazione e localizzazione WPF](../../../../docs/framework/wpf/advanced/wpf-globalization-and-localization-overview.md)