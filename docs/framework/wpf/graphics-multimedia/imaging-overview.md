---
title: "Cenni preliminari sulla creazione dell&#39;immagine | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conversione di immagini"
  - "ritaglio di immagini"
  - "decodifica di formati di immagine"
  - "visualizzazione di immagini"
  - "codifica di formati di immagine"
  - "decodifica dei formati per le immagini"
  - "codifica dei formati per le immagini"
  - "metadati delle immagini"
  - "immagini, informazioni sulla creazione dell'immagine"
  - "API per la creazione dell'immagine"
  - "metadati, immagini"
  - "disegno con oggetti Image"
  - "rotazione di immagini"
  - "adattamento delle immagini"
ms.assetid: 72aad87a-e6f3-4937-94cd-a18b7766e990
caps.latest.revision: 32
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# Cenni preliminari sulla creazione dell&#39;immagine
In questo argomento viene presentata un'introduzione a [!INCLUDE[TLA#tla_wic](../../../../includes/tlasharptla-wic-md.md)].  [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] consente agli sviluppatori di visualizzare, trasformare e formattare le immagini.  
  
   
  
<a name="_wpfImaging"></a>   
## WPF Imaging Component  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] offre miglioramenti significativi nelle funzionalità di creazione dell'immagine in [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)].  Le funzionalità di creazione dell'immagine, ad esempio la visualizzazione di un'immagine bitmap o l'utilizzo di un'immagine in un controllo comune, si basavano in precedenza sulle librerie [!INCLUDE[TLA#tla_gdi](../../../../includes/tlasharptla-gdi-md.md)] o [!INCLUDE[TLA#tla_gdiplus](../../../../includes/tlasharptla-gdiplus-md.md)].  Queste [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] forniscono la funzionalità di creazione dell'immagine di base, ma sono prive di funzioni quali il supporto per l'estensibilità dei codec e per immagini di elevata fedeltà.  [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] è progettato per risolvere i difetti delle interfacce [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] e [!INCLUDE[TLA2#tla_gdiplus](../../../../includes/tla2sharptla-gdiplus-md.md)] e per fornire un nuovo set di [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] al fine di visualizzare e utilizzare immagini nelle applicazioni.  
  
 Sono disponibili due modi per accedere all'[!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] di [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)], un componente gestito e un componente non gestito.  Il componente non gestito offre le seguenti funzionalità.  
  
-   Modello di estensibilità per formati immagine nuovi o proprietari.  
  
-   Prestazioni e sicurezza migliorate per i formati immagine nativi, compresi [!INCLUDE[TLA#tla_bmp](../../../../includes/tlasharptla-bmp-md.md)], [!INCLUDE[TLA#tla_jpegorg](../../../../includes/tlasharptla-jpegorg-md.md)], [!INCLUDE[TLA#tla_png](../../../../includes/tlasharptla-png-md.md)], [!INCLUDE[TLA#tla_tiff](../../../../includes/tlasharptla-tiff-md.md)], [!INCLUDE[TLA#tla_wdp](../../../../includes/tlasharptla-wdp-md.md)], [!INCLUDE[TLA#tla_gif](../../../../includes/tlasharptla-gif-md.md)] e icone \(ICO\).  
  
-   Conservazione di dati immagine con elevata profondità in bit fino a 8 bit per canale \(32 bit per pixel\).  
  
-   Operazioni di ridimensionamento, ritaglio e rotazione delle immagini non distruttive.  
  
-   Gestione dei colori semplificata.  
  
-   Supporto per metadati proprietari nei file.  
  
-   Il componente gestito utilizza l'infrastruttura non gestita per garantire l'integrazione omogenea delle immagini con altre funzionalità [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], ad esempio [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)], animazione e grafica.  Il componente gestito sfrutta inoltre il modello di estensibilità dei codec per la creazione dell'immagine di [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] che consente il riconoscimento automatico di nuovi formati immagine nelle applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 La maggior parte delle [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] gestite risiedono nello spazio dei nomi <xref:System.Windows.Media.Imaging?displayProperty=fullName>, anche se numerosi tipi importanti, come <xref:System.Windows.Media.ImageBrush> e <xref:System.Windows.Media.ImageDrawing>, risiedono nello spazio dei nomi <xref:System.Windows.Media?displayProperty=fullName> e <xref:System.Windows.Controls.Image> risiede nello spazio dei nomi <xref:System.Windows.Controls?displayProperty=fullName>.  
  
 In questo argomento vengono fornite informazioni aggiuntive sul componente gestito.  Per ulteriori informazioni sull'[!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] non gestita, vedere la documentazione [Unmanaged WPF Imaging Component](_wic_lh).  
  
<a name="_imageformats"></a>   
## Formati immagine WPF  
 Un codec viene utilizzato per codificare o decodificare un formato multimediale specifico.  [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] include un codec per i formati immagine [!INCLUDE[TLA2#tla_bmp](../../../../includes/tla2sharptla-bmp-md.md)], [!INCLUDE[TLA2#tla_jpeg](../../../../includes/tla2sharptla-jpeg-md.md)], [!INCLUDE[TLA2#tla_png](../../../../includes/tla2sharptla-png-md.md)], [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)], [!INCLUDE[TLA2#tla_wdp](../../../../includes/tla2sharptla-wdp-md.md)], [!INCLUDE[TLA2#tla_gif](../../../../includes/tla2sharptla-gif-md.md)] e ICON.  Ciascuno di questi codec consente alle applicazioni di decodificare e, a eccezione di ICON, codificare i rispettivi formati immagine.  
  
 <xref:System.Windows.Media.Imaging.BitmapSource> è una classe importante utilizzata nella codifica e decodifica delle immagini.  È il blocco predefinito di base della pipeline di [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] e rappresenta un insieme unico e costante di pixel a determinate dimensione e risoluzione.  Un oggetto <xref:System.Windows.Media.Imaging.BitmapSource> può essere costituito da un singolo frame di un'immagine a più frame oppure può essere il risultato di una trasformazione eseguita su un oggetto <xref:System.Windows.Media.Imaging.BitmapSource>.  È l'elemento padre di molte delle classi principali utilizzate nella creazione dell'immagine di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], ad esempio <xref:System.Windows.Media.Imaging.BitmapFrame>.  
  
 <xref:System.Windows.Media.Imaging.BitmapFrame> viene utilizzato per archiviare i dati bitmap effettivi di un formato immagine.  Molti formati immagine supportano un solo <xref:System.Windows.Media.Imaging.BitmapFrame>, anche se formati come [!INCLUDE[TLA2#tla_gif](../../../../includes/tla2sharptla-gif-md.md)] e [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)] supportano più frame per immagine.  I frame vengono utilizzati dai decodificatori come dati di input e passati ai codificatori per creare file di immagine.  
  
 Nell'esempio riportato di seguito un oggetto <xref:System.Windows.Media.Imaging.BitmapFrame> viene creato da un oggetto <xref:System.Windows.Media.Imaging.BitmapSource> e successivamente aggiunto a un'immagine [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)].  
  
 [!code-csharp[BitmapFrameExample#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BitmapFrameExample/CSharp/BitmapFrame.cs#10)]
 [!code-vb[BitmapFrameExample#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BitmapFrameExample/VB/BitmapFrame.vb#10)]  
  
### Decodifica dei formati immagine  
 La decodifica delle immagini è la conversione di un formato immagine in dati immagine che possono essere utilizzati dal sistema.  I dati immagine possono quindi essere utilizzati per visualizzare, elaborare o codificare un formato diverso.  La selezione del decodificatore si basa sul formato immagine.  La selezione del codec è automatica, a meno che non venga specificato un decodificatore specifico.  Negli esempi della sezione [Visualizzazione delle immagini in WPF](#_displayingimages) viene illustrata la decodifica automatica.  I decodificatori di formati personalizzati sviluppati tramite interfacce [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] non gestite e registrati con il sistema partecipano automaticamente alla selezione del decodificatore.  In questo modo è possibile visualizzare automaticamente formati personalizzati nelle applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo di un decodificatore bitmap per decodificare un'immagine [!INCLUDE[TLA2#tla_bmp](../../../../includes/tla2sharptla-bmp-md.md)].  
  
 [!code-cpp[BmpBitmapDecoderEncoder#5](../../../../samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#5)]
 [!code-csharp[BmpBitmapDecoderEncoder#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#5)]
 [!code-vb[BmpBitmapDecoderEncoder#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#5)]  
  
### Codifica dei formati immagine  
 La codifica delle immagini è la conversione dei dati immagine in un formato immagine specifico.  I dati immagine codificati possono quindi essere utilizzati per creare nuovi file di immagine.  In [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] sono disponibili codificatori per ognuno dei formati immagine descritti in precedenza.  
  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo di un codificatore per salvare un'immagine bitmap appena creata.  
  
 [!code-cpp[BmpBitmapDecoderEncoder#3](../../../../samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#3)]
 [!code-csharp[BmpBitmapDecoderEncoder#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#3)]
 [!code-vb[BmpBitmapDecoderEncoder#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#3)]  
  
<a name="_displayingimages"></a>   
## Visualizzazione delle immagini in WPF  
 Esistono diversi modi per visualizzare un'immagine in un'applicazione [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)].  Le immagini possono essere visualizzate tramite un controllo <xref:System.Windows.Controls.Image>, disegnate su un elemento visivo tramite un oggetto <xref:System.Windows.Media.ImageBrush> o disegnate utilizzando <xref:System.Windows.Media.ImageDrawing>.  
  
### Utilizzo del controllo Image  
 <xref:System.Windows.Controls.Image> è un elemento del framework e rappresenta la principale modalità per visualizzare le immagini nelle applicazioni.  In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], <xref:System.Windows.Controls.Image> può essere utilizzato in due modi: sintassi degli attributi o sintassi delle proprietà.  Nell'esempio riportato di seguito viene illustrato come eseguire il rendering di un'immagine con una larghezza di 200 pixel utilizzando sia la sintassi degli attributi sia la sintassi dei tag delle proprietà.  Per ulteriori informazioni sulla sintassi degli attributi e sulla sintassi delle proprietà, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
 [!code-xml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
 In molti esempi viene utilizzato un oggetto <xref:System.Windows.Media.Imaging.BitmapImage> per fare riferimento a un file di immagine.  <xref:System.Windows.Media.Imaging.BitmapImage> è un oggetto <xref:System.Windows.Media.Imaging.BitmapSource> specializzato ottimizzato per il caricamento di [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e consente di visualizzare facilmente immagini come proprietà <xref:System.Windows.Controls.Image.Source%2A> di un controllo <xref:System.Windows.Controls.Image>.  
  
 Nell'esempio riportato di seguito viene illustrato come eseguire il rendering di un'immagine con una larghezza di 200 pixel mediante codice.  
  
> [!NOTE]
>  <xref:System.Windows.Media.Imaging.BitmapImage> implementa l'interfaccia di <xref:System.ComponentModel.ISupportInitialize> per ottimizzare l'inizializzazione su più proprietà.  Le modifiche della proprietà possono verificarsi solo durante l'inizializzazione dell'oggetto.  Chiamare il metodo <xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A> per segnalare che l'inizializzazione è stata avviata e il metodo <xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A> per segnalare che l'inizializzazione è stata completata.  Dopo l'inizializzazione, le modifiche della proprietà vengono ignorate.  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
#### Rotazione, conversione e ritaglio delle immagini  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente agli utenti di trasformare le immagini utilizzando proprietà di <xref:System.Windows.Media.Imaging.BitmapImage> oppure oggetti <xref:System.Windows.Media.Imaging.BitmapSource> aggiuntivi, quali <xref:System.Windows.Media.Imaging.CroppedBitmap> o <xref:System.Windows.Media.Imaging.FormatConvertedBitmap>.  Queste trasformazioni delle immagini consentono di ridimensionare o ruotare un'immagine, modificarne il formato di pixel o ritagliarla.  
  
 Le rotazioni delle immagini vengono eseguite tramite la proprietà <xref:System.Windows.Media.Imaging.BitmapImage.Rotation%2A> di <xref:System.Windows.Media.Imaging.BitmapImage>.  Le rotazioni possono essere eseguite solo con incrementi di 90 gradi.  Nell'esempio riportato di seguito un'immagine viene ruotata di 90 gradi.  
  
 [!code-xml[ImageElementExample#TransformedXAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml#transformedxaml2)]  
  
 [!code-csharp[ImageElementExample#TransformedCSharp1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml.cs#transformedcsharp1)]
 [!code-vb[ImageElementExample#TransformedCSharp1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/TransformedImageExample.xaml.vb#transformedcsharp1)]  
  
 La conversione di un'immagine in un diverso formato di pixel, ad esempio le gradazioni di grigio, viene eseguita tramite <xref:System.Windows.Media.Imaging.FormatConvertedBitmap>.  Negli esempi riportati di seguito un'immagine viene convertita in <xref:System.Windows.Media.PixelFormats.Gray4%2A>.  
  
 [!code-xml[ImageElementExample_snip#ConvertedXAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml#convertedxaml2)]  
  
 [!code-csharp[ImageElementExample_snip#ConvertedCSharp1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml.cs#convertedcsharp1)]
 [!code-vb[ImageElementExample_snip#ConvertedCSharp1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/FormatConvertedExample.xaml.vb#convertedcsharp1)]  
  
 Per ritagliare un'immagine, è possibile utilizzare la proprietà <xref:System.Windows.UIElement.Clip%2A> di <xref:System.Windows.Controls.Image> o di <xref:System.Windows.Media.Imaging.CroppedBitmap>.  In genere, per visualizzare una parte di un'immagine, è opportuno utilizzare <xref:System.Windows.UIElement.Clip%2A>.  Se è necessario codificare e salvare un'immagine ritagliata, utilizzare <xref:System.Windows.Media.Imaging.CroppedBitmap>.  Nell'esempio riportato di seguito, un'immagine viene ritagliata tramite la proprietà Clip utilizzando un oggetto <xref:System.Windows.Media.EllipseGeometry>.  
  
 [!code-xml[ImageElementExample_snip#CroppedXAMLUsingClip1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml#croppedxamlusingclip1)]  
  
 [!code-csharp[ImageElementExample_snip#CroppedCSharpUsingClip1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml.cs#croppedcsharpusingclip1)]
 [!code-vb[ImageElementExample_snip#CroppedCSharpUsingClip1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/CroppedImageExample.xaml.vb#croppedcsharpusingclip1)]  
  
#### Adattamento delle immagini  
 La proprietà <xref:System.Windows.Controls.Image.Stretch%2A> controlla la modalità in cui un'immagine viene adattata per riempire il proprio contenitore.  La proprietà <xref:System.Windows.Controls.Image.Stretch%2A> accetta i seguenti valori, definiti dall'enumerazione <xref:System.Windows.Media.Stretch>:  
  
-   <xref:System.Windows.Media.Stretch>: l'immagine non viene adattata per riempire l'area di output.  Se l'immagine è più grande dell'area di output, viene disegnata nell'area di output tagliando la parte che non è possibile inserire.  
  
-   <xref:System.Windows.Media.Stretch>: l'immagine viene ridimensionata per adattarsi all'area di output.  Poiché l'altezza e la larghezza dell'immagine vengono ridimensionate in modo indipendente, le proporzioni originali dell'immagine potrebbero non essere mantenute.  In atri termini, l'immagine potrebbe essere distorta allo scopo di riempire completamente il contenitore di output.  
  
-   <xref:System.Windows.Media.Stretch>: l'immagine viene ridimensionata in modo da adattarsi completamente all'area di output.  Le proporzioni dell'immagine vengono mantenute.  
  
-   <xref:System.Windows.Media.Stretch>: l'immagine viene ridimensionata in modo da riempire completamente l'area di output, rispettando al tempo stesso le proporzioni originali dell'immagine.  
  
 Nell'esempio riportato di seguito ogni enumerazione di <xref:System.Windows.Media.Stretch> disponibile viene applicata a un oggetto <xref:System.Windows.Controls.Image>.  
  
 Nell'immagine riportata di seguito viene illustrato l'output dell'esempio e l'impatto delle diverse impostazioni di <xref:System.Windows.Controls.Image.Stretch%2A> al momento dell'applicazione a un'immagine.  
  
 ![TileBrush con impostazioni Stretch diverse](../../../../docs/framework/wpf/graphics-multimedia/media/img-mmgraphics-stretchenum.png "img\_mmgraphics\_stretchenum")  
Impostazioni di adattamento diverse  
  
 [!code-xml[ImageElementExample_snip#ImageStretchExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageStretchExample.xaml#imagestretchexamplewholepage)]  
  
### Disegno con le immagini  
 Le immagini possono anche essere visualizzate in un'applicazione tramite il disegno con <xref:System.Windows.Media.Brush>.  I pennelli consentono di disegnare oggetti dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] utilizzando colori semplici e a tinta unita, ma anche insiemi complessi di modelli e immagini.  Per disegnare con le immagini, utilizzare <xref:System.Windows.Media.ImageBrush>.  <xref:System.Windows.Media.ImageBrush> è un tipo di oggetto <xref:System.Windows.Media.TileBrush> che definisce il proprio contenuto come immagine bitmap.  In un oggetto <xref:System.Windows.Media.ImageBrush> viene visualizzata una sola immagine, specificata dalla relativa proprietà <xref:System.Windows.Media.ImageBrush.ImageSource%2A>.  È possibile controllare il modo in cui l'immagine viene adattata, allineata e affiancata, consentendo all'utente di evitare distorsioni e produrre pattern e altri effetti.  Nella figura riportata di seguito vengono illustrati alcuni degli effetti che possono essere ottenuti utilizzando <xref:System.Windows.Media.ImageBrush>.  
  
 ![Esempi di output di ImageBrush](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-mmgraphics-imagebrushexamples.png "wcpsdk\_mmgraphics\_imagebrushexamples")  
Tramite i tratti con immagine è possibile riempire forme, controlli, testo e così via  
  
 Nell'esempio riportato di seguito viene illustrato come disegnare lo sfondo di un pulsante con un'immagine utilizzando <xref:System.Windows.Media.ImageBrush>.  
  
 [!code-xml[UsingImageBrush#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush/CS/PaintingWithImages.xaml#4)]  
  
 Per ulteriori informazioni su <xref:System.Windows.Media.ImageBrush> e sul disegno di immagini vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  
  
<a name="_metadata"></a>   
## Metadati delle immagini  
 Alcuni file di immagine contengono metadati che ne descrivono il contenuto o le caratteristiche.  Ad esempio, la maggior parte delle fotocamere digitali creano immagini che contengono metadati relativi alla fabbricazione e al modello della fotocamera utilizzata per scattare la fotografia.  Ogni formato immagine gestisce i metadati in modo diverso ma [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] offre un sistema uniforme per archiviare e recuperare i metadati per ogni formato immagine supportato.  
  
 L'accesso ai metadati viene fornito tramite la proprietà <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A> di un oggetto <xref:System.Windows.Media.Imaging.BitmapSource>.  <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A> restituisce un oggetto <xref:System.Windows.Media.Imaging.BitmapMetadata> che include tutti i metadati contenuti nell'immagine.  Questi dati possono essere contenuti in uno schema di metadati o in una combinazione di schemi diversi.  [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] supporta i seguenti schemi di metadati di immagine: [!INCLUDE[TLA#tla_exif](../../../../includes/tlasharptla-exif-md.md)], tEXt \(dati testuali PNG\), [!INCLUDE[TLA#tla_ifd](../../../../includes/tlasharptla-ifd-md.md)], [!INCLUDE[TLA#tla_iptc](../../../../includes/tlasharptla-iptc-md.md)] e [!INCLUDE[TLA#tla_xmp](../../../../includes/tlasharptla-xmp-md.md)].  
  
 Per semplificare il processo di lettura dei metadati, <xref:System.Windows.Media.Imaging.BitmapMetadata> fornisce diverse proprietà denominate facilmente accessibili, ad esempio <xref:System.Windows.Media.Imaging.BitmapMetadata.Author%2A>, <xref:System.Windows.Media.Imaging.BitmapMetadata.Title%2A> e <xref:System.Windows.Media.Imaging.BitmapMetadata.CameraModel%2A>.  È inoltre possibile utilizzare molte di queste proprietà denominate per scrivere metadati.  Il lettore di query dei metadati offre supporto aggiuntivo per la lettura dei metadati.  Il metodo <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> viene utilizzato per recuperare un lettore di query dei metadati fornendo una query di stringa come *"\/app1\/exif\/"*.  Nell'esempio riportato di seguito, viene utilizzato <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> per ottenere il testo archiviato nel percorso *"\/Text\/Description"*.  
  
 [!code-cpp[BitmapMetadata#GetQuery](../../../../samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#getquery)]
 [!code-csharp[BitmapMetadata#GetQuery](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#getquery)]
 [!code-vb[BitmapMetadata#GetQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#getquery)]  
  
 Per scrivere metadati, viene utilizzato un writer di query dei metadati.  Tramite <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> viene ottenuto il writer di query e impostato il valore desiderato.  Nell'esempio riportato di seguito, viene utilizzato <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> per scrivere il testo archiviato nel percorso *"\/Text\/Description"*.  
  
 [!code-cpp[BitmapMetadata#SetQuery](../../../../samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#setquery)]
 [!code-csharp[BitmapMetadata#SetQuery](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#setquery)]
 [!code-vb[BitmapMetadata#SetQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#setquery)]  
  
<a name="_extensibility"></a>   
## Estensibilità dei codec  
 Una funzionalità fondamentale di [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] è il modello di estensibilità per i codec di nuove immagini.  Queste interfacce non gestite consentono agli sviluppatori di codec di integrare i codec con [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], in modo da consentire alle applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] di utilizzare automaticamente nuovi formati immagine.  
  
 Per un esempio di [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] di estensibilità, vedere l'[esempio di codec Win32](http://go.microsoft.com/fwlink/?LinkID=160052) \(la pagina potrebbe essere in inglese\).  In questo esempio viene illustrato come creare un decodificatore e un codificatore per un formato immagine personalizzato.  
  
> [!NOTE]
>  Affinché il sistema lo riconosca, è necessario che il codec disponga di una firma digitale.  
  
## Vedere anche  
 <xref:System.Windows.Media.Imaging.BitmapSource>   
 <xref:System.Windows.Media.Imaging.BitmapImage>   
 <xref:System.Windows.Controls.Image>   
 <xref:System.Windows.Media.Imaging.BitmapMetadata>   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Esempio di codec Win32](http://go.microsoft.com/fwlink/?LinkID=160052)