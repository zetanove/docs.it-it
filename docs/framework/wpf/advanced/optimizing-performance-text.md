---
title: "Ottimizzazione delle prestazioni: testo | Microsoft Docs"
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
  - "rendering di testo"
  - "collegamenti ipertestuali"
  - "testo formattato [WPF]"
  - "testo, delle prestazioni"
  - "icone"
ms.assetid: 66b1b9a7-8618-48db-b616-c57ea4327b98
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Ottimizzazione delle prestazioni: testo
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]include il supporto per la presentazione del contenuto di testo tramite l'utilizzo e ricco di funzionalità [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] controlli. In generale è possibile dividere il rendering del testo nei tre livelli:  
  
1.  Utilizzo di <xref:System.Windows.Documents.Glyphs> e <xref:System.Windows.Media.GlyphRun> direttamente gli oggetti.  
  
2.  Utilizzo di <xref:System.Windows.Media.FormattedText> oggetto.  
  
3.  Utilizzando i controlli di livello elevato, ad esempio il <xref:System.Windows.Controls.TextBlock> e <xref:System.Windows.Documents.FlowDocument> oggetti.  
  
 In questo argomento fornisce testo consigli relativi alle prestazioni di rendering.  
  
   
  
<a name="Glyph_Level"></a>   
## <a name="rendering-text-at-the-glyph-level"></a>Il rendering del testo a livello di glifo  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]fornisce il supporto di testo avanzato incluso il markup a livello di glifo con accesso diretto alla <xref:System.Windows.Documents.Glyphs> per i clienti che desiderano intercettare e salvare in modo permanente il testo dopo la formattazione. Queste funzionalità forniscono supporto critico per il testo diversi requisiti per il rendering in ognuno dei seguenti scenari.  
  
-   Visualizzazione dei documenti a formato fisso.  
  
-   Scenari di stampa.  
  
    -   [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]come un linguaggio della stampante.  
  
    -   [!INCLUDE[TLA#tla_mxdw](../../../../includes/tlasharptla-mxdw-md.md)].  
  
    -   Driver della stampante precedenti, l'output di [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] applicazioni in formato fisso.  
  
    -   Formato dello spool di stampa.  
  
-   Rappresentazione di documenti con formato fisso, inclusi i client per le versioni precedenti di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] e altri dispositivi di elaborazione.  
  
> [!NOTE]
>  <xref:System.Windows.Documents.Glyphs> e <xref:System.Windows.Media.GlyphRun> sono progettati per la presentazione di documenti a formato fisso e scenari di stampa. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]vengono forniti diversi elementi per il layout generale e [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] scenari, ad esempio <xref:System.Windows.Controls.Label> e <xref:System.Windows.Controls.TextBlock>. Per ulteriori informazioni sul layout e [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] scenari, vedere il [funzionalità tipografiche di WPF](../../../../docs/framework/wpf/advanced/typography-in-wpf.md).  
  
 Negli esempi seguenti viene illustrano come definire le proprietà per un <xref:System.Windows.Documents.Glyphs> oggetto [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]. Il <xref:System.Windows.Documents.Glyphs> oggetto rappresenta l'output di un <xref:System.Windows.Media.GlyphRun> in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. Negli esempi si presuppone che i tipi di carattere Arial, Courier New e Times New Roman siano installati nel **C:\WINDOWS\Fonts** cartella nel computer locale.  
  
 [!code-xml[GlyphsOvwSample1#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSample1/CS/default.xaml#1)]  
  
### <a name="using-drawglyphrun"></a>Utilizzo di DrawGlyphRun  
 Se si dispone di un controllo personalizzato e si desidera per il rendering dei glifi, utilizzare il <xref:System.Windows.Media.DrawingContext.DrawGlyphRun%2A> metodo.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]sono inoltre disponibili servizi di basso livello per la formattazione personalizzata mediante l'utilizzo di <xref:System.Windows.Media.FormattedText> oggetto. La soluzione più efficace per il rendering del testo in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] è costituito dalla generazione del contenuto di testo a livello di glifo utilizzando <xref:System.Windows.Documents.Glyphs> e <xref:System.Windows.Media.GlyphRun>. Tuttavia, il costo di questa efficienza è la perdita di facile da usare il formato RTF, funzionalità incorporate di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] controlli, ad esempio <xref:System.Windows.Controls.TextBlock> e <xref:System.Windows.Documents.FlowDocument>.  
  
<a name="FormattedText_Object"></a>   
## <a name="formattedtext-object"></a>Oggetto FormattedText  
 Il <xref:System.Windows.Media.FormattedText> oggetto consente di disegnare testo su più righe in cui ogni carattere del testo può essere formattato singolarmente. Per ulteriori informazioni, vedere [del testo in formato disegno](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md).  
  
 Per creare il testo formattato, chiamare il <xref:System.Windows.Media.FormattedText.%23ctor%2A> costruttore per creare un <xref:System.Windows.Media.FormattedText> oggetto. Dopo aver creato la stringa di testo formattato iniziale, è possibile applicare una gamma di stili di formattazione. Se l'applicazione deve implementare un layout personalizzato, il <xref:System.Windows.Media.FormattedText> oggetto è la scelta migliore rispetto all'utilizzo di un controllo, ad esempio <xref:System.Windows.Controls.TextBlock>. Per ulteriori informazioni sul <xref:System.Windows.Media.FormattedText> di oggetti, vedere [del testo in formato disegno](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md) .  
  
 Il <xref:System.Windows.Media.FormattedText> oggetto fornisce funzionalità di formattazione del testo di basso livello. È possibile applicare vari stili di formattazione per uno o più caratteri. Ad esempio, è possibile chiamare entrambi il <xref:System.Windows.Media.FormattedText.SetFontSize%2A> e <xref:System.Windows.Media.FormattedText.SetForegroundBrush%2A> metodi per modificare la formattazione dei primi cinque caratteri del testo.  
  
 L'esempio di codice seguente crea un <xref:System.Windows.Media.FormattedText> dell'oggetto e ne esegue il rendering.  
  
 [!code-csharp[formattedtextsnippets#FormattedTextSnippets1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FormattedTextSnippets/CSharp/Window1.xaml.cs#formattedtextsnippets1)]
 [!code-vb[formattedtextsnippets#FormattedTextSnippets1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FormattedTextSnippets/visualbasic/window1.xaml.vb#formattedtextsnippets1)]  
  
<a name="FlowDocument_TextBlock_Label"></a>   
## <a name="flowdocument-textblock-and-label-controls"></a>FlowDocument, TextBlock e controlli etichetta  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]include più controlli per il disegno di testo sullo schermo. Ogni controllo è destinato a uno scenario diverso e ha un proprio elenco di funzionalità e limitazioni.  
  
### <a name="flowdocument-impacts-performance-more-than-textblock-or-label"></a>FlowDocument influisce sulle prestazioni più di TextBlock o Label  
 In generale, il <xref:System.Windows.Controls.TextBlock> elemento deve essere utilizzato quando il supporto limitato del testo è richiesto, ad esempio una frase breve in un [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]. <xref:System.Windows.Controls.Label> può essere utilizzato quando è richiesto il supporto minimo del testo. Il <xref:System.Windows.Documents.FlowDocument> elemento è un contenitore per i documenti rinnovabile che supportano la presentazione dettagliata del contenuto e pertanto, ha un impatto maggiore sulle prestazioni rispetto all'utilizzo di <xref:System.Windows.Controls.TextBlock> o <xref:System.Windows.Controls.Label> controlli.  
  
 Per ulteriori informazioni su <xref:System.Windows.Documents.FlowDocument>, vedere [Flow Document Overview](../../../../docs/framework/wpf/advanced/flow-document-overview.md).  
  
### <a name="avoid-using-textblock-in-flowdocument"></a>Evitare di utilizzare TextBlock in FlowDocument  
 Il <xref:System.Windows.Controls.TextBlock> elemento deriva da <xref:System.Windows.UIElement>. Il <xref:System.Windows.Documents.Run> elemento deriva da <xref:System.Windows.Documents.TextElement>, che è meno costoso da utilizzare rispetto a un <xref:System.Windows.UIElement>-oggetto derivato. Quando possibile, utilizzare <xref:System.Windows.Documents.Run> anziché <xref:System.Windows.Controls.TextBlock> per visualizzare il contenuto di testo in un <xref:System.Windows.Documents.FlowDocument>.  
  
 Nell'esempio di codice seguente illustra due modalità di impostazione del contenuto di testo all'interno di un <xref:System.Windows.Documents.FlowDocument>:  
  
 [!code-xml[Performance#PerformanceSnippet13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/FlowDocument.xaml#performancesnippet13)]  
  
### <a name="avoid-using-run-to-set-text-properties"></a>Evitare di utilizzare il comando Esegui per impostare le proprietà di testo  
 In generale, utilizzando un <xref:System.Windows.Documents.Run> all'interno di un <xref:System.Windows.Controls.TextBlock> è prestazioni più elevato rispetto al mancato utilizzo esplicita <xref:System.Windows.Documents.Run> oggetto affatto. Se si utilizza un <xref:System.Windows.Documents.Run> per impostare le proprietà di testo, impostare tali proprietà direttamente nel <xref:System.Windows.Controls.TextBlock> invece.  
  
 Nell'esempio di codice seguente illustra questi due metodi per impostare una proprietà di testo, in questo caso, il <xref:System.Windows.Controls.TextBlock.FontWeight%2A> proprietà:  
  
 [!code-xml[Performance#PerformanceSnippet12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml#performancesnippet12)]  
  
 Nella tabella seguente vengono mostrati i costi della visualizzazione di 1000 <xref:System.Windows.Controls.TextBlock> oggetti con e senza l'esplicita <xref:System.Windows.Documents.Run>.  
  
|**Tipo di TextBlock**|**Ora di creazione (ms)**|**Eseguire il rendering di tempo (ms)**|  
|------------------------|------------------------------|----------------------------|  
|Eseguire l'impostazione delle proprietà di testo|146|540|  
|Impostazione delle proprietà di testo TextBlock|43|453|  
  
### <a name="avoid-databinding-to-the-labelcontent-property"></a>Evitare l'associazione dati alla proprietà Label. Content  
 Si immagini uno scenario in cui è necessario un <xref:System.Windows.Controls.Label> oggetto che è stato aggiornato di frequente da un <xref:System.String> origine. Quando l'associazione dati di <xref:System.Windows.Controls.Label> dell'elemento <xref:System.Windows.Controls.ContentControl.Content%2A> proprietà per il <xref:System.String> origine oggetto, si verifichi un peggioramento delle prestazioni. Ogni volta che l'origine <xref:System.String> viene aggiornato, il vecchio <xref:System.String> oggetto viene ignorato e un nuovo <xref:System.String> viene ricreata, perché un <xref:System.String> oggetto non è modificabile, non può essere modificata. A sua volta, determinando così il <xref:System.Windows.Controls.ContentPresenter> di <xref:System.Windows.Controls.Label> per eliminare il contenuto precedente e rigenerare il nuovo contenuto per visualizzare il nuovo oggetto <xref:System.String>.  
  
 Per risolvere questo problema è semplice. Se il <xref:System.Windows.Controls.Label> non è impostata su un oggetto personalizzato <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> valore, sostituire il <xref:System.Windows.Controls.Label> con un <xref:System.Windows.Controls.TextBlock> e associare i dati relativi <xref:System.Windows.Controls.TextBlock.Text%2A> proprietà alla stringa di origine.  
  
|**Proprietà con associazione a dati**|**Ora di aggiornamento (ms)**|  
|-----------------------------|----------------------------|  
|Label. Content|835|  
|TextBlock. Text|242|  
  
<a name="Hyperlink"></a>   
## <a name="hyperlink"></a>Collegamento ipertestuale  
 Il <xref:System.Windows.Documents.Hyperlink> oggetto è un elemento di contenuto del flusso di livello inline che consente di ospitare collegamenti ipertestuali all'interno del contenuto di flusso.  
  
### <a name="combine-hyperlinks-in-one-textblock-object"></a>Combinare collegamenti ipertestuali in un oggetto TextBlock  
 È possibile ottimizzare l'utilizzo di più <xref:System.Windows.Documents.Hyperlink> elementi raggruppandoli insieme all'interno dello stesso <xref:System.Windows.Controls.TextBlock>. Ciò consente di ridurre al minimo il numero di oggetti creati nell'applicazione. Potrebbe ad esempio, si desidera visualizzare più collegamenti ipertestuali, ad esempio le operazioni seguenti:  
  
 Home page di MSN | My MSN  
  
 Nell'esempio di codice seguente viene illustrato più <xref:System.Windows.Controls.TextBlock> elementi utilizzati per visualizzare i collegamenti ipertestuali:  
  
 [!code-xml[Performance#PerformanceSnippet9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet9)]  
  
 Nell'esempio di codice seguente viene illustrato un modo più efficiente per visualizzare i collegamenti ipertestuali, l'utilizzo di un singolo <xref:System.Windows.Controls.TextBlock>:  
  
 [!code-xml[Performance#PerformanceSnippet10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet10)]  
  
### <a name="showing-underlines-on-hyperlinks-only-on-mouseenter-events"></a>Visualizzazione delle sottolineature nei collegamenti ipertestuali solo sugli eventi MouseEnter  
 Oggetto <xref:System.Windows.TextDecoration> oggetto è rappresenta ornamenti visivi che è possibile aggiungere testo, tuttavia, può essere prestazioni intensive da creare. Se si usano ampiamente <xref:System.Windows.Documents.Hyperlink> elementi, provare a visualizzare un carattere di sottolineatura solo al momento della generazione di un evento, ad esempio il <xref:System.Windows.ContentElement.MouseEnter> evento. Per ulteriori informazioni, vedere [specificare se un collegamento ipertestuale è sottolineato](../../../../docs/framework/wpf/advanced/how-to-specify-whether-a-hyperlink-is-underlined.md).  
  
 ![Collegamenti ipertestuali con TextDecoration](../../../../docs/framework/wpf/advanced/media/textdecoration03.png "TextDecoration03")  
Collegamento ipertestuale sul MouseEnter  
  
 Nell'esempio di codice seguente viene illustrato un <xref:System.Windows.Documents.Hyperlink> definito con e senza un carattere di sottolineatura:  
  
 [!code-xml[Performance#PerformanceSnippet11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet11)]  
  
 Nella tabella seguente viene illustrato l'impatto sulle prestazioni della visualizzazione di 1000 <xref:System.Windows.Documents.Hyperlink> elementi con e senza un carattere di sottolineatura.  
  
|**Collegamento ipertestuale**|**Ora di creazione (ms)**|**Eseguire il rendering di tempo (ms)**|  
|-------------------|------------------------------|----------------------------|  
|Con carattere di sottolineatura|289|1130|  
|Senza carattere di sottolineatura|299|776|  
  
<a name="Text_Formatting_Features"></a>   
## <a name="text-formatting-features"></a>Funzionalità di formattazione del testo  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]fornisce servizi, ad esempio sillabazione proposta automatica RTF. Questi servizi possono influire sulle prestazioni dell'applicazione e devono essere utilizzati solo quando necessario.  
  
### <a name="avoid-unnecessary-use-of-hyphenation"></a>Evitare l'utilizzo non necessario di sillabazione  
 La sillabazione automatica vengono trattino dei punti di interruzione per le righe di testo e consente di posizioni di interruzione aggiuntive per le righe in <xref:System.Windows.Controls.TextBlock> e <xref:System.Windows.Documents.FlowDocument> oggetti. Per impostazione predefinita, la funzionalità di sillabazione automatica è disabilitata in questi oggetti. È possibile abilitare questa funzionalità impostando la proprietà dell'oggetto IsHyphenationEnabled su `true`. Tuttavia, abilitando questa funzionalità, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per avviare [!INCLUDE[TLA#tla_com](../../../../includes/tlasharptla-com-md.md)] l'interoperabilità, che può influire sulle prestazioni dell'applicazione. È consigliabile non utilizzare la sillabazione automatica a meno che non è necessaria.  
  
### <a name="use-figures-carefully"></a>Utilizzare con attenzione le cifre  
 Oggetto <xref:System.Windows.Documents.Figure> elemento rappresenta una parte del contenuto del flusso che può essere posizionata all'interno di una pagina di contenuto. In alcuni casi, un <xref:System.Windows.Documents.Figure> può causare un'intera pagina riformattare automaticamente se la posizione è in conflitto con il contenuto che è già stato disposto. È possibile ridurre la possibilità di riformattazione non necessaria per un raggruppamento di <xref:System.Windows.Documents.Figure> elementi accanto a altro oppure dichiarandoli accanto all'inizio del contenuto in uno scenario di dimensioni di pagina fisse.  
  
### <a name="optimal-paragraph"></a>Paragrafo ottimale  
 La funzionalità di paragrafo ottimale di <xref:System.Windows.Documents.FlowDocument> oggetto dispone i paragrafi in modo che gli spazi vuoti vengano distribuiti quanto più possibile uniforme. Per impostazione predefinita, la funzionalità di paragrafo ottimale è disabilitata. È possibile abilitare questa funzionalità impostando l'oggetto <xref:System.Windows.Documents.FlowDocument.IsOptimalParagraphEnabled%2A> proprietà `true`. Tuttavia, l'abilitazione di questa funzionalità influisce sulle prestazioni dell'applicazione. È consigliabile non utilizzare la funzionalità di paragrafo ottimale a meno che non è necessaria.  
  
## <a name="see-also"></a>Vedere anche  
 [Ottimizzazione delle prestazioni dell'applicazione WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [Pianificazione per le prestazioni dell'applicazione](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [Sfruttando i vantaggi dell'Hardware](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Creazione di immagini ed elementi grafici&2;D](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Comportamento degli oggetti](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Risorse dell'applicazione](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)