---
title: "Cenni preliminari sulle funzionalit&#224; bidirezionali di WPF | Microsoft Docs"
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
  - "funzionalità bidirezionali"
  - "FlowDirection (proprietà)"
  - "FlowDocument (proprietà)"
  - "Span (elementi)"
ms.assetid: fd850e25-7dba-408c-b521-8873e51dc968
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Cenni preliminari sulle funzionalit&#224; bidirezionali di WPF
A differenza di altre piattaforme di sviluppo, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono disponibili molte funzionalità che supportano lo sviluppo rapido di un contenuto bidirezionale, ad esempio, la presenza contemporanea di dati da sinistra a destra e da destra a sinistra nello stesso documento.  Allo stesso tempo, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene offerta un'esperienza eccellente per gli utenti che richiedono funzionalità bidirezionali, ad esempio gli utenti che utilizzano l'arabo e l'ebraico.  
  
 Nelle sezioni seguenti vengono illustrate molte funzionalità bidirezionali con i relativi esempi in cui viene descritto come ottenere la migliore visualizzazione di un contenuto bidirezionale.  Nella maggior parte degli esempi viene utilizzato [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)], tuttavia si possono facilmente applicare i concetti al codice[!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] o [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)].  
  
   
  
<a name="FlowDirection"></a>   
## FlowDirection  
 La proprietà di base che definisce la direzione di flusso del contenuto in un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è <xref:System.Windows.FrameworkElement.FlowDirection%2A>.  Questa proprietà può essere impostata su uno dei due valori di enumerazione, <xref:System.Windows.FlowDirection> o <xref:System.Windows.FlowDirection>.  La proprietà è disponibile in tutti gli elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che ereditano da <xref:System.Windows.FrameworkElement>.  
  
 Negli esempi seguenti viene impostata la direzione di flusso di un elemento <xref:System.Windows.Controls.TextBox>.  
  
 **Direzione di flusso da sinistra a destra.**  
  
 [!code-xml[LTRRTL#LTR](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#ltr)]  
  
 **Direzione di flusso da destra a sinistra.**  
  
 [!code-xml[LTRRTL#RTL](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#rtl)]  
  
 Nell'immagine seguente viene mostrato il rendering del codice precedente.  
  
 **Immagine che illustra la direzione di flusso**  
  
 ![Allineamento TextBlock](../../../../docs/framework/wpf/advanced/media/lefttorightrighttoleft.png "LefttoRightRighttoLeft")  
  
 Un elemento all'interno di una struttura ad albero dell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] erediterà <xref:System.Windows.FrameworkElement.FlowDirection%2A> dal relativo contenitore.  Nell'esempio seguente, <xref:System.Windows.Controls.TextBlock> si trova all'interno di <xref:System.Windows.Controls.Grid>, che risiede in <xref:System.Windows.Window>.  L'impostazione di <xref:System.Windows.FrameworkElement.FlowDirection%2A> per <xref:System.Windows.Window> implica la sua impostazione anche per <xref:System.Windows.Controls.Grid> e <xref:System.Windows.Controls.TextBlock>.  
  
 Nell'esempio seguente viene illustrata l'impostazione di <xref:System.Windows.FrameworkElement.FlowDirection%2A>.  
  
 [!code-xml[FlowDirection#FlowDirection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDirection/CS/Window1.xaml#flowdirection)]  
  
 L'oggetto <xref:System.Windows.Window> di primo livello dispone di <xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection>, pertanto anche tutti gli elementi contenuti in esso ereditano lo stesso oggetto <xref:System.Windows.FrameworkElement.FlowDirection%2A>.  Affinché un elemento esegua l'override di un oggetto <xref:System.Windows.FrameworkElement.FlowDirection%2A> specificato, deve aggiungere una modifica di direzione esplicita, ad esempio il cambiamento del secondo oggetto <xref:System.Windows.Controls.TextBlock> dell'esempio precedente in <xref:System.Windows.FlowDirection>.  Se non viene definito nessun oggetto <xref:System.Windows.FrameworkElement.FlowDirection%2A>, viene applicato l'oggetto <xref:System.Windows.FlowDirection> predefinito.  
  
 Nell'immagine seguente viene mostrato l'output dell'esempio precedente.  
  
 **Immagine che illustra la direzione di flusso assegnata in modo esplicito**  
  
 ![Illustrazione della direzione del flusso](../../../../docs/framework/wpf/advanced/media/flowdir.png "FlowDir")  
  
<a name="FlowDocument"></a>   
## FlowDocument  
 Molte piattaforme di sviluppo, ad esempio [!INCLUDE[TLA#tla_html](../../../../includes/tlasharptla-html-md.md)], [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] e Java, forniscono un supporto particolare per lo sviluppo di contenuto bidirezionale.  I linguaggi di markup, ad esempio [!INCLUDE[TLA#tla_html](../../../../includes/tlasharptla-html-md.md)] offrono agli autori dei contenuti il markup necessario per visualizzare il testo in qualsiasi direzione richiesta, ad esempio con il tag [!INCLUDE[TLA#tla_html](../../../../includes/tlasharptla-html-md.md)] 4.0, "dir" accetta "rtl" o "ltr" come valori.  Questo tag è simile alla proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A>, ma la proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A> funziona in un modo più avanzato per eseguire il layout del contenuto testuale e può essere utilizzata per un contenuto diverso dal testo.  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], <xref:System.Windows.Documents.FlowDocument> è un elemento dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] versatile che consente l'hosting di una combinazione di testo, tabelle, immagini e altri elementi.  Nell'esempio presentato nelle sezioni seguenti viene utilizzato questo elemento.  
  
 L'aggiunta di testo a <xref:System.Windows.Documents.FlowDocument> può essere eseguita in molti modi.  Uno di quelli più semplici è rappresentato da <xref:System.Windows.Documents.Paragraph>, vale a dire un elemento a livello di blocco utilizzato per raggruppare il contenuto, ad esempio un testo.  Per aggiungere testo agli elementi di livello inline riportati negli esempi, utilizzare <xref:System.Windows.Documents.Span> e <xref:System.Windows.Documents.Run>.  <xref:System.Windows.Documents.Span> è un elemento del contenuto del flusso di livello inline utilizzato per raggruppare altri elementi inline, mentre <xref:System.Windows.Documents.Run> è un elemento del contenuto del flusso di livello inline destinato a contenere un'esecuzione di testo non formattato.  <xref:System.Windows.Documents.Span> può generare più elementi <xref:System.Windows.Documents.Run>.  
  
 Nel primo esempio di documento è contenuto un documento che dispone di un numero di nomi per la condivisione di rete. Ad esempio `\\server1\folder\file.ext`.  Indipendentemente dal fatto che questo collegamento di rete si trovi in un documento in arabo o in inglese, si desidera che venga sempre visualizzato nello stesso modo.  Nell'immagine seguente viene mostrato il collegamento nel documento <xref:System.Windows.FlowDirection> arabo.  
  
 **Immagine che illustra l'utilizzo dell'elemento Span**  
  
 ![Documento con flusso da destra a sinistra](../../../../docs/framework/wpf/advanced/media/flowdocument.png "FlowDocument")  
  
 Dal momento che il testo è <xref:System.Windows.FlowDirection>, tutti i caratteri speciali, ad esempio "\\", separano il testo in un ordine da destra a sinistra.  Di conseguenza il collegamento non viene visualizzato nell'ordine corretto, pertanto per risolvere il problema, il testo deve essere incorporato al fine di conservare un oggetto <xref:System.Windows.Documents.Run> separato che scorre <xref:System.Windows.FlowDirection>.  Invece di disporre di un oggetto <xref:System.Windows.Documents.Run> separato per ciascuna lingua, un modo migliore per risolvere il problema consiste nell'incorporare il testo inglese utilizzato meno frequentemente in un oggetto <xref:System.Windows.Documents.Span> arabo più grande.  
  
 Questa condizione è illustrata nell'immagine seguente.  
  
 **Immagine che illustra l'utilizzo dell'elemento Run in un elemento Span**  
  
 ![Schermata di XamlPad](../../../../docs/framework/wpf/advanced/media/runspan.png "RunSpan")  
  
 Nell'esempio seguente viene illustrato l'utilizzo degli elementi <xref:System.Windows.Documents.Run> e <xref:System.Windows.Documents.Span> nei documenti.  
  
 [!code-xml[RunSpan#RunSpan](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RunSpan/CS/Window1.xaml#runspan)]  
  
<a name="SpanElements"></a>   
## Elementi Span  
 L'elemento <xref:System.Windows.Documents.Span> funziona come un separatore di limiti tra i testi con diverse direzioni di flusso.  Persino gli elementi <xref:System.Windows.Documents.Span> con la stessa direzione di flusso dispongono di diversi ambiti bidirezionali, vale a dire che gli elementi <xref:System.Windows.Documents.Span> vengono ordinati in base all'oggetto <xref:System.Windows.FlowDirection> del contenitore e solo il contenuto dell'elemento <xref:System.Windows.Documents.Span> segue <xref:System.Windows.FlowDirection> di <xref:System.Windows.Documents.Span>.  
  
 Nell'immagine seguente viene mostrata la direzione di flusso di diversi elementi <xref:System.Windows.Controls.TextBlock>.  
  
 **Immagine che illustra la direzione di flusso in diversi elementi TextBlock**  
  
 ![Blocchi di testo con direzioni di flusso diverse](../../../../docs/framework/wpf/advanced/media/span.png "Span")  
  
 Nell'esempio seguente viene illustrato come utilizzare elementi <xref:System.Windows.Documents.Span> e <xref:System.Windows.Documents.Run> per ottenere i risultati mostrati nell'immagine precedente.  
  
 [!code-xml[Span#Span](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Span/CS/Window1.xaml#span)]  
  
 Negli elementi <xref:System.Windows.Controls.TextBlock> dell'esempio, gli elementi <xref:System.Windows.Documents.Span> vengono disposti in base a <xref:System.Windows.FlowDirection> degli elementi padre, tuttavia il testo di ciascun elemento <xref:System.Windows.Documents.Span> scorre in base a <xref:System.Windows.FlowDirection>.  Questa condizione può essere applicata all'alfabeto latino e arabo oppure a qualsiasi altra lingua.  
  
### Aggiunta di xml:lang  
 Nell'immagine seguente viene mostrato un altro esempio in cui vengono utilizzati numeri ed espressioni aritmetiche, ad esempio `"200.0+21.4=221.4"`.  Notare che è stato impostato solo l'oggetto <xref:System.Windows.FlowDirection>.  
  
 **Immagine che visualizza i numeri che utilizzano solo la direzione di flusso**  
  
 ![Numeri con flusso da destra a sinistra](../../../../docs/framework/wpf/advanced/media/langattribute.png "LangAttribute")  
  
 Gli utenti di questa applicazione rimarranno delusi dall'output, poiché anche se l'oggetto <xref:System.Windows.FlowDirection> è corretto, la forma dei numeri non corrisponde a quella dei numeri arabi.  
  
 Gli elementi XAML possono includere un attributo [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] \(`xml:lang`\) che definisce la lingua di ciascun elemento.  XAML supporta inoltre un principio relativo a linguaggio [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] in base al quale i valori `xml:lang` applicati agli elementi padre della struttura ad albero vengono utilizzati dagli elementi figlio.  Nell'esempio precedente, dal momento che non era stata definita nessuna lingua per l'elemento <xref:System.Windows.Documents.Run> o per qualsiasi altro elemento di primo livello, è stata utilizzato l'oggetto `xml:lang` predefinito di XAML, vale a dire `en-US`.  L'algoritmo interno per la definizione dei numeri di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] seleziona i numeri nella lingua corrispondente, in questo caso l'inglese.  Per eseguire correttamente il rendering dei numeri arabi, è necessario impostare `xml:lang`.  
  
 Nell'immagine riportata di seguito viene mostrato un esempio con l'attributo `xml:lang` aggiunto.  
  
 **Immagine che illustra l'utilizzo dell'attributo xml:lang**  
  
 ![Numeri arabi con flusso da destra a sinistra](../../../../docs/framework/wpf/advanced/media/langattribute2.png "LangAttribute2")  
  
 Nell'esempio seguente viene aggiunto l'attributo `xml:lang` all'applicazione.  
  
 [!code-xml[LangAttribute#LangAttribute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LangAttribute/CS/Window1.xaml#langattribute)]  
  
 Prestare attenzione ai diversi valori `xml:lang` delle lingue che dipendono dalla regione di destinazione, ad esempio `"ar-SA"` e `"ar-EG"` che rappresentano due varianti dell'arabo.  Negli esempi precedenti viene illustrata la necessità di definire sia il valore `xml:lang` sia il valore <xref:System.Windows.FlowDirection>.  
  
<a name="FlowDirectionNontext"></a>   
## FlowDirection con elementi non di testo  
 <xref:System.Windows.FlowDirection> non definisce solo la modalità di scorrimento del testo in un elemento testuale, ma anche la direzione di flusso di quasi tutti gli elementi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)].  Nell'immagine seguente viene mostrato un oggetto <xref:System.Windows.Controls.ToolBar> che utilizza un oggetto <xref:System.Windows.Media.LinearGradientBrush> orizzontale per disegnare lo sfondo.  
  
 **Immagine che illustra una barra degli strumenti con una sfumatura da sinistra a destra**  
  
 ![Schermata della sfumatura](../../../../docs/framework/wpf/advanced/media/gradient.png "Gradient")  
  
 Dopo aver impostato l'oggetto <xref:System.Windows.FlowDirection> su <xref:System.Windows.FlowDirection>, i pulsanti <xref:System.Windows.Controls.ToolBar> vengono disposti da destra a sinistra e <xref:System.Windows.Media.LinearGradientBrush> riallinea gli offset in modo che scorrano da destra a sinistra.  
  
 Nell'immagine seguente viene mostrato il riallineamento di <xref:System.Windows.Media.LinearGradientBrush>.  
  
 **Immagine che illustra una barra degli strumenti con una sfumatura da destra a sinistra**  
  
 ![Sfumatura con flusso da destra a sinistra](../../../../docs/framework/wpf/advanced/media/gradient2-wpf.png "Gradient2\_WPF")  
  
 Nell'esempio seguente viene disegnato un oggetto <xref:System.Windows.FlowDirection> <xref:System.Windows.Controls.ToolBar>.  \(per disegnarlo da sinistra a destra, rimuovere l'attributo <xref:System.Windows.FlowDirection> da <xref:System.Windows.Controls.ToolBar>.  
  
 [!code-xml[Gradient#Gradient](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Gradient/CS/Window1.xaml#gradient)]  
  
<a name="FlowDirectionExceptions"></a>   
### Eccezioni di FlowDirection  
 Esistono alcuni casi in cui <xref:System.Windows.FlowDirection> non si comporta nel modo previsto.  In questa sezione vengono illustrate due di queste eccezioni.  
  
 **Image**  
  
 <xref:System.Windows.Controls.Image> rappresenta un controllo che visualizza un'immagine.  In [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)], questo oggetto può essere utilizzato con una proprietà<xref:System.Windows.Controls.Image.Source%2A> che definisce l'[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] di <xref:System.Windows.Controls.Image> da visualizzare.  
  
 A differenza di altri elementi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], <xref:System.Windows.Controls.Image> non eredita <xref:System.Windows.FlowDirection> dal contenitore.  Tuttavia, se l'oggetto <xref:System.Windows.FlowDirection> è impostato in modo esplicito su <xref:System.Windows.FlowDirection>, un oggetto <xref:System.Windows.Controls.Image> viene visualizzato capovolto in senso orizzontale.  Questa condizione viene implementata come una funzionalità utile per gli sviluppatori di contenuti bidirezionali, poiché, in alcuni casi, il capovolgimento in senso orizzontale dell'immagine genera l'effetto desiderato.  
  
 Nell'immagine seguente viene mostrato un oggetto <xref:System.Windows.Controls.Image> capovolto.  
  
 **Immagine che illustra un'immagine capovolta**  
  
 ![Schermata di XamlPad](../../../../docs/framework/wpf/advanced/media/image.png "Image")  
  
 Nell'esempio seguente viene dimostrato che <xref:System.Windows.Controls.Image> non riesce a ereditare l'oggetto <xref:System.Windows.FlowDirection> da <xref:System.Windows.Controls.StackPanel> che lo contiene.  **Nota** È necessario disporre di un file denominato **ms\_logo.jpg** nell'unità C:\\ per eseguire questo esempio.  
  
 [!code-xml[Image#Image](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Image/CS/Window1.xaml#image)]  
  
 **Nota** Nei file scaricati è incluso un file **ms\_logo.jpg**.  Nel codice si presuppone che il file con estensione jpg non si trovi all'interno del progetto ma in un'altra posizione nell'unità C:\\.  È necessario copiare il file con estensione jpg dai file di progetto nell'unità C:\\ oppure modificare il codice affinché la ricerca venga eseguita all'interno del progetto.  A tale scopo, modificare `Source="file://c:/ms_logo.jpg"` in `Source="ms_logo.jpg"`.  
  
 **Percorsi**  
  
 Oltre a <xref:System.Windows.Controls.Image>, un altro elemento interessante è <xref:System.Windows.Shapes.Path>.  Path è un oggetto che consente di disegnare una serie di righe e curve collegate.  Si comporta in modo simile a <xref:System.Windows.Controls.Image> per quanto riguarda <xref:System.Windows.FlowDirection>; ad esempio <xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection> è un'immagine speculare orizzontale di <xref:System.Windows.FlowDirection>.  Tuttavia, a differenza di <xref:System.Windows.Controls.Image>, <xref:System.Windows.Shapes.Path> eredita <xref:System.Windows.FlowDirection> dal contenitore che non deve essere specificato in modo esplicito.  
  
 Nell'esempio seguente viene disegnata una semplice freccia con 3 righe.  La prima freccia eredita la direzione di flusso di <xref:System.Windows.FlowDirection> da <xref:System.Windows.Controls.StackPanel> in modo che i punti iniziali e finali vengano misurati da una radice posizionata sul lato destro.  La seconda freccia dispone di un oggetto <xref:System.Windows.FlowDirection> <xref:System.Windows.FlowDirection> esplicito e inizia dal lato destro.  Tuttavia, la radice iniziale della terza freccia è collocata sul lato sinistro.  Per ulteriori informazioni sul disegno, vedere <xref:System.Windows.Media.LineGeometry> e <xref:System.Windows.Media.GeometryGroup>.  
  
 [!code-xml[Paths#Paths](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Paths/CS/Window1.xaml#paths)]  
  
 Nell'immagine seguente viene mostrato l'output dell'esempio precedente.  
  
 **Immagine che illustra le frecce disegnate utilizzando l'elemento Path**  
  
 ![Percorsi](../../../../docs/framework/wpf/advanced/media/paths.png "Paths")  
  
 <xref:System.Windows.Controls.Image> e <xref:System.Windows.Shapes.Path> sono due esempi del modo in cui [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] utilizza <xref:System.Windows.FlowDirection>.  Oltre a disporre gli elementi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] in una direzione specifica all'interno di un contenitore, l'oggetto <xref:System.Windows.FlowDirection> può essere utilizzato con elementi quali <xref:System.Windows.Controls.InkPresenter> che esegue il rendering dell'input penna sulla superficie, su <xref:System.Windows.Media.LinearGradientBrush> e su <xref:System.Windows.Media.RadialGradientBrush>.  Se è necessario che il comportamento da destra a sinistra del contenuto simuli un comportamento da sinistra a destra o viceversa, in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] è disponibile tale funzionalità.  
  
<a name="NumberSubstitution"></a>   
## Sostituzione numerica  
 Storicamente, in [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] è sempre stata supportata la sostituzione numerica, consentendo la rappresentazione di diverse forme di tipo linguistico per le stesse cifre e mantenendo unificata, per le diverse impostazioni locali, la memoria interna di queste cifre, ad esempio i numeri vengono memorizzati con i noti valori esadecimali, 0 x 40, 0 x 41, ma visualizzati in base alla lingua selezionata.  
  
 In questo modo, le applicazioni hanno potuto elaborare i valori numerici senza dover convertirli da una lingua a un'altra, ad esempio un utente può aprire un foglio di calcolo di [!INCLUDE[TLA#tla_xl](../../../../includes/tlasharptla-xl-md.md)] in un [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] localizzato in arabo e visualizzare i numeri in arabo, ma anche aprirlo nella versione europea di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] visualizzando la rappresentazione europea degli stessi numeri.  Questa condizione è necessaria anche per altri simboli, quali i separatori virgola e il simbolo della percentuale, poiché sono spesso associati a numeri nello stesso documento.  
  
 In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] è stata mantenuta la stessa tradizione e aggiunto un ulteriore supporto a questa funzionalità che consente un maggiore controllo dell'utente sul momento e sulla modalità di utilizzo della sostituzione.  Sebbene questa funzionalità sia stata progettata per tutte le lingue, è particolarmente utile per i contenuti bidirezionali in cui la definizione delle cifre per una lingua specifica rappresenta solitamente una sfida per gli sviluppatori di applicazioni, a causa delle diverse impostazioni cultura con cui un'applicazione può essere eseguita.  
  
 La proprietà principale che controlla il funzionamento della sostituzione numerica in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] è la proprietà di dipendenza <xref:System.Windows.Media.NumberSubstitution.Substitution%2A>.  La classe <xref:System.Windows.Media.NumberSubstitution> specifica la modalità di visualizzazione dei numeri nel testo.  Dispone di tre proprietà pubbliche che ne definiscono il comportamento.  Di seguito è riportato un riepilogo di tutte le proprietà.  
  
 **CultureSource:**  
  
 Questa proprietà specifica come vengono determinate le impostazioni cultura per i numeri.  Accetta uno dei tre valori di enumerazione di <xref:System.Windows.Media.NumberCultureSource>.  
  
-   Override: le impostazioni cultura del numero sono quelle della proprietà <xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A>.  
  
-   Text: le impostazioni cultura del numero sono quelle della sequenza di testo.  Nel markup, si tratterebbe di `xml:lang` o della relativa proprietà alias `Language` \(<xref:System.Windows.FrameworkElement.Language%2A> o <xref:System.Windows.FrameworkContentElement.Language%2A>\).  Inoltre, si tratta del valore predefinito per le classi che derivano da <xref:System.Windows.FrameworkContentElement>.  Tali classi includono <xref:System.Windows.Documents.Paragraph?displayProperty=fullName>, <xref:System.Windows.Documents.Table?displayProperty=fullName>, <xref:System.Windows.Documents.TableCell?displayProperty=fullName> e così via.  
  
-   User: le impostazioni cultura del numero sono quelle del thread corrente.  Questa proprietà è quella predefinita per tutte le sottoclassi di <xref:System.Windows.FrameworkElement>, ad esempio <xref:System.Windows.Controls.Page>, <xref:System.Windows.Window> e <xref:System.Windows.Controls.TextBlock>.  
  
 **CultureOverride**:  
  
 La proprietà <xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> viene utilizzata solo se la proprietà <xref:System.Windows.Media.NumberSubstitution.CultureSource%2A> è impostata su <xref:System.Windows.Media.NumberCultureSource>, in caso contrario viene ignorata.  Specifica le impostazioni cultura del numero.  Un valore pari a `null`, vale a dire il valore predefinito, viene interpretato come en\-US.  
  
 **Substitution**:  
  
 Questa proprietà specifica il tipo di sostituzione numerica da eseguire.  Accetta uno dei seguenti valori di enumerazione di <xref:System.Windows.Media.NumberSubstitutionMethod>:  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>: il metodo di sostituzione viene determinato in base alla proprietà <xref:System.Globalization.NumberFormatInfo.DigitSubstitution%2A?displayProperty=fullName> delle impostazioni cultura del numero.  Questa è l'impostazione predefinita.  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>: se le impostazioni cultura del numero sono in arabo o in farsi, specifica che le cifre dipendono dal contesto.  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>: il rendering dei numeri viene sempre eseguito come cifre europee.  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>: il rendering dei numeri viene eseguito utilizzando le cifre nazionali per le impostazioni cultura del numero, come specificato dalla proprietà <xref:System.Globalization.CultureInfo.NumberFormat%2A> delle impostazioni cultura.  
  
-   <xref:System.Windows.Media.NumberSubstitutionMethod>: il rendering dei numeri viene eseguito utilizzando le cifre tradizionali per le impostazioni cultura del numero.  Per la maggior parte delle impostazioni cultura, questo valore è uguale a <xref:System.Windows.Media.NumberSubstitutionMethod>.  Tuttavia, i valori <xref:System.Windows.Media.NumberSubstitutionMethod> sono rappresentati da cifre latine per alcune impostazioni cultura arabe, mentre questo valore viene rappresentato in cifre arabe per tutte le impostazioni cultura arabe.  
  
 Significato dei valori per uno sviluppatore di contenuti bidirezionali  Nella maggior parte dei casi, lo sviluppatore deve solo definire <xref:System.Windows.FlowDirection> e la lingua di ciascun elemento testuale dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], ad esempio `Language="ar-SA"` e logica <xref:System.Windows.Media.NumberSubstitution> gestisce la visualizzazione dei numeri in base all'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] corretta.  Nell'esempio seguente viene illustrato l'utilizzo dei numeri arabi e inglesi in un'applicazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] che esegue una versione araba di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  
  
 [!code-xml[Numbers#Numbers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Numbers/CS/Window1.xaml#numbers)]  
  
 Nell'immagine seguente viene mostrato l'output dell'esempio precedente se viene eseguita una versione araba di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  
  
 **Immagine che illustra i numeri arabi e inglesi visualizzati**  
  
 ![Schermata di XamlPad con numeri](../../../../docs/framework/wpf/advanced/media/numbers.png "Numbers")  
  
 <xref:System.Windows.FlowDirection> era importante in questo caso, poiché l'impostazione di <xref:System.Windows.FlowDirection> su <xref:System.Windows.FlowDirection> avrebbe prodotto cifre europee.  Nelle sezioni seguenti viene descritto come ottenere una visualizzazione unificata delle cifre in tutto il documento.  Se questo esempio non è in esecuzione su una versione araba di Windows, tutte le cifre vengono visualizzate come cifre europee.  
  
 **Definizione delle regole di sostituzione**  
  
 In un'applicazione reale, è necessario impostare l'oggetto Language a livello di codice.  Ad esempio, si può impostare l'attributo `xml:lang` in modo che sia uguale a quello utilizzato dall'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] del sistema oppure modificare la lingua in base allo stato applicazione.  
  
 Se si desidera apportare modifiche in base allo stato applicazione, utilizzare altre funzionalità fornite da [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
 Innanzitutto, scegliere l'impostazione `NumberSubstitution.CultureSource="Text"` del componente dell'applicazione.  L'utilizzo di questa impostazione garantisce che le impostazioni non provengano dall'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] per gli elementi di testo che dispongono di "User" come valore predefinito, ad esempio <xref:System.Windows.Controls.TextBlock>.  
  
 Di seguito è riportato un esempio:  
  
||  
|-|  
|`<TextBlock`<br /><br /> `Name="text1" NumberSubstitution.CultureSource="Text">`<br /><br /> `1234+5679=6913`<br /><br /> `</TextBlock>`|  
  
 Nel codice [!INCLUDE[TLA2#tla_lhcshrp](../../../../includes/tla2sharptla-lhcshrp-md.md)] corrispondente, impostare, ad esempio, la proprietà `Language` su `"ar-SA"`.  
  
||  
|-|  
|`text1.Language =`<br /><br /> `System.Windows.Markup.XmlLanguage.GetLanguage("ar-SA");`|  
  
 Se è necessario impostare la proprietà `Language` sulla lingua dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dell'utente corrente, utilizzare il codice seguente.  
  
||  
|-|  
|`text1.Language =`<br /><br /> `System.Windows.Markup.XmlLanguage.GetLanguage(`<br /><br /> `System.Globalization.CultureInfo.CurrentUICulture.IetfLanguageTag);`|  
  
 <xref:System.Globalization.CultureInfo.CurrentCulture%2A> rappresenta le impostazioni cultura attuali utilizzate dal thread corrente in fase di esecuzione.  
  
 L'esempio [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] finale deve essere simile all'esempio seguente.  
  
 [!code-xml[Numbers2#Numbers2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Numbers2/CS/Window1.xaml#numbers2)]  
  
 L'esempio [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] finale deve essere simile all'esempio seguente.  
  
 [!code-csharp[NumbersCSharp#NumbersCSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/NumbersCSharp/CSharp/Window1.xaml.cs#numberscsharp)]  
  
 Nell'immagine seguente viene illustrato l'aspetto della finestra per entrambi i linguaggi di programmazione.  
  
 **Immagine che visualizza i numeri arabi**  
  
 ![Numeri arabi](../../../../docs/framework/wpf/advanced/media/numbers2.png "Numbers2")  
  
 **Utilizzo della proprietà Substitution**  
  
 Il funzionamento della sostituzione numerica in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] dipende dall'oggetto Language dell'elemento di testo e da <xref:System.Windows.FlowDirection>.  Se l'oggetto <xref:System.Windows.FlowDirection> viene mantenuto a destra, viene eseguito il rendering delle cifre europee.  Tuttavia, se è preceduto da un testo arabo o se l'oggetto Language è impostato su "ar" e <xref:System.Windows.FlowDirection> è <xref:System.Windows.FlowDirection>, viene eseguito il rendering delle cifre arabe.  
  
 In alcuni casi, tuttavia, è possibile creare un'applicazione unificata utilizzando, ad esempio, le cifre europee per tutti gli utenti  oppure cifre arabe nelle celle <xref:System.Windows.Documents.Table> con un oggetto <xref:System.Windows.Style> specifico.  Tale operazione può essere eseguita facilmente utilizzando la proprietà <xref:System.Windows.Media.NumberSubstitution.Substitution%2A>.  
  
 Nell'esempio seguente, per il primo oggetto <xref:System.Windows.Controls.TextBlock> non è stata impostata la proprietà <xref:System.Windows.Media.NumberSubstitution.Substitution%2A>, pertanto nell'algoritmo vengono visualizzate le cifre arabe, come previsto.  Tuttavia, nel secondo oggetto <xref:System.Windows.Controls.TextBlock>, la sostituzione viene impostata su European, eseguendo l'override della sostituzione predefinita per i numeri arabi, e vengono visualizzate le cifre europee.  
  
 [!code-xml[Numbers3#Numbers3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Numbers3/CS/Window1.xaml#numbers3)]