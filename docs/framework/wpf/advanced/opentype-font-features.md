---
title: "Funzionalit&#224; dei tipi di carattere OpenType | Microsoft Docs"
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
  - "tipi di carattere OpenType"
  - "tipografia, la tecnologia di carattere OpenType"
  - "OpenType (tecnologia dei tipi di carattere)"
ms.assetid: 4061a9d1-fe8b-4921-9e17-18ec7d2e3ea2
caps.latest.revision: 38
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 37
---
# Funzionalit&#224; dei tipi di carattere OpenType
In questo argomento viene fornita una panoramica di alcune delle principali funzionalità di [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] tecnologia in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
   
  
<a name="overview"></a>   
## <a name="opentype-font-format"></a>Formato di carattere OpenType  
 Il [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] il formato del carattere è un'estensione del [!INCLUDE[TLA#tla_truetype](../../../../includes/tlasharptla-truetype-md.md)] formato carattere, aggiungendo il supporto per i dati di tipo di carattere PostScript. Il [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] il formato del carattere è stato sviluppato congiuntamente da [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] e Adobe Corporation. [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]tipi di carattere e il sistema operativo di servizi che supportano [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] tipi di carattere forniscono agli utenti un modo semplice di installare e utilizzare tipi di carattere, se contengono i tipi di carattere [!INCLUDE[TLA2#tla_truetype](../../../../includes/tla2sharptla-truetype-md.md)] strutture o CFF (PostScript).  
  
 Il [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] il formato del carattere per affrontare le sfide per gli sviluppatori seguenti:  
  
-   Supporto multipiattaforma più ampio.  
  
-   Supporto migliorato per set di caratteri internazionali.  
  
-   Migliore protezione dei dati di tipo di carattere.  
  
-   File di dimensioni inferiori per rendere più efficiente la distribuzione di tipo di carattere.  
  
-   Un più ampio supporto per il controllo tipografico avanzato.  
  
> [!NOTE]
>  Windows SDK contiene un set di esempio [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] i tipi di carattere che è possibile utilizzare con [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] applicazioni. Questi tipi di carattere forniscono la maggior parte delle funzionalità illustrate nella parte restante di questo argomento. Per ulteriori informazioni, vedere [Sample OpenType Font Pack](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md).  
  
 Vedere il [specifica OpenType](http://go.microsoft.com/fwlink/?LinkId=96731) per informazioni dettagliate di [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] il formato del carattere.  
  
### <a name="advanced-typographic-extensions"></a>Estensioni tipografiche avanzate  
 Le tabelle tipografiche avanzate ([!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] tabelle Layout) estendono le funzionalità di carattere con [!INCLUDE[TLA2#tla_truetype](../../../../includes/tla2sharptla-truetype-md.md)] o CFF. [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]Tipi di carattere layout contengono informazioni aggiuntive che estendono le funzionalità dei tipi di carattere per il supporto tipografico internazionale di alta qualità. La maggior parte dei [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] tipi di carattere espone solo un subset del totale [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] le funzionalità disponibili. [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]tipi di carattere forniscono le funzionalità seguenti.  
  
-   Numerosi mapping tra i caratteri e glifi che supportano legature, forme posizionali, alternative e altre sostituzioni del carattere.  
  
-   Supporto per l'allegato glifo e posizionamento bidimensionale.  
  
-   Script e della lingua informazioni esplicite contenute nel tipo di carattere, quindi un'applicazione di elaborazione di testo possa modificare il comportamento di conseguenza.  
  
 Il [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] tabelle Layout sono descritti più dettagliatamente il ["Font File Tables"](http://www.microsoft.com/typography/otspec/otff.htm) sezione del [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] specifica.  
  
 Il resto di questa panoramica introduce l'ampiezza e la flessibilità di alcune delle visivamente interessanti [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] funzionalità esposte dalle proprietà del <xref:System.Windows.Documents.Typography> oggetto. Per ulteriori informazioni su questo oggetto, vedere [classe tipografica](#typography_class).  
  
<a name="variants"></a>   
## <a name="variants"></a>Varianti  
 Le varianti vengono utilizzate per eseguire il rendering di stili tipografici diversi, ad esempio apici e pedici.  
  
### <a name="superscripts-and-subscripts"></a>Apici e pedici  
 Il <xref:System.Windows.Documents.Typography.Variants%2A> proprietà consente di impostare valori apici e pedici per un [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] tipo di carattere.  
  
 Il testo seguente vengono visualizzati gli apici per il tipo di carattere Palatino Linotype.  
  
 ![Testo con apici OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont14.png "opentypefont14")  
Testo con apici OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire gli apici per il tipo di carattere Palatino Linotype, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#12)]  
  
 Il testo seguente vengono visualizzati i pedici per il tipo di carattere Palatino Linotype.  
  
 ![Testo con pedici OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont15.png "opentypefont15")  
Testo con pedici OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire i pedici per il tipo di carattere Palatino Linotype, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#13)]  
  
### <a name="decorative-uses-of-superscripts-and-subscripts"></a>Utilizzi decorativi di apici e pedici  
 È inoltre possibile utilizzare apici e pedici per creare effetti decorativi del testo case. Il testo seguente visualizza testo apice e pedice per il tipo di carattere Palatino Linotype. Si noti che le lettere maiuscole non sono interessate.  
  
 ![Testo con apici e pedici OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont16.png "opentypefont16")  
Testo con apici e pedici OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire gli apici e pedici per un tipo di carattere, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#14)]  
  
<a name="capitals"></a>   
## <a name="capitals"></a>Lettere maiuscole  
 Le lettere maiuscole sono un set di caratteri tipografici che il rendering del testo nei glifi di stile maiuscolo. In genere, quando viene eseguito il rendering di testo come tutte le lettere maiuscole, la spaziatura tra le lettere può risultare troppo ridotta e lo spessore e la proporzione delle lettere troppo elevate. [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]supporta numerosi formati di stili per le lettere maiuscole, inclusi maiuscoletto, maiuscoletto ridotto, titoli e spaziatura tra caratteri maiuscoli. Questi formati stilistici consentono di controllare l'aspetto di lettere maiuscole.  
  
 Il testo seguente consente di visualizzare le lettere maiuscole standard per il tipo di carattere Pescadero, seguite dalle lettere con stile "SmallCaps" e "AllSmallCaps". In questo caso, la stessa dimensione del carattere viene utilizzata per tutte le tre parole.  
  
 ![Testo con caratteri maiuscoli OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont11.png "opentypefont11")  
Testo con caratteri maiuscoli OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire le maiuscole per il tipo di carattere Pescadero, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto. Quando viene utilizzato il formato "SmallCaps", le lettere maiuscole iniziali viene ignorata.  
  
 [!code-xml[OpenTypeFontSamples#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#9)]  
  
### <a name="titling-capitals"></a>Le maiuscole  
 Queste lettere sono più chiaro in proporzione e il peso e progettato per conferire un aspetto più elegante rispetto alle maiuscole normali. Queste lettere vengono in genere utilizzate in caratteri di dimensioni maggiori come intestazioni. Il testo seguente consente di visualizzare le maiuscole normale e per i titoli per il tipo di carattere Pescadero. Si noti gli spessore delle aste del testo nella seconda riga.  
  
 ![Testo con caratteri maiuscoli per i titoli OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont20.png "OpenTypeFont20")  
Testo con caratteri maiuscoli per i titoli OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire le maiuscole per il tipo di carattere Pescadero, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet17](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet17)]  
  
### <a name="capital-spacing"></a>Spaziatura tra caratteri maiuscoli  
 Spaziatura tra caratteri maiuscoli è una funzionalità che consente di ottenere una maggiore spaziatura quando si utilizza tutte le lettere maiuscole nel testo. Lettere maiuscole in genere sono progettate per essere utilizzate con la lettera minuscola. Spaziatura appropriata tra una lettera maiuscola e minuscola può risultare troppo ridotta quando vengono utilizzate le lettere maiuscole. Il testo seguente consente di visualizzare la spaziatura normale e capitale per il tipo di carattere Pescadero.  
  
 ![Testo con spaziatura tra caratteri maiuscoli OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont21.png "OpenTypeFont21")  
Testo con spaziatura tra caratteri maiuscoli OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire la spaziatura tra maiuscole per il tipo di carattere Pescadero, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet18](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet18)]  
  
<a name="ligatures"></a>   
## <a name="ligatures"></a>Legature  
 Legature sono due o più glifi che vengono trasformati in un singolo glifo per creare un testo più leggibile o gradevole. [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]tipi di carattere supportano quattro tipi di legature:  
  
-   **Legature standard**. Progettato per migliorare la leggibilità. Legature standard includono "fi", "fl" e "ff".  
  
-   **Legature contestuali**. Progettato per migliorare la leggibilità, fornendo un comportamento più join tra i caratteri che costituiscono l'alfabeto.  
  
-   **Legature discrezionali**. Progettato per essere ornamentali in modo specifico per migliorare la leggibilità.  
  
-   **Legature storiche**. Progettato per essere cronologici in modo specifico per migliorare la leggibilità.  
  
 Glifi di legature standard per il tipo di carattere Pericles verrà visualizzato il testo seguente.  
  
 ![Testo con legature standard OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont04.png "opentypefont04")  
Testo con legature standard OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire i glifi di legature standard per il tipo di carattere Pericles, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#4)]  
  
 Il testo seguente visualizza i glifi di legature discrezionali per il tipo di carattere Pericles.  
  
 ![Testo con legature discrezionali OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont05.png "opentypefont05")  
Testo con legature discrezionali OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire i glifi di legature discrezionali per il tipo di carattere Pericles, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#5)]  
  
 Per impostazione predefinita, [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] tipi di carattere in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] consentono legature standard. Ad esempio, se si utilizza il tipo di carattere Palatino Linotype, le legature standard "fi", "ff" e "fl" vengono visualizzati come un glifo di caratteri combinati. Si noti che la coppia di caratteri per ogni alfabeto standard contigui.  
  
 ![Testo con legature standard OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont06.png "opentypefont06")  
Testo con legature standard OpenType  
  
 Tuttavia, è possibile disabilitare questa funzionalità in modo che un alfabeto standard, ad esempio "ff" viene visualizzato come due glifi distinti, anziché come un glifo di caratteri combinati.  
  
 ![Testo con legature standard OpenType disabilitate](../../../../docs/framework/wpf/advanced/media/opentypefont07.png "opentypefont07")  
Testo con legature standard OpenType disabilitate  
  
 Nell'esempio di codice seguente viene illustrato come disabilitare i glifi di legature standard per il tipo di carattere Palatino Linotype, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#6)]  
  
<a name="swashes"></a>   
## <a name="swashes"></a>Caratteri ornati  
 I caratteri ornati sono glifi decorativi che utilizzano ornamenti elaborati spesso associato alla calligrafia. Glifi standard e ornati per il tipo di carattere Pescadero verrà visualizzato il testo seguente.  
  
 ![Testo con glifi standard e ornati OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont08.png "opentypefont08")  
Testo con glifi standard e ornati OpenType  
  
 Caratteri ornati vengono spesso utilizzati come elementi decorativi in frasi brevi, ad esempio annunci di eventi. Il testo seguente utilizza caratteri ornati per enfatizzare le lettere maiuscole del nome dell'evento.  
  
 ![Testo con caratteri ornati OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont09.png "opentypefont09")  
Testo con caratteri ornati OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire caratteri ornati per un tipo di carattere, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#7)]  
  
### <a name="contextual-swashes"></a>Caratteri ornati contestuali  
 Alcune combinazioni di glifi ornati possono causare un aspetto poco piacevole, ad esempio sovrapposizione del tratto discendente nelle lettere adiacenti. Utilizzando un ornati contestuali consente di utilizzare un glifo ornati sostitutivo che produce un aspetto migliore. Il testo seguente viene illustrata la stessa parola prima e dopo aver applicato un ornati contestuali.  
  
 ![Testo con caratteri ornati contestuali OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont19.png "OpenTypeFont19")  
Testo con caratteri ornati contestuali OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire un ornati contestuali per il tipo di carattere Pescadero, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet16)]  
  
<a name="alternates"></a>   
## <a name="alternates"></a>Alternative  
 Le alternative sono glifi che è possibile sostituire un glifo standard. [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]tipi di carattere, ad esempio il tipo di carattere Pericles utilizzato negli esempi seguenti, possono contenere glifi alternativi che è possibile utilizzare per creare aspetti diversi per il testo. Il testo seguente è riportati glifi standard per il tipo di carattere Pericles.  
  
 ![Testo con glifi standard OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont01.png "opentypefont01")  
Testo con glifi standard OpenType  
  
 Il Pericles [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] include glifi aggiuntivi che offrono alternative stilistiche all'insieme di glifi standard. Glifi di stile alternativo viene visualizzato il testo seguente.  
  
 ![Testo con glifi di stile alternativo OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont02.png "opentypefont02")  
Testo con glifi di stile alternativo OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire i glifi di stile alternativo per il tipo di carattere Pericles, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#2)]  
  
 Diversi altri glifi alternativi stilistici per il tipo di carattere Pericles verrà visualizzato il testo seguente.  
  
 ![Testo con glifi di stile alternativo OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont03.png "opentypefont03")  
Testo con glifi di stile alternativo OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire gli altri glifi alternativi stilistici.  
  
 [!code-xml[OpenTypeFontSamples#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#3)]  
  
### <a name="random-contextual-alternates"></a>Alternative contestuali casuali  
 Le alternative contestuali casuali forniscono più glifi sostitutivi per un singolo carattere. Quando viene implementato con caratteri di tipo script, questa funzionalità è possibile simulare grafia utilizzando un set di glifi scelti casualmente con piccole differenze nell'aspetto. Il testo seguente utilizza alternative contestuali casuali per il tipo di carattere Lindsey. Si noti che la lettera "a" varia leggermente nell'aspetto  
  
 ![Testo con alternative contestuali casuali OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont23.png "OpenTypeFont23")  
Testo con alternative contestuali casuali OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire le alternative contestuali casuali per il tipo di carattere Lindsey, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/Window1.xaml#opentypefontsnippet20)]  
  
### <a name="historical-forms"></a>Storico  
 Storico rappresentano convenzioni tipografiche comuni nel passato. La frase "Boston, Massachusetts", verrà visualizzato il testo seguente utilizzando un formato storico di glifi per il tipo di carattere Palatino Linotype.  
  
 ![Testo con formati di tipo storico OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont10.png "opentypefont10")  
Testo con formati di tipo storico OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire storico per il tipo di carattere Palatino Linotype, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#8)]  
  
<a name="numerical_styles"></a>   
## <a name="numerical-styles"></a>Stili numerici  
 Tipi di carattere OpenType supportano un numero elevato di funzionalità che può essere utilizzato con i valori numerici in formato testo.  
  
### <a name="fractions"></a>Frazioni di secondo  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]i tipi di carattere supportano gli stili per le frazioni di secondo, tra cui barrato e in pila.  
  
 Il testo seguente vengono illustrati gli stili per il tipo di carattere Palatino Linotype.  
  
 ![Testo con caratteri OpenType barra e frazioni sovrapposte](../../../../docs/framework/wpf/advanced/media/opentypefont12.png "opentypefont12")  
Testo con frazioni con la barra e frazioni sovrapposte OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire stili per il tipo di carattere Palatino Linotype, utilizzando le proprietà di frazioni di <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#10)]  
  
### <a name="old-style-numerals"></a>Stile antico  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]tipi di carattere supportano un formato numerico in stile antico. Questo formato è utile per la visualizzazione dei numerali negli stili che non sono più standard. Il testo seguente consente di visualizzare una data del XVIII secolo in formati standard e in stile antico per il tipo di carattere Palatino Linotype.  
  
 ![Testo con stile antico OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont24.png "OpenTypeFont24")  
Testo con caratteri numerici in stile antico OpenType  
  
 Il testo seguente visualizza i numeri standard per il tipo di carattere Palatino Linotype, seguiti da stile antico.  
  
 ![Testo set di caratteri numerici in stile antico OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont13.png "opentypefont13")  
Testo con set di caratteri numerici in stile antico OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire caratteri numerici in stile antico per il tipo di carattere Palatino Linotype, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#11)]  
  
### <a name="proportional-and-tabular-figures"></a>Cifre proporzionali e tabulari  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]tipi di carattere supportano una funzionalità proporzionali e tabulari per controllare l'allineamento delle larghezze quando si utilizzano caratteri numerici. Cifre proporzionali considerano ogni carattere numerico come dotato di una larghezza diversa, ovvero "1" è inferiore a "5". Le cifre tabulari vengono trattate come caratteri numerici di uguale larghezza in modo da consentirne l'allineamento verticale, che migliora la leggibilità delle informazioni di tipo finanziario.  
  
 Due cifre proporzionali viene visualizzato il seguente testo nella prima colonna utilizzando il tipo di carattere Miramonte. Si noti la differenza tra i caratteri numerici "5" e "1". La seconda colonna Mostra gli stessi due valori numerici con la larghezza regolata tramite la funzionalità tabulari.  
  
 ![Testo con cifre proporzionali / tabulari OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont22.png "OpenTypeFont22")  
Testo con cifre proporzionali e tabulari OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire le cifre proporzionali e tabulari per il tipo di carattere Miramonte, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/Window1.xaml#opentypefontsnippet19)]  
  
### <a name="slashed-zero"></a>Zero barrato  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)]tipi di carattere supportano un barrato formato numerico con zero per evidenziare la differenza tra la lettera "A" e il numero "0". Il barrato che zero viene spesso utilizzato per gli identificatori in informazioni finanziarie e aziendali.  
  
 Il testo seguente visualizza un identificatore di ordine di esempio utilizzando il tipo di carattere Miramonte. La prima riga utilizza caratteri numerici standard. La seconda riga utilizzata numerici con zero barrato per fornire un contrasto migliore con la lettera maiuscola "O".  
  
 ![Testo con caratteri OpenType numerici con zero barrato](../../../../docs/framework/wpf/advanced/media/opentypefont17.png "OpenTypeFont17")  
Testo con caratteri numerici con zero barrato OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire caratteri numerici con zero barrato per il tipo di carattere Miramonte, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto.  
  
 [!code-xml[OpenTypeFontSamples#OpenTypeFontSnippet15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#opentypefontsnippet15)]  
  
<a name="typography_class"></a>   
## <a name="typography-class"></a>Classe tipografica  
 Il <xref:System.Windows.Documents.Typography> oggetto espone il set di funzionalità che un [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] supporta tipi di carattere. Impostando le proprietà di <xref:System.Windows.Documents.Typography> nel markup, è possibile creare facilmente documenti che sfruttano [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] funzionalità.  
  
 Il testo seguente consente di visualizzare le lettere maiuscole standard per il tipo di carattere Pescadero, seguite dalle lettere con stile "SmallCaps" e "AllSmallCaps". In questo caso, la stessa dimensione del carattere viene utilizzata per tutte le tre parole.  
  
 ![Testo con caratteri maiuscoli OpenType](../../../../docs/framework/wpf/advanced/media/opentypefont11.png "opentypefont11")  
Testo con caratteri maiuscoli OpenType  
  
 Nell'esempio di codice seguente viene illustrato come definire le maiuscole per il tipo di carattere Pescadero, utilizzando le proprietà del <xref:System.Windows.Documents.Typography> oggetto. Quando viene utilizzato il formato "SmallCaps", le lettere maiuscole iniziali viene ignorata.  
  
 [!code-xml[OpenTypeFontSamples#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontSamples/CS/PageOne.xaml#9)]  
  
 L'esempio di codice seguente viene eseguita la stessa operazione dell'esempio di codice precedente.  
  
 [!code-csharp[TypographyCodeSnippets#TypographyCodeSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TypographyCodeSnippets/CSharp/Page1.xaml.cs#typographycodesnippet1)]
 [!code-vb[TypographyCodeSnippets#TypographyCodeSnippet1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TypographyCodeSnippets/visualbasic/page1.xaml.vb#typographycodesnippet1)]  
  
### <a name="typography-class-properties"></a>Proprietà della classe tipografica  
 Nella tabella seguente sono elencate le proprietà, valori e le impostazioni predefinite di <xref:System.Windows.Documents.Typography> oggetto.  
  
|Proprietà|O più valori|Valore predefinito|  
|--------------|----------------|-------------------|  
|<xref:System.Windows.Documents.Typography.AnnotationAlternates%2A>|Valore numerico - byte|0|  
|<xref:System.Windows.Documents.Typography.Capitals%2A>|<xref:System.Windows.FontCapitals> | <xref:System.Windows.FontCapitals> | <xref:System.Windows.FontCapitals> | <xref:System.Windows.FontCapitals> | <xref:System.Windows.FontCapitals> | <xref:System.Windows.FontCapitals> | <xref:System.Windows.FontCapitals>|<xref:System.Windows.FontCapitals?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.CapitalSpacing%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.CaseSensitiveForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.ContextualAlternates%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.ContextualLigatures%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.ContextualSwashes%2A>|Valore numerico - byte|0|  
|<xref:System.Windows.Documents.Typography.DiscretionaryLigatures%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.EastAsianExpertForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.EastAsianLanguage%2A>|<xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage> | <xref:System.Windows.FontEastAsianLanguage>|<xref:System.Windows.FontEastAsianLanguage?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.EastAsianWidths%2A>|<xref:System.Windows.FontEastAsianWidths> | <xref:System.Windows.FontEastAsianWidths> | <xref:System.Windows.FontEastAsianWidths> | <xref:System.Windows.FontEastAsianWidths> | <xref:System.Windows.FontEastAsianWidths> | <xref:System.Windows.FontEastAsianWidths>|<xref:System.Windows.FontEastAsianWidths?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.Fraction%2A>|<xref:System.Windows.FontFraction> | <xref:System.Windows.FontFraction> | <xref:System.Windows.FontFraction>|<xref:System.Windows.FontFraction?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.HistoricalForms%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.HistoricalLigatures%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.Kerning%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.MathematicalGreek%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.NumeralAlignment%2A>|<xref:System.Windows.FontNumeralAlignment> | <xref:System.Windows.FontNumeralAlignment> | <xref:System.Windows.FontNumeralAlignment>|<xref:System.Windows.FontNumeralAlignment?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.NumeralStyle%2A>|<xref:System.Boolean>|<xref:System.Windows.FontNumeralStyle?displayProperty=fullName>|  
|<xref:System.Windows.Documents.Typography.SlashedZero%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StandardLigatures%2A>|<xref:System.Boolean>|`true`|  
|<xref:System.Windows.Documents.Typography.StandardSwashes%2A>|valore numerico-byte|0|  
|<xref:System.Windows.Documents.Typography.StylisticAlternates%2A>|valore numerico-byte|0|  
|<xref:System.Windows.Documents.Typography.StylisticSet1%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet2%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet3%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet4%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet5%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet6%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet7%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet8%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet9%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet10%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet11%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet12%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet13%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet14%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet15%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet16%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet17%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet18%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet19%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.StylisticSet20%2A>|<xref:System.Boolean>|`false`|  
|<xref:System.Windows.Documents.Typography.Variants%2A>|<xref:System.Windows.FontVariants> | <xref:System.Windows.FontVariants> | <xref:System.Windows.FontVariants> | <xref:System.Windows.FontVariants> | <xref:System.Windows.FontVariants> | <xref:System.Windows.FontVariants>|<xref:System.Windows.FontVariants?displayProperty=fullName>|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Documents.Typography>   
 [Specifica OpenType](http://go.microsoft.com/fwlink/?LinkId=96731)   
 [Funzionalità tipografiche di WPF](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)   
 [Pacchetto di tipi di carattere OpenType di esempio](../../../../docs/framework/wpf/advanced/sample-opentype-font-pack.md)   
 [Caratteri di assemblaggio con applicazioni](../../../../docs/framework/wpf/advanced/packaging-fonts-with-applications.md)