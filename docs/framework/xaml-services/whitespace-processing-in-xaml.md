---
title: "Whitespace Processing in XAML | Microsoft Docs"
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
  - "East Asian characters [XAML Services]"
  - "XAML [XAML Services], whitespace processing"
  - "whitespace processing in XAML [XAML Services]"
  - "characters [XAML Services], East Asian"
ms.assetid: cc9cc377-7544-4fd0-b65b-117b90bb0b23
caps.latest.revision: 20
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 19
---
# Whitespace Processing in XAML
Le regole del linguaggio per XAML definiscono la modalità di elaborazione degli spazi vuoti significativi tramite l'implementazione di un processore [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]. In questo argomento vengono illustrate queste regole del linguaggio XAML, nonché la gestione degli spazi vuoti aggiuntivi definita dall'implementazione [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] del processore XAML e del writer XAML per la serializzazione.  
  
<a name="whitespace_definition"></a>   
## Definizione di spazio vuoto  
 Coerentemente con [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)] gli spazi vuoti in [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] sono costituiti da spazi, caratteri di avanzamento riga e di tabulazione. Questi corrispondono per rispettivamente ai valori [!INCLUDE[TLA#tla_unicode](../../../includes/tlasharptla-unicode-md.md)] 0020, 000A e 0009.  
  
<a name="whitespace_normalization"></a>   
## Normalizzazione degli spazi vuoti  
 Per impostazione predefinita, quando un processore [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] elabora un file [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)], viene eseguita la normalizzazione degli spazi vuoti come illustrato di seguito:  
  
1.  I caratteri di avanzamento riga inseriti tra i caratteri dell'Asia orientale vengono rimossi. Per una definizione dei "caratteri dell'Asia orientale", vedere la sezione relativa più avanti in questo argomento.  
  
2.  Tutti gli spazi vuoti \(spazi, avanzamento riga, tabulazioni\) vengono convertiti in spazi.  
  
3.  Tutti gli spazi consecutivi vengono eliminati e sostituiti da un unico spazio.  
  
4.  Uno spazio immediatamente successivo al tag di inizio viene eliminato.  
  
5.  Uno spazio immediatamente precedente al tag di fine viene eliminato.  
  
 L'"impostazione predefinita" corrisponde allo stato indicato dal valore predefinito dell'attributo [XML:space](../../../docs/framework/xaml-services/xml-space-handling-in-xaml.md).  
  
<a name="whitespace_in_inner_text_and_string_primitives"></a>   
## Spazi vuoti nel testo interno e primitive di stringa  
 Le regole di normalizzazione precedenti si applicano al testo interno presente negli elementi XAML. Dopo la normalizzazione, un processore XAML converte qualsiasi testo interno in un tipo appropriato come illustrato di seguito:  
  
-   Se il tipo della proprietà non è una raccolta, ma non è nemmeno un tipo <xref:System.Object>, il processore XAML tenta di eseguire la conversione a quel tipo usando il convertitore dei tipi. Una conversione non riuscita causa un errore in fase di compilazione.  
  
-   Se il tipo della proprietà è una raccolta e il testo interno è contiguo, \(non sono frapposti tag di elementi\), il testo interno viene analizzato come singolo oggetto <xref:System.String>. Se il tipo di raccolta non accetta <xref:System.String>, anche in questo caso si verifica un errore in fase di compilazione.  
  
-   Se il tipo della proprietà è <xref:System.Object>, il testo interno viene analizzato come un singolo oggetto <xref:System.String>. Se sono frapposti tag di elementi, viene generato un errore in fase di compilazione, in quanto il tipo <xref:System.Object> implica un solo oggetto \(<xref:System.String> o diverso\).  
  
-   Se il tipo della proprietà è una raccolta e il testo interno non è contiguo, la prima sottostringa viene convertita in un oggetto <xref:System.String> e aggiunta come elemento della raccolta. Quindi l'elemento frapposto sarà aggiunto come elemento della raccolta e infine la sottostringa finale \(se presente\) verrà aggiunta alla raccolta come terzo elemento <xref:System.String>.  
  
<a name="preserving_whitespace"></a>   
## Conservazione degli spazi vuoti  
 Esistono diverse tecniche che consentono di mantenere gli spazi vuoti nel codice [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] di origine in modo che non siano soggetti alla normalizzazione degli spazi vuoti del processore [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] per la presentazione conclusiva.  
  
 **xml:space\="preserve"**: specificare questo attributo al livello dell'elemento in cui si vogliono conservare gli spazi vuoti. Vengono così mantenuti tutti gli spazi vuoti, inclusi gli spazi che potrebbero essere aggiunti dalle applicazioni di modifica del codice per allineare gli elementi in modo ottimale, come nidificazione visivamente intuitiva. Tuttavia, il rendering di tali spazi dipende ancora una volta dal modello di contenuto per l'elemento contenitore. Evitare di specificare `xml:space="preserve"` al livello radice, perché la maggior parte dei modelli a oggetti non considera gli spazi vuoti come significativi, indipendentemente dalla modalità di impostazione dell'attributo. L'impostazione `xml:space` globalmente può avere conseguenze sulle prestazioni dell'elaborazione XAML, in particolare la serializzazione, in alcune implementazioni. Si consiglia piuttosto di impostare l'attributo specificamente al livello degli elementi che eseguono il rendering degli spazi vuoti all'interno delle stringhe o che costituiscono raccolte significative di spazi vuoti.  
  
 **Entità e spazi unificatori**: [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] supporta il posizionamento di qualsiasi entità [!INCLUDE[TLA#tla_unicode](../../../includes/tlasharptla-unicode-md.md)] all'interno di un modello di testo a oggetti. È possibile usare entità dedicate quali gli spazi unificatori \(& \#160; nella codifica UTF\-8\). È anche possibile usare controlli rich text che supportano caratteri spazio unificatore. È necessario prestare molta attenzione se si usano entità per simulare caratteristiche di layout, ad esempio il rientro, in quanto l'output di runtime delle entità varierà in base a un maggior numero di fattori rispetto alle funzionalità per ottenere i risultati di rientro in un sistema di layout tipico, ad esempio l'utilizzo corretto di pannelli e margini. Ad esempio, viene eseguito il mapping delle entità ai tipi di carattere, pertanto le dimensioni possono cambiare in funzione della selezione del tipo di carattere operata dall'utente.  
  
<a name="east_asian_characters"></a>   
## Caratteri dell'Asia orientale  
 I "caratteri dell'Asia orientale" vengono definiti come un set di caratteri [!INCLUDE[TLA2#tla_unicode](../../../includes/tla2sharptla-unicode-md.md)] compresi tra U\+20000 a U\+2FFFD e tra U\+30000 a U\+3FFFD. Questo sottoinsieme talvolta è denominato anche "ideogrammi CJK". Per altre informazioni, vedere [http:\/\/www.unicode.org](http://www.unicode.org/).  
  
<a name="whitespace_and_text_content_models"></a>   
## Spazi vuoti e modelli di contenuto di testo  
 In pratica, la conservazione degli spazi vuoti riguarda solo un sottoinsieme di tutti i possibili modelli di contenuto. Tale sottoinsieme è composto dai modelli di contenuto che accettano un tipo <xref:System.String> Singleton in una determinata forma, una raccolta <xref:System.String> dedicata o una combinazione di <xref:System.String> e di altri tipi in un raccolta <xref:System.Collections.IList> o <xref:System.Collections.Generic.ICollection%601>.  
  
### Spazi vuoti e modelli di contenuto del testo in WPF  
 Per scopo illustrativo, nella restante parte di questa sezione viene fatto riferimento a tipi particolari definiti da WPF. Le funzionalità di gestione degli spazi vuoti descritti in questo argomento sono generalmente pertinenti ai servizi XAML di .NET Framework e a WPF. Per una dimostrazione di questo comportamento, potrebbe essere utile provare a usare parti del markup XAML di WPF, osservare i risultati prodotti in un oggetto grafico, quindi indirizzare di nuovo la serializzazione al markup.  
  
 Anche per i modelli di contenuto che accettano le stringhe, il comportamento predefinito all'interno di tali modelli prevede che tutti gli spazi vuoti rimanenti non siano trattati come significativi. Ad esempio, <xref:System.Windows.Controls.ListBox> accetta un <xref:System.Collections.IList>, ma lo spazio vuoto \(ad esempio i caratteri di avanzamento riga tra ogni <xref:System.Windows.Controls.ListBoxItem>\) non viene mantenuto e non viene sottoposto a rendering. Se si tenta di usare i caratteri di avanzamento riga come separatori tra le stringhe per elementi <xref:System.Windows.Controls.ListBoxItem> l'esito sarà negativo; le stringhe separate dai caratteri di avanzamento riga sono considerate come una singola stringa e un singolo elemento.  
  
 Le raccolte che trattano gli spazi vuoti come significativi sono in genere parte del modello di documento dinamico. La raccolta primaria che supporta il comportamento di mantenimento degli spazi vuoti è <xref:System.Windows.Documents.InlineCollection>. Questa classe di raccolte viene dichiarata con <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>; una volta trovato questo attributo, il processore [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] tratterà gli spazi vuoti all'interno della raccolta come significativi. La combinazione di `xml:space="preserve"` e spazio vuoto all'interno di una raccolta specificata da <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> implica che tutti gli spazi vuoti vengono mantenuti e sottoposti a rendering. La combinazione di `xml:space="default"` e spazio vuoto all'interno di un oggetto <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> comporta la normalizzazione degli spazi vuoti iniziali descritta in precedenza, mediante la quale viene mantenuto uno spazio vuoto in determinate posizioni e tali spazi sono conservati e sottoposti a rendering. Sarà l'utente a decidere il comportamento più appropriato e a usare `xml:space` in maniera selettiva per abilitare il comportamento desiderato.  
  
 Inoltre, determinati elementi inline che implicano un'interruzione di riga in un modello di documento dinamico devono evitare l'introduzione di uno spazio aggiuntivo persino in una raccolta significativa di spazi vuoti. L'elemento <xref:System.Windows.Documents.LineBreak>, ad esempio, ha la stessa funzione del tag \<BR\/\> in [!INCLUDE[TLA2#tla_html](../../../includes/tla2sharptla-html-md.md)] e in genere per migliorare la leggibilità del markup, un oggetto <xref:System.Windows.Documents.LineBreak> è separato dal testo successivo tramite la creazione di un carattere di avanzamento riga. Tale avanzamento riga non deve essere normalizzato per l'utilizzo come spazio iniziale nella riga successiva. Per abilitare questo comportamento, alla definizione della classe per l'elemento <xref:System.Windows.Documents.LineBreak> viene applicato l'oggetto <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>, che viene quindi interpretato dal processore [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] per indicare che quello spazio vuoto che circonda <xref:System.Windows.Documents.LineBreak> sarà sempre tagliato.  
  
## Vedere anche  
 [Panoramica di XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [XML Character Entities and XAML](../../../docs/framework/xaml-services/xml-character-entities-and-xaml.md)   
 [xml:space Handling in XAML](../../../docs/framework/xaml-services/xml-space-handling-in-xaml.md)