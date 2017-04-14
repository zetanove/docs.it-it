---
title: "Formattazione del testo avanzata | Microsoft Docs"
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
  - "formattazione [WPF]"
  - "testo [WPF]"
  - "tipografia, testo (formattazione)"
ms.assetid: f0a7986e-f5b2-485c-a27d-f8e922022212
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Formattazione del testo avanzata
[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] fornisce un set di [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] molto efficace per includere testo nell'applicazione.  Il layout e le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] dell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)], ad esempio <xref:System.Windows.Controls.TextBlock>, forniscono gli elementi di utilizzo più comune e generale per la presentazione del testo.  Le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] di disegno, quali <xref:System.Windows.Media.GlyphRunDrawing> e <xref:System.Windows.Media.FormattedText>, consentono di includere il testo formattato nei disegni.  Al livello più avanzato, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce un motore di formattazione del testo estensibile per controllare qualsiasi aspetto della presentazione del testo, ad esempio la gestione degli archivi di testo, la gestione della formattazione di sequenze di testo e la gestione degli oggetti incorporati.  
  
 In questo argomento viene presentata un'introduzione alla formattazione del testo in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Vengono descritti in particolare l'implementazione del client e l'utilizzo del motore di formattazione del testo di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
> [!NOTE]
>  Tutti gli esempi di codice all'interno di questo documento sono disponibili in [Esempio di formattazione di testo avanzata](http://go.microsoft.com/fwlink/?LinkID=159965).  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="prereq"></a>   
## Prerequisiti  
 Questo argomento presuppone che l'utente abbia dimestichezza con le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] di livello più elevato utilizzate per la presentazione del testo.  La maggior parte degli scenari utente non richiede l'utilizzo delle [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] di formattazione del testo avanzata illustrate in questo argomento.  Per un'introduzione alle diverse [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] di testo, vedere [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md).  
  
<a name="section1"></a>   
## Formattazione del testo avanzata  
 Il layout del testo e i controlli dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] offrono proprietà di formattazione che consentono di includere facilmente un testo formattato nell'applicazione.  Questi controlli espongono numerose proprietà per la gestione della presentazione del testo, inclusi il carattere tipografico, le dimensioni e il colore.  In situazioni ordinarie, questi controlli sono in grado di gestire la maggior parte degli scenari di presentazione del testo nell'applicazione.  Tuttavia, alcuni scenari avanzati richiedono il controllo dell'archiviazione del testo e della presentazione del testo.  A tal fine, in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] viene fornito un motore di formattazione del testo estensibile.  
  
 Le funzionalità di formattazione del testo avanzata di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] sono costituite da un motore di formattazione del testo, da un archivio di testo, da sequenze di testo e da proprietà di formattazione.  Il motore di formattazione del testo, <xref:System.Windows.Media.TextFormatting.TextFormatter>, crea righe di testo da utilizzare per la presentazione.  Per effettuare questa operazione, è necessario avviare il processo di formattazione delle righe e chiamare l'oggetto <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> del formattatore di testo.  Il formattatore di testo recupera le sequenze di testo dall'archivio di testo chiamando il metodo <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> dell'archivio.  Gli oggetti <xref:System.Windows.Media.TextFormatting.TextRun> vengono quindi trasformati in oggetti <xref:System.Windows.Media.TextFormatting.TextLine> dal formattatore di testo e passati all'applicazione per l'ispezione o la visualizzazione.  
  
<a name="section2"></a>   
## Utilizzo del formattatore di testo  
 <xref:System.Windows.Media.TextFormatting.TextFormatter> è il motore di formattazione del testo di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] e fornisce servizi per la formattazione delle righe di testo e per l'inserimento di interruzioni di riga.  Il formattatore di testo può gestire diversi formati di carattere del testo e stili di paragrafo e include il supporto per il layout di testo internazionale.  
  
 A differenza di un [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] di testo tradizionale, l'oggetto <xref:System.Windows.Media.TextFormatting.TextFormatter> interagisce con un client di layout di testo tramite un insieme di metodi di callback.  È necessario che il client fornisca questi metodi in un'implementazione della classe <xref:System.Windows.Media.TextFormatting.TextSource>.  Nel seguente diagramma viene illustrata l'interazione di layout di testo tra l'applicazione client e <xref:System.Windows.Media.TextFormatting.TextFormatter>.  
  
 ![Diagramma del client del layout di testo e TextFormatter](../../../../docs/framework/wpf/advanced/media/textformatter01.png "TextFormatter01")  
Interazione tra l'applicazione e TextFormatter  
  
 Il formattatore di testo viene utilizzato per recuperare le righe del testo formattato dall'archivio di testo, che costituisce un'implementazione di <xref:System.Windows.Media.TextFormatting.TextSource>.  Questa operazione viene eseguita creando innanzitutto un'istanza del formattatore di testo tramite il metodo <xref:System.Windows.Media.TextFormatting.TextFormatter.Create%2A>.  Questo metodo crea un'istanza del formattatore di testo e imposta i valori massimi di altezza e larghezza della riga.  Una volta creata un'istanza del formattatore di testo, viene avviato il processo di creazione della riga tramite la chiamata al metodo <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A>.  L'oggetto <xref:System.Windows.Media.TextFormatting.TextFormatter> richiama l'origine del testo per recuperare il testo e i parametri di formattazione per le sequenze di testo che formano una riga.  
  
 Nell'esempio seguente, viene illustrato il processo di formattazione di un archivio di testo.  L'oggetto <xref:System.Windows.Media.TextFormatting.TextFormatter> viene utilizzato per recuperare le righe di testo dall'archivio di testo e formattare quindi la riga di testo per il disegno nell'oggetto <xref:System.Windows.Media.DrawingContext>.  
  
 [!code-csharp[TextFormatterExample#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextFormatterExample#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/Window1.xaml.vb#100)]  
  
<a name="section3"></a>   
## Implementazione dell'archivio di testo del client  
 Quando si estende il motore di formattazione del testo, è necessario implementare e gestire tutti gli aspetti dell'archivio di testo.  Non si tratta di un'attività elementare.  L'archivio di testo è responsabile del rilevamento delle proprietà delle sequenze di testo, delle proprietà dei paragrafi, degli oggetti incorporati e di altri contenuti simili.  Fornisce inoltre al formattatore di testo singoli oggetti <xref:System.Windows.Media.TextFormatting.TextRun> che il formattatore utilizza per creare oggetti <xref:System.Windows.Media.TextFormatting.TextLine>.  
  
 Per gestire la virtualizzazione dell'archivio di testo, quest'ultimo deve essere derivato da <xref:System.Windows.Media.TextFormatting.TextSource>.  <xref:System.Windows.Media.TextFormatting.TextSource> definisce il metodo utilizzato dal formattatore di testo per recuperare le sequenze di testo dall'archivio di testo.  <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> è il metodo che consente di recuperare le sequenze di testo utilizzate nella formattazione delle righe.  La chiamata a <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> viene effettuata ripetutamente dal formattatore di testo finché non si verifica una delle seguenti condizioni:  
  
-   Viene restituito un oggetto <xref:System.Windows.Media.TextFormatting.TextEndOfLine> o una sottoclasse.  
  
-   La larghezza complessiva delle sequenze di testo supera la larghezza massima della riga specificata nella chiamata per creare il formattatore di testo o nella chiamata al metodo <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> del formattatore di testo.  
  
-   Viene restituita una sequenza di nuova riga [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)], ad esempio "CF", "LF" o "CRLF".  
  
<a name="section4"></a>   
## Inserimento delle sequenze di testo  
 Il fulcro del processo di formattazione del testo è dato dall'interazione tra il formattatore di testo e l'archivio di testo.  L'implementazione di <xref:System.Windows.Media.TextFormatting.TextSource> fornisce al formattatore di testo gli oggetti <xref:System.Windows.Media.TextFormatting.TextRun> e le proprietà con cui formattare le sequenze di testo.  Questa interazione viene gestita dal metodo <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A>, chiamato dal formattatore di testo.  
  
 Nella tabella seguente sono riportati alcuni degli oggetti <xref:System.Windows.Media.TextFormatting.TextRun> predefiniti.  
  
|Tipo TextRun|Utilizzo|  
|------------------|--------------|  
|<xref:System.Windows.Media.TextFormatting.TextCharacters>|Sequenza di testo specializzata utilizzata per passare nuovamente al formattatore di testo una rappresentazione dei glifi dei caratteri.|  
|<xref:System.Windows.Media.TextFormatting.TextEmbeddedObject>|Sequenza di testo specializzata utilizzata per fornire un contenuto nel quale la misurazione, l'hit testing e il disegno vengono eseguite come un'unica operazione, ad esempio un pulsante o un'immagine all'interno del testo.|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfLine>|Sequenza di testo specializzata utilizzata per contrassegnare la fine di una riga.|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>|Sequenza di testo specializzata utilizzata per contrassegnare la fine di un paragrafo.|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfSegment>|Sequenza di testo specializzata utilizzata per contrassegnare la fine di un segmento, ad esempio per terminare l'ambito interessato da un'esecuzione precedente di <xref:System.Windows.Media.TextFormatting.TextModifier>.|  
|<xref:System.Windows.Media.TextFormatting.TextHidden>|Sequenza di testo specializzata utilizzata per contrassegnare un intervallo di caratteri nascosti.|  
|<xref:System.Windows.Media.TextFormatting.TextModifier>|Sequenza di testo specializzata utilizzata per modificare le proprietà delle sequenze di testo nel relativo ambito.  L'ambito si estende alla successiva sequenza di testo <xref:System.Windows.Media.TextFormatting.TextEndOfSegment> corrispondente o al successivo oggetto <xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>.|  
  
 Qualsiasi oggetto <xref:System.Windows.Media.TextFormatting.TextRun> predefinito può essere sottoclassato.  Ciò consente all'origine del testo di fornire al formattatore di testo sequenze di testo che includono dati personalizzati.  
  
 Nell'esempio seguente viene illustrato un metodo <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A>.  Questo archivio di testo restituisce oggetti <xref:System.Windows.Media.TextFormatting.TextRun> al formattatore di testo per l'elaborazione.  
  
 [!code-csharp[TextFormatterExample#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/CustomTextSource.cs#101)]
 [!code-vb[TextFormatterExample#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/CustomTextSource.vb#101)]  
  
> [!NOTE]
>  In questo esempio, l'archivio di testo fornisce a tutto il testo le stesse proprietà.  Gli archivi di testo avanzati devono implementare una gestione personalizzata dell'estensione in modo da consentire ai singoli caratteri di disporre di più proprietà.  
  
<a name="section5"></a>   
## Specifica delle proprietà di formattazione  
 Gli oggetti <xref:System.Windows.Media.TextFormatting.TextRun> vengono formattati utilizzando le proprietà fornite dall'archivio di testo.  Queste proprietà possono essere di due tipi, <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> e <xref:System.Windows.Media.TextFormatting.TextRunProperties>.  <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> gestisce le proprietà che interessano il paragrafo, quali <xref:System.Windows.TextAlignment> e <xref:System.Windows.FlowDirection>.  <xref:System.Windows.Media.TextFormatting.TextRunProperties> include proprietà che possono essere diverse per ciascuna sequenza di testo all'interno di un paragrafo, ad esempio il pennello per il primo piano, <xref:System.Windows.Media.Typeface> e le dimensioni del carattere.  Per implementare i tipi di proprietà dei paragrafi e delle sequenze di testo personalizzati, l'applicazione deve creare delle classi che derivano rispettivamente da <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> e da <xref:System.Windows.Media.TextFormatting.TextRunProperties>.  
  
## Vedere anche  
 [Funzionalità tipografiche di WPF](../../../../docs/framework/wpf/advanced/typography-in-wpf.md)   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)