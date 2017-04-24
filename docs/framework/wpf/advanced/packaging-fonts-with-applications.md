---
title: "Creazione di un package di tipi di carattere tramite applicazioni | Microsoft Docs"
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
  - "applicazioni, assemblaggio di tipi di carattere"
  - "tipi di carattere, assemblaggio con applicazioni"
  - "assemblaggio di tipi di carattere con applicazioni"
  - "tipografia, assemblaggio di tipi di carattere con applicazioni"
ms.assetid: db15ee48-4d24-49f5-8b9d-a64460865286
caps.latest.revision: 29
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# Creazione di un package di tipi di carattere tramite applicazioni
In questo argomento vengono forniti cenni preliminari su come creare un package di tipi di carattere con l'applicazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
> [!NOTE]
>  Come accade con la maggior parte dei software, i file dei tipi di carattere vengono concessi in licenza anziché venduti.  Le licenze che regolano l'utilizzo dei tipi di carattere variano in base al fornitore, ma in generale la maggior parte delle licenze, incluse quelle relative ai tipi di carattere [!INCLUDE[TLA#tla_ms#initcap](../../../../includes/tlasharptla-mssharpinitcap-md.md)], viene fornita con le applicazioni e [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] non consente di incorporare i tipi di carattere all'interno delle applicazioni o di ridistribuirli in altro modo.  Pertanto, è responsabilità dello sviluppatore accertarsi di disporre dei diritti di licenza necessari per qualsiasi tipo di carattere incorporato all'interno di un'applicazione o ridistribuito in altro modo.  
  
   
  
<a name="introduction_to_packaging_fonts"></a>   
## Introduzione alla creazione di package di tipi di carattere  
 È possibile creare package dei tipi di carattere come risorse all'interno delle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] al fine di visualizzare il testo dell'interfaccia utente e altri tipi di contenuto basato sul testo.  I tipi di carattere possono essere separati dai file di assembly dell'applicazione oppure incorporati all'interno di questi ultimi.  È inoltre possibile creare una libreria di tipi di carattere di sole risorse alla quale l'applicazione può fare riferimento.  
  
 I tipi di carattere [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] e [!INCLUDE[TLA#tla_truetype](../../../../includes/tlasharptla-truetype-md.md)] contengono un flag di tipo, fsType, che indica i diritti di licenza per l'incorporamento dei tipi di carattere per il tipo di carattere.  Tuttavia, questo flag di tipo si riferisce solo ai tipi di carattere incorporati archiviati in un documento, non a quelli incorporati in un'applicazione.  È possibile recuperare i diritti di incorporamento dei tipi di carattere per un tipo di carattere creando un oggetto <xref:System.Windows.Media.GlyphTypeface> e facendo riferimento alla relativa proprietà <xref:System.Windows.Media.GlyphTypeface.EmbeddingRights%2A>.  Per ulteriori informazioni sul flag fsType, fare riferimento alla sezione relativa alla metrica di OS\/2 e di Windows della specifica [OpenType Specification](http://www.microsoft.com/typography/otspec/os2.htm) \(informazioni in lingua inglese\).  
  
 Sul sito Web [Microsoft Typography](http://www.microsoft.com/typography/links/) \(informazioni in lingua inglese\) sono incluse informazioni sui contatti che consentono di individuare il fornitore di un particolare tipo di carattere oppure un fornitore per un lavoro personalizzato.  
  
<a name="adding_fonts_as_content_items"></a>   
## Aggiunta di tipi di carattere come elementi di contenuto  
 È possibile aggiungere tipi di carattere all'applicazione come elementi di contenuto del progetto separati dai file di assembly dell'applicazione.  Ciò significa che gli elementi di contenuto non sono incorporati come risorse all'interno di un assembly.  Nell'esempio di file di progetto seguente viene mostrata la modalità di definizione degli elementi di contenuto.  
  
```  
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Content Include="Peric.ttf" />  
    <Content Include="Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
 Per assicurare che l'applicazione sia in grado di utilizzare i tipi di carattere in fase di esecuzione, è necessario garantire l'accesso ai tipi di carattere nella directory di distribuzione dell'applicazione.  L'elemento `<CopyToOutputDirectory>` del file di progetto dell'applicazione consente di copiare automaticamente i tipi di carattere nella directory di distribuzione dell'applicazione durante il processo di compilazione.  Nell'esempio di file di progetto seguente viene mostrato come copiare i tipi di carattere nella directory di distribuzione.  
  
```  
<ItemGroup>  
  <Content Include="Peric.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
  <Content Include="Pericl.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
</ItemGroup>  
```  
  
 Nell'esempio di codice seguente viene mostrato come fare riferimento al tipo di carattere dell'applicazione come elemento di contenuto. L'elemento di contenuto al quale si fa riferimento deve trovarsi nella stessa directory dei file di assembly dell'applicazione.  
  
 [!code-xml[FontSnippets#FontPackageSnippet8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet8)]  
  
<a name="adding_fonts_as_resource_items"></a>   
## Aggiunta di tipi di carattere come elementi di risorsa  
 È possibile aggiungere i tipi di carattere all'applicazione come elementi di risorsa del progetto incorporati nei file di assembly dell'applicazione.  L'utilizzo di una sottodirectory separata per le risorse consente di organizzare i file di progetto dell'applicazione.  Nell'esempio di file di progetto seguente viene mostrato come definire i tipi di carattere come elementi di risorsa in una sottodirectory separata..  
  
```  
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Resource Include="resources\Peric.ttf" />  
    <Resource Include="resources\Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
> [!NOTE]
>  Quando si aggiungono dei tipi di carattere come risorse all'applicazione, assicurarsi di impostare l'elemento `<Resource>`, non l'elemento `<EmbeddedResource>` nel file di progetto dell'applicazione.  L'elemento `<EmbeddedResource>` per l'azione di compilazione non è supportato.  
  
 Nell'esempio di markup seguente viene mostrato come fare riferimento alle risorse dei tipi di carattere dell'applicazione.  
  
 [!code-xml[FontSnippets#FontPackageSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet1)]  
  
### Riferimento agli elementi di risorsa dei tipi di carattere dal codice  
 Per fare riferimento agli elementi di risorsa dei tipi di carattere dal codice è necessario fornire un riferimento alla risorsa dei tipi di carattere che sia composto da due parti: l'[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] di base e il riferimento di percorso del tipo di carattere.  Tali valori vengono utilizzati come parametri per il metodo <xref:System.Windows.Media.FontFamily.%23ctor%2A>.  Nell'esempio di codice seguente viene mostrato come fare riferimento alle risorse dei tipi di carattere dell'applicazione nella sottodirectory del progetto denominata `resources`.  
  
 [!code-csharp[FontSnippets#FontPackageSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet2)]
 [!code-vb[FontSnippets#FontPackageSnippet2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet2)]  
  
 L'[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] di base può includere la sottodirectory dell'applicazione in cui risiede la risorsa del tipo di carattere.  In questo caso, non è necessario che il riferimento di percorso del tipo di carattere specifichi una directory; tuttavia è necessario che includa un "`./`" iniziale che indica che la risorsa del tipo di carattere si trova nella stessa directory specificata dall'[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] di base.  Nell'esempio di codice seguente viene mostrato un modo alternativo per fare riferimento all'elemento della risorsa del tipo di carattere. Il codice è equivalente all'esempio di codice precedente.  
  
 [!code-csharp[FontSnippets#FontPackageSnippet5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet5)]
 [!code-vb[FontSnippets#FontPackageSnippet5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet5)]  
  
### Riferimento a tipi di carattere della stessa sottodirectory dell'applicazione  
 È possibile collocare il contenuto dell'applicazione e i file di risorse all'interno della stessa sottodirectory definita dall'utente all'interno del progetto dell'applicazione.  Nell'esempio di file di progetto seguente viene mostrata un pagina di contenuto e le risorse dei tipi di carattere definite nella stessa sottodirectory.  
  
```  
<ItemGroup>  
  <Page Include="pages\HomePage.xaml" />  
</ItemGroup>  
<ItemGroup>  
  <Resource Include="pages\Peric.ttf" />  
  <Resource Include="pages\Pericl.ttf" />  
</ItemGroup>  
```  
  
 Poiché il contenuto dell'applicazione e il tipo di carattere si trovano nella stessa sottodirectory, il riferimento del tipo di carattere è relativo al contenuto dell'applicazione.  Negli esempi seguenti viene mostrato come fare riferimento alla risorsa del tipo di carattere dell'applicazione quando il tipo di carattere si trova nella stessa directory dell'applicazione.  
  
 [!code-xml[FontSnippets#FontPackageSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml#fontpackagesnippet3)]  
  
 [!code-csharp[FontSnippets#FontPackageSnippet4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml.cs#fontpackagesnippet4)]
 [!code-vb[FontSnippets#FontPackageSnippet4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/pages/homepage.xaml.vb#fontpackagesnippet4)]  
  
### Enumerazione dei tipi di carattere in un'applicazione  
 Per enumerare i tipi di carattere come elementi di risorsa nell'applicazione, utilizzare il metodo <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> o il metodo <xref:System.Windows.Media.Fonts.GetTypefaces%2A>.  Nell'esempio seguente viene mostrato come utilizzare il metodo <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> per restituire la raccolta di oggetti <xref:System.Windows.Media.FontFamily> dal percorso dei tipi di carattere dell'applicazione.  In questo caso, l'applicazione contiene una sottodirectory denominata "resources".  
  
 [!code-csharp[FontSnippets#FontsSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet3)]
 [!code-vb[FontSnippets#FontsSnippet3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet3)]  
  
 Nell'esempio seguente viene mostrato come utilizzare il metodo <xref:System.Windows.Media.Fonts.GetTypefaces%2A> per restituire la raccolta di oggetti <xref:System.Windows.Media.Typeface> dal percorso dei tipi di carattere dell'applicazione.  In questo caso, l'applicazione contiene una sottodirectory denominata "resources".  
  
 [!code-csharp[FontSnippets#FontsSnippet7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet7)]
 [!code-vb[FontSnippets#FontsSnippet7](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet7)]  
  
<a name="creating_a_font_resource_library"></a>   
## Creazione di una libreria di risorse dei tipi di carattere  
 È possibile creare una libreria di sole risorse contenente unicamente tipi di carattere. Questo tipo di progetto di libreria non contiene alcun codice.  La creazione di una libreria di sole risorse è una tecnica comune per separare le risorse dal codice dell'applicazione che le utilizza.  Tale tecnica consente inoltre di includere più progetti di applicazione nell'assembly di librerie.  Nell'esempio di file di progetto seguente vengono mostrate le sezioni principali di un progetto di libreria di sole risorse.  
  
```  
<PropertyGroup>  
  <AssemblyName>FontLibrary</AssemblyName>  
  <OutputType>library</OutputType>  
  ...  
</PropertyGroup>  
...  
<ItemGroup>  
  <Resource Include="Kooten.ttf" />  
  <Resource Include="Pesca.ttf" />  
</ItemGroup  
```  
  
### Riferimento a un tipo di carattere in una libreria di risorse  
 Per fare riferimento a un tipo di carattere in una libreria di risorse dall'applicazione è necessario aggiungere il nome dell'assembly di librerie come prefisso al riferimento del tipo di carattere.  In questo caso, l'assembly di risorse del tipo di carattere è "FontLibrary".  Per separare il nome dell'assembly dal riferimento all'interno dell'assembly utilizzare un carattere ';'.  L'aggiunta della parola chiave "Component" seguita dal riferimento al nome del tipo di carattere consente di fornire il riferimento completo alla risorsa della libreria dei tipi di carattere.  Nell'esempio di codice seguente viene mostrato come fare riferimento a un tipo di carattere in un assembly di librerie della risorsa.  
  
 [!code-xml[OpenTypeFontsSample#OpenTypeFontsSample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontsSample/CS/Kootenay.xaml#opentypefontssample1)]  
  
> [!NOTE]
>  Il presente SDK contiene una serie di tipi di carattere [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] di esempio che è possibile utilizzare con le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  I tipi di carattere sono definiti in una libreria di sole risorse.  Per ulteriori informazioni, vedere [Esempio di pacchetto di tipi di carattere OpenType](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md).  
  
<a name="limitations_on_font_usage"></a>   
## Limitazioni dell'utilizzo dei tipi di carattere  
 Nell'elenco seguente sono indicate diverse limitazioni relative alla creazione di package di tipi di caratteri e al relativo utilizzo nelle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
-   **Bit di autorizzazione per l'incorporamento dei tipi di carattere:** le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non controllano né applicano bit di autorizzazione per l'incorporamento dei tipi di carattere.  Per ulteriori informazioni, vedere la sezione [Introduzione\_alla creazione\_di package di tipi di carattere](#introduction_to_packaging_fonts).  
  
-   **Sito dei tipi di carattere di origine:** le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non consentono un riferimento del tipo di carattere a un [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] http o ftp  
  
-   **URI assoluto che utilizza la notazione pack:**  le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non consentono la creazione di un oggetto <xref:System.Windows.Media.FontFamily> a livello di codice mediante la notazione "pack:" come parte del riferimento all'[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] assoluto per un tipo di carattere.  Ad esempio, `"pack://application:,,,/resources/#Pericles Light"` è un riferimento del tipo di carattere non valido.  
  
-   **Incorporamento automatico dei tipi di carattere:** durante la fase di progettazione, non esiste alcun supporto per la ricerca dell'utilizzo dei tipi di carattere di un'applicazione e per l'incorporamento automatico dei tipi di carattere nelle risorse dell'applicazione.  
  
-   **Sottoinsiemi di tipi di carattere:** le applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non supportano la creazione di sottoinsiemi di tipi di carattere per i documenti non statici.  
  
-   Nei casi in cui esista un riferimento errato, l'applicazione ricorre all'utilizzo di un tipo di carattere disponibile.  
  
## Vedere anche  
 <xref:System.Windows.Documents.Typography>   
 <xref:System.Windows.Media.FontFamily>   
 [Microsoft Typography: collegamenti, notizie e contatti](http://www.microsoft.com/typography/links/)   
 [Specifiche OpenType](http://www.microsoft.com/typography/otspec/)   
 [Funzionalità dei tipi di carattere OpenType](../../../../docs/framework/wpf/advanced/opentype-font-features.md)   
 [Esempio di pacchetto di tipi di carattere OpenType](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md)