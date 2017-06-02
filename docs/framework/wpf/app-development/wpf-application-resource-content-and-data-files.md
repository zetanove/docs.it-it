---
title: "File di dati e di risorse dell&#39;applicazione WPF. | Microsoft Docs"
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
  - "sviluppo di applicazioni [WPF], file"
  - "gestione applicazioni [WPF]"
  - "file di dati [WPF]"
  - "risorse incorporate [WPF]"
  - "file [WPF]"
  - "risorse separate [WPF]"
  - "riferimento ai file dell'applicazione [WPF]"
  - "file remoti [WPF]"
  - "file di risorse [WPF]"
  - "sito di origine (file) [WPF]"
  - "applicazione WPF, file"
ms.assetid: 7ad2943b-3961-41d3-8fc6-1582d43f5d99
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# File di dati e di risorse dell&#39;applicazione WPF.
Le applicazioni [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] dipendono spesso da file contenenti dati non eseguibili, quali ad esempio [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], immagini, video e audio.  [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] offre un supporto speciale per la configurazione, l'identificazione e l'utilizzo di questi tipi di file di dati, definiti file di dati dell'applicazione.  Questo supporto si basa su un insieme specifico di tipi di file di dati dell'applicazione, tra cui:  
  
-   **File di risorse**: file di dati compilati in un assembly [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] eseguibile o di librerie.  
  
-   **File di dati**: file di dati autonomi che possiedono un'associazione esplicita a un assembly [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] eseguibile.  
  
-   **File del sito di origine**: file di dati autonomi che non possiedono alcuna associazione a un assembly [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] eseguibile.  
  
 Un'importante distinzione da fare tra questi tre tipi di file riguarda il fatto che i file di risorse e i file di dati sono resi noti in fase di compilazione, pertanto sono conosciuti esplicitamente da un assembly.  Nel caso dei file del sito di origine, invece, è possibile che un assembly non ne abbia alcuna conoscenza oppure che ne abbia una conoscenza implicita tramite un riferimento all'[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] di tipo pack. In quest'ultimo caso, non vi è alcuna garanzia che il file del sito di origine a cui si fa riferimento sia effettivamente esistente.  
  
 Per fare riferimento ai file di dati dell'applicazione, [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] utilizza lo schema [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] di tipo pack, descritto dettagliatamente in [URI di tipo pack in WPF](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md).  
  
 In questo argomento viene illustrato come configurare e utilizzare i file di dati dell'applicazione.  
  
   
  
<a name="Resource_Files"></a>   
## File di risorse  
 Se un file di dati deve sempre essere disponibile per un'applicazione, l'unico modo per garantire la disponibilità è compilarlo nell'assembly eseguibile principale dell'applicazione o in uno degli assembly a cui si fa riferimento.  Questo tipo di file di dati dell'applicazione è noto come *file di risorse*.  
  
 I file di risorse devono essere utilizzati nei seguenti casi:  
  
-   Non occorre aggiornare il contenuto del file di risorse dopo la relativa compilazione in un assembly.  
  
-   Si desidera semplificare la complessità di distribuzione dell'applicazione riducendo il numero di dipendenze dei file.  
  
-   Il file di dati dell'applicazione deve essere localizzabile \(vedere [Cenni preliminari sulla globalizzazione e localizzazione WPF](../../../../docs/framework/wpf/advanced/wpf-globalization-and-localization-overview.md)\).  
  
> [!NOTE]
>  I file di risorse descritti in questa sezione sono diversi dai file di risorse descritti in [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md) e diverso da quello delle risorse incorporate o collegate descritte in  [Gestione delle risorse delle applicazioni \(.NET\)](../Topic/Managing%20Application%20Resources%20\(.NET\).md).  
  
### Configurazione dei file di risorse  
 In [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], un file di risorse è un file incluso in un progetto [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)] come elemento `Resource`.  
  
```  
<Project "xmlns=http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Resource Include="ResourceFile.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  Per creare un file di risorse in [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)], occorre aggiungere un file a un progetto e impostare `Build Action` su `Resource`.  
  
 Quando il progetto viene compilato, [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] compila la risorsa nell'assembly.  
  
### Utilizzo dei file di risorse  
 Per caricare un file di risorse è possibile chiamare il metodo <xref:System.Windows.Application.GetResourceStream%2A> della classe <xref:System.Windows.Application>, passando un [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] di tipo pack che identifica il file di risorse desiderato.  <xref:System.Windows.Application.GetResourceStream%2A> restituisce un oggetto <xref:System.Windows.Resources.StreamResourceInfo>, il quale espone il file di risorse come <xref:System.IO.Stream> e ne descrive il tipo di contenuto.  
  
 Nel codice di esempio seguente viene illustrato come utilizzare <xref:System.Windows.Application.GetResourceStream%2A> per caricare un file di risorse <xref:System.Windows.Controls.Page> e impostarlo come contenuto di un oggetto <xref:System.Windows.Controls.Frame> \(`pageFrame`\):  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadapageresourcefilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadapageresourcefilemanuallycode)]  
  
 Sebbene la chiamata a <xref:System.Windows.Application.GetResourceStream%2A> consenta di accedere a <xref:System.IO.Stream>, è necessario eseguire un'operazione aggiuntiva di conversione nel tipo della proprietà con la quale verrà impostato.  In alternativa, è possibile fare in modo che [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] apra e converta <xref:System.IO.Stream> caricando un file di risorse direttamente nella proprietà di un tipo tramite codice.  
  
 Nell'esempio seguente viene illustrato come caricare <xref:System.Windows.Controls.Page> direttamente in <xref:System.Windows.Controls.Frame> \(`pageFrame`\) tramite codice.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadpageresourcefilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadpageresourcefilefromcode)]  
  
 Nell'esempio che segue viene illustrato il markup equivalente del precedente esempio.  
  
 [!code-xml[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml#loadpageresourcefilefromxaml)]  
  
### File di codice dell'applicazione come file di risorse  
 Tramite [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] di tipo pack è possibile fare riferimento a uno speciale insieme di file di codice dell'applicazione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], il quale include finestre, pagine, documenti dinamici e dizionari risorse.  Ad esempio, è possibile impostare la proprietà <xref:System.Windows.Application.StartupUri%2A?displayProperty=fullName> con un [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] di tipo pack che fa riferimento alla finestra o alla pagina che si desidera caricare all'avvio di un'applicazione.  
  
 [!code-xml[WPFAssemblyResourcesSnippets#SetApplicationStartupURI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/App.xaml#setapplicationstartupuri)]  
  
 Questa operazione può essere eseguita quando un file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è incluso in un progetto [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)] come elemento `Page`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Page Include="MainWindow.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  In [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)], se si aggiunge un nuovo oggetto <xref:System.Windows.Window>, <xref:System.Windows.Navigation.NavigationWindow>, <xref:System.Windows.Controls.Page>, <xref:System.Windows.Documents.FlowDocument> o <xref:System.Windows.ResourceDictionary> a un progetto, per impostazione predefinita `Build Action` per il file di markup viene impostata su `Page`.  
  
 Quando si compila un progetto con elementi `Page`, gli elementi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] vengono convertiti nel formato binario e compilati nell'assembly associato.  Di conseguenza, questi file possono essere utilizzati allo stesso modo dei file di risorse tipici.  
  
> [!NOTE]
>  Se un file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] viene configurato come elemento `Resource` e non possiede un file code\-behind, sarà il codice [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] non elaborato a essere compilato in un assembly e non una versione binaria dello stesso.  
  
<a name="Content_Files"></a>   
## File di dati  
 Un *file di dati* viene distribuito come file separato insieme a un assembly eseguibile.  Sebbene questi file non vengano compilati in un assembly, dal canto loro gli assembly vengono compilati con i metadati che stabiliscono un'associazione con ciascun file di dati.  
  
 È necessario utilizzare i file di dati quando l'applicazione richiede un insieme specifico di file di dati che possono essere aggiornati senza dover ricompilare l'assembly che li utilizza.  
  
### Configurazione dei file di dati  
 Per aggiungere un file di dati a un progetto, è necessario che un file di dati dell'applicazione sia incluso in un elemento `Content`.  Inoltre, dal momento che un file di dati non viene compilato direttamente nell'assembly, è necessario impostare l'elemento di metadati [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)]```CopyToOutputDirectory` per specificare che il file di dati viene copiato in un percorso relativo all'assembly compilato.  Per fare in modo che la risorsa venga copiata nella cartella dell'output di compilazione ogni qualvolta un progetto viene compilato, impostare l'elemento di metadati `CopyToOutputDirectory` con il valore `Always`.  In alternativa, è possibile fare in modo che solo la versione più recente della risorsa venga copiata nella cartella dell'output di compilazione utilizzando il valore `PreserveNewest`.  
  
 Di seguito viene illustrato un file configurato come file di dati, il quale viene copiato nella cartella dell'output di compilazione soltanto quando una nuova versione della risorsa viene aggiunta al progetto.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Content Include="ContentFile.xaml">  
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
    </Content>  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  Per creare un file di dati in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)], occorre aggiungere un file a un progetto e impostare `Build Action` su `Content`, quindi impostare `Copy to Output Directory` su `Copy always` \(equivalente a `Always`\) e `Copy if newer` \(equivalente a `PreserveNewest`\).  
  
 Quando il progetto viene compilato, per ogni file di dati viene compilato un attributo <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> nei metadati dell'assembly.  
  
 `[assembly: AssemblyAssociatedContentFile("ContentFile.xaml")]`  
  
 Il valore di <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> implica il percorso del file di dati relativo alla posizione nel progetto.  Ad esempio, se un file di dati si trovasse in una sottocartella del progetto, le informazioni sul percorso aggiuntive verrebbero incorporate nel valore <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>.  
  
 `[assembly: AssemblyAssociatedContentFile("Resources/ContentFile.xaml")]`  
  
 Il valore di <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> è anche il valore del percorso del file di dati nella cartella dell'output di compilazione.  
  
### Utilizzo dei file di dati  
 Per caricare un file di dati è possibile chiamare il metodo <xref:System.Windows.Application.GetContentStream%2A> della classe <xref:System.Windows.Application>, passando un [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] di tipo pack che identifica il file di dati desiderato.  <xref:System.Windows.Application.GetContentStream%2A> restituisce un oggetto <xref:System.Windows.Resources.StreamResourceInfo>, il quale espone il file di dati come <xref:System.IO.Stream> e ne descrive il tipo di contenuto.  
  
 Nel codice di esempio seguente viene illustrato come utilizzare <xref:System.Windows.Application.GetContentStream%2A> per caricare un file di dati <xref:System.Windows.Controls.Page> e impostarlo come contenuto di un oggetto <xref:System.Windows.Controls.Frame> \(`pageFrame`\).  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadapagecontentfilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadapagecontentfilemanuallycode)]  
  
 Sebbene la chiamata a <xref:System.Windows.Application.GetContentStream%2A> consenta di accedere a <xref:System.IO.Stream>, è necessario eseguire un'operazione aggiuntiva di conversione nel tipo della proprietà con la quale verrà impostato.  In alternativa, è possibile fare in modo che [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] apra e converta <xref:System.IO.Stream> caricando un file di risorse direttamente nella proprietà di un tipo tramite codice.  
  
 Nell'esempio seguente viene illustrato come caricare <xref:System.Windows.Controls.Page> direttamente in <xref:System.Windows.Controls.Frame> \(`pageFrame`\) tramite codice.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadpagecontentfilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadpagecontentfilefromcode)]  
  
 Nell'esempio che segue viene illustrato il markup equivalente del precedente esempio.  
  
 [!code-xml[WPFAssemblyResourcesSnippets#LoadPageContentFileFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml#loadpagecontentfilefromxaml)]  
  
<a name="Site_of_Origin_Files"></a>   
## File del sito di origine  
 I file di risorse hanno una relazione esplicita con gli assembly con i quali vengono distribuiti, come definito da <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>.  Talvolta, però, è possibile che si debba stabilire una relazione implicita o inesistente tra un assembly e un file di dati dell'applicazione, ad esempio nei seguenti casi:  
  
-   Un file non esiste in fase di compilazione.  
  
-   I file richiesti dall'assembly non saranno noti fino alla fase di esecuzione.  
  
-   Si vuole avere la possibilità di aggiornare i file senza ricompilare l'assembly al quale sono associati.  
  
-   L'applicazione utilizza file di dati di grandi dimensioni, ad esempio audio e video, che devono essere scaricati dagli utenti unicamente su richiesta.  
  
 È possibile caricare questi tipi di file utilizzando schemi [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] tradizionali, quali ad esempio gli schemi file:\/\/\/ e http:\/\/.  
  
 [!code-xml[WPFAssemblyResourcesSnippets#AbsolutePackUriFileHttpReferenceXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/AbsolutePackUriPage.xaml#absolutepackurifilehttpreferencexaml)]  
  
 Tuttavia, gli schemi file:\/\/\/ e http:\/\/ richiedono che l'applicazione abbia un livello di attendibilità totale.  Se l'applicazione è un'[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] avviata da Internet o Intranet e richiede soltanto l'insieme di autorizzazioni consentite per le applicazioni avviate da tali percorsi, i file separati possono essere caricati unicamente dal sito di origine dell'applicazione \(percorso di avvio\).  I file di questo tipo sono noti come file del *sito di origine*.  
  
 I file del sito di origine rappresentano l'unica opzione per le applicazioni parzialmente attendibili, benché non siano limitati a questo tipo di applicazione.  È possibile che le applicazioni completamente attendibili debbano caricare file di dati dell'applicazione sconosciuti in fase di compilazione. Sebbene queste applicazioni possano utilizzare file:\/\/\/, è probabile che i file di dati dell'applicazione vengano installati nella stessa cartella dell'assembly dell'applicazione o in una sottocartella di questo.  In questo caso è più facile utilizzare un riferimento al sito di origine piuttosto che file:\/\/\/, poiché l'utilizzo di file:\/\/\/ richiede l'elaborazione del percorso completo del file.  
  
> [!NOTE]
>  Al contrario dei file di dati, i file del sito di origine non vengono memorizzati nella cache con un'[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] in un computer client.  Di conseguenza vengono scaricati solo se esplicitamente richiesto.  Se un'[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] possiede file multimediali di grandi dimensioni, configurandoli come file del sito di origine l'avvio iniziale dell'applicazione sarà molto più rapido e i file verranno scaricati solo su richiesta.  
  
### Configurazione dei file del sito di origine  
 Se i file del sito di origine sono inesistenti o sconosciuti in fase di compilazione, è necessario utilizzare meccanismi di distribuzione tradizionali per assicurare che i file necessari siano disponibili in fase di esecuzione. Tali meccanismi includono il programma della riga di comando `XCopy` e [!INCLUDE[TLA#tla_wininstall](../../../../includes/tlasharptla-wininstall-md.md)].  
  
 Se in fase di compilazione si conoscono i file da collocare nel sito di origine, ma si vuole comunque evitare una dipendenza esplicita, è possibile aggiungere tali file a un progetto [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)] come elemento `None`.  Come per i file di dati, è necessario impostare l'attributo `CopyToOutputDirectory` [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] per specificare che il file del sito di origine viene copiato in un percorso relativo all'assembly compilato, specificando il valore `Always` o `PreserveNewest`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <None Include="PageSiteOfOriginFile.xaml">  
    <CopyToOutputDirectory>Always</CopyToOutputDirectory>  
  </None>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  Per creare un file del sito di origine in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)], occorre aggiungere un file a un progetto e impostare `Build Action` su `None`.  
  
 Quando il progetto viene compilato, [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] copia i file specificati nella cartella dell'output di compilazione.  
  
### Utilizzo dei file del sito di origine  
 Per caricare un file del sito di origine è possibile chiamare il metodo <xref:System.Windows.Application.GetRemoteStream%2A> della classe <xref:System.Windows.Application>, passando un [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] di tipo pack che identifica il file del sito di origine desiderato.  <xref:System.Windows.Application.GetRemoteStream%2A> restituisce un oggetto <xref:System.Windows.Resources.StreamResourceInfo>, il quale espone il file del sito di origine come <xref:System.IO.Stream> e ne descrive il tipo di contenuto.  
  
 Nel codice di esempio seguente viene illustrato come utilizzare <xref:System.Windows.Application.GetRemoteStream%2A> per caricare un file del sito di origine <xref:System.Windows.Controls.Page> e impostarlo come contenuto di un oggetto <xref:System.Windows.Controls.Frame> \(`pageFrame`\).  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadapagesoofilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadapagesoofilemanuallycode)]  
  
 Sebbene la chiamata a <xref:System.Windows.Application.GetRemoteStream%2A> consenta di accedere a <xref:System.IO.Stream>, è necessario eseguire un'operazione aggiuntiva di conversione nel tipo della proprietà con la quale verrà impostato.  In alternativa, è possibile fare in modo che [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] apra e converta <xref:System.IO.Stream> caricando un file di risorse direttamente nella proprietà di un tipo tramite codice.  
  
 Nell'esempio seguente viene illustrato come caricare <xref:System.Windows.Controls.Page> direttamente in <xref:System.Windows.Controls.Frame> \(`pageFrame`\) tramite codice.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadpagesoofilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadpagesoofilefromcode)]  
  
 Nell'esempio che segue viene illustrato il markup equivalente del precedente esempio.  
  
 [!code-xml[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml#loadpagesoofilefromxaml)]  
  
<a name="Rebuilding_after_Changing_Build_Type"></a>   
## Ricompilazione in seguito a modifica del tipo di compilazione  
 Dopo avere modificato il tipo di compilazione di un file di dati dell'applicazione, è necessario ricompilare l'intera applicazione affinché le modifiche vengano applicate.  Se ci si limita a compilare l'applicazione, le modifiche non vengono applicate.  
  
## Vedere anche  
 [URI di tipo pack in WPF](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)