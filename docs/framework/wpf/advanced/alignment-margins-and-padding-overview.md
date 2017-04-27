---
title: "Panoramica su allineamento, margini e spaziatura interna | Microsoft Docs"
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
  - "allineamento"
  - "classi, FrameworkElement"
  - "FrameworkElement (classe)"
  - "margini"
  - "spaziatura"
ms.assetid: 9c6a2009-9b86-4e40-8605-0a2664dc3973
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Panoramica su allineamento, margini e spaziatura interna
La classe <xref:System.Windows.FrameworkElement> espone molte proprietà utilizzate per posizionare con precisione gli elementi figlio.  In questo argomento vengono descritte quattro delle proprietà più importanti: <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, <xref:System.Windows.Controls.Border.Padding%2A> e <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>.  È fondamentale comprendere gli effetti di queste proprietà, perché forniscono la base per controllare la posizione degli elementi nelle applicazioni [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
   
  
<a name="wcpsdk_layout_amp_introduction"></a>   
## Introduzione al posizionamento degli elementi  
 Utilizzando [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è possibile posizionare gli elementi in molti modi.  Tuttavia, per ottenere il layout ideale non è sufficiente scegliere semplicemente l'elemento <xref:System.Windows.Controls.Panel> appropriato.  Un controllo accurato del posizionamento richiede una buona conoscenza delle proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, <xref:System.Windows.Controls.Border.Padding%2A> e <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>.  
  
 Nell'immagine seguente è illustrato uno scenario di layout in cui vengono utilizzate diverse proprietà di posizionamento.  
  
 ![Esempio di proprietà di posizionamento WPF](../../../../docs/framework/wpf/advanced/media/layout-margins-padding-alignment-graphic1.png "layout\_margins\_padding\_alignment\_graphic1")  
  
 A prima vista, può sembrare che gli elementi <xref:System.Windows.Controls.Button> siano stati posizionati in modo casuale.  Le posizioni sono in realtà controllate con precisione utilizzando una combinazione di margini, allineamento e spaziatura interna.  
  
 Nell'esempio seguente viene descritto come creare il layout dell'immagine precedente.  Un elemento <xref:System.Windows.Controls.Border> incapsula un elemento <xref:System.Windows.Controls.StackPanel> padre, con un valore di <xref:System.Windows.Controls.Border.Padding%2A> pari a 15 [Device Independent Pixel](GTMT).  Ciò spiega la banda <xref:System.Windows.Media.Brushes.LightBlue%2A> stretta che circonda l'elemento <xref:System.Windows.Controls.StackPanel> figlio.  Gli elementi figlio dell'oggetto <xref:System.Windows.Controls.StackPanel> vengono utilizzati per illustrare ognuna delle varie proprietà di posizionamento descritte in questo argomento.  Vengono utilizzati tre elementi <xref:System.Windows.Controls.Button> per illustrare le proprietà <xref:System.Windows.FrameworkElement.Margin%2A> e <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>.  
  
 [!code-csharp[MPALayoutSampleIntro#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutSampleIntro/CSharp/MPA_Layout_Sample_Intro.cs#1)]
 [!code-vb[MPALayoutSampleIntro#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutSampleIntro/VisualBasic/MPALayoutIntro.vb#1)]  
  
 Nel diagramma seguente viene fornita una visualizzazione dettagliata delle varie proprietà di posizionamento utilizzate nell'esempio precedente.  Nelle sezioni successive di questo argomento viene descritto in maggior dettaglio come utilizzare ogni proprietà di posizionamento.  
  
 ![Proprietà di posizionamento con callout nella schermata](../../../../docs/framework/wpf/advanced/media/layout-margins-padding-alignment-graphic2.png "layout\_margins\_padding\_alignment\_graphic2")  
  
<a name="wcpsdk_layout_amp_alignment_properties"></a>   
## Informazioni sulle proprietà di allineamento  
 Le proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> e <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> descrivono come deve essere posizionato un elemento figlio all'interno dello spazio di layout allocato di un elemento padre.  Utilizzando insieme queste proprietà, è possibile posizionare con precisione gli elementi figlio.  Ad esempio, gli elementi figlio di un oggetto <xref:System.Windows.Controls.DockPanel> possono specificare quattro allineamenti orizzontali diversi: <xref:System.Windows.HorizontalAlignment>, <xref:System.Windows.HorizontalAlignment> o <xref:System.Windows.HorizontalAlignment> oppure <xref:System.Windows.HorizontalAlignment> per riempire lo spazio disponibile.  Per il posizionamento verticale sono disponibili valori analoghi.  
  
> [!NOTE]
>  Le proprietà <xref:System.Windows.FrameworkElement.Height%2A> e <xref:System.Windows.FrameworkElement.Width%2A> impostate in modo esplicito su un elemento hanno la precedenza sul valore della proprietà <xref:System.Windows.HorizontalAlignment>.  Se si tenta di impostare le proprietà <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.Width%2A>e il valore `Stretch` della proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, la richiesta `Stretch` viene ignorata.  
  
<a name="wcpsdk_layout_amp_horizontalalignment_properties"></a>   
### Proprietà HorizontalAlignment  
 La proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> dichiara le caratteristiche di allineamento orizzontale da applicare agli elementi figlio.  Nella tabella seguente viene illustrato ognuno dei valori possibili della proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>.  
  
|Membro|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.HorizontalAlignment>|Gli elementi figlio sono allineati a sinistra dello spazio di layout allocato dell'elemento padre.|  
|<xref:System.Windows.HorizontalAlignment>|Gli elementi figlio sono allineati al centro dello spazio di layout allocato dell'elemento padre.|  
|<xref:System.Windows.HorizontalAlignment>|Gli elementi figlio sono allineati a destra dello spazio di layout allocato dell'elemento padre.|  
|<xref:System.Windows.HorizontalAlignment> \(impostazione predefinita\)|Gli elementi figlio vengono estesi fino a riempire lo spazio di layout allocato dell'elemento padre.  I valori espliciti <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> hanno la precedenza.|  
  
 Nell'esempio seguente viene illustrato come applicare la proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> agli elementi <xref:System.Windows.Controls.Button>.  Viene mostrato ogni valore dell'attributo per illustrare in modo più efficace i vari comportamenti di rendering.  
  
 [!code-csharp[MPALayoutHorizontalAlignment#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/CSharp/MPA_Layout_HorizontalAlignment.cs#2)]
 [!code-vb[MPALayoutHorizontalAlignment#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/VisualBasic/MPA_Layout_HorizontalAlignment.vb#2)]  
  
 Il risultato del codice precedente è simile a quello riportato nell'immagine seguente.  Gli effetti del posizionamento di ogni valore di <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> sono visibili nell'illustrazione.  
  
 ![Esempio di HorizontalAlignment](../../../../docs/framework/wpf/advanced/media/layout-horizontal-alignment-graphic.png "layout\_horizontal\_alignment\_graphic")  
  
<a name="wcpsdk_layout_amp_verticalalignment_properties"></a>   
### Proprietà VerticalAlignment  
 La proprietà <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> descrive le caratteristiche di allineamento verticale da applicare agli elementi figlio.  Nella tabella seguente viene illustrato ognuno dei valori possibili della proprietà <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>.  
  
|Membro|Descrizione|  
|------------|-----------------|  
|<xref:System.Windows.VerticalAlignment>|Gli elementi figlio sono allineati nella parte superiore dello spazio di layout allocato dell'elemento padre.|  
|<xref:System.Windows.VerticalAlignment>|Gli elementi figlio sono allineati al centro dello spazio di layout allocato dell'elemento padre.|  
|<xref:System.Windows.VerticalAlignment>|Gli elementi figlio sono allineati nella parte inferiore dello spazio di layout allocato dell'elemento padre.|  
|<xref:System.Windows.VerticalAlignment> \(impostazione predefinita\)|Gli elementi figlio vengono estesi fino a riempire lo spazio di layout allocato dell'elemento padre.  I valori espliciti <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> hanno la precedenza.|  
  
 Nell'esempio seguente viene illustrato come applicare la proprietà <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> agli elementi <xref:System.Windows.Controls.Button>.  Viene mostrato ogni valore dell'attributo per illustrare in modo più efficace i vari comportamenti di rendering.  Ai fini dell'esempio, come elemento padre viene utilizzato un elemento <xref:System.Windows.Controls.Grid> con griglia visibile per illustrare il comportamento di layout di ogni valore della proprietà.  
  
 [!code-csharp[MPALayoutVerticalAlignment#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutVerticalAlignment/CSharp/MPA_Layout_VerticalAlignment.cs#2)]
 [!code-vb[MPALayoutVerticalAlignment#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutVerticalAlignment/VisualBasic/MPA_Layout_VerticalAlignment.vb#2)]
 [!code-xml[MPALayoutVerticalAlignment#2](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MPALayoutVerticalAlignment/XAML/default.xaml#2)]  
  
 Il risultato del codice precedente è simile a quello riportato nell'immagine seguente.  Gli effetti del posizionamento di ogni valore di <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> sono visibili nell'illustrazione.  
  
 ![Esempio di proprietà VerticalAlignment](../../../../docs/framework/wpf/advanced/media/layout-vertical-alignment-graphic.png "layout\_vertical\_alignment\_graphic")  
  
<a name="wcpsdk_layout_amp_margin_properties"></a>   
## Informazioni sulle proprietà Margin  
 La proprietà <xref:System.Windows.FrameworkElement.Margin%2A> descrive la distanza tra un elemento e l'elemento figlio o i peer.  I valori di <xref:System.Windows.FrameworkElement.Margin%2A> possono essere uniformi, utilizzando una sintassi come `Margin="20"`.  Con questa sintassi, all'elemento viene applicato un valore uniforme di <xref:System.Windows.FrameworkElement.Margin%2A> pari a 20 [DIP \(Device Independent Pixel\)](GTMT).  I valori di <xref:System.Windows.FrameworkElement.Margin%2A> possono anche essere quattro valori distinti, ognuno che descrive un margine distinto da applicare alla parte sinistra, superiore, destra e inferiore \(in quest'ordine\), ad esempio `Margin="0,10,5,25"`.  L'utilizzo corretto della proprietà <xref:System.Windows.FrameworkElement.Margin%2A> consente di esercitare un controllo molto accurato sulla posizione di rendering di un elemento e degli elementi adiacenti o figlio.  
  
> [!NOTE]
>  Un margine diverso da zero applica uno spazio all'esterno delle proprietà <xref:System.Windows.FrameworkElement.ActualWidth%2A> e <xref:System.Windows.FrameworkElement.ActualHeight%2A> dell'elemento.  
  
 Nell'esempio seguente viene illustrato come applicare margini uniformi intorno a un gruppo di elementi <xref:System.Windows.Controls.Button>.  Gli elementi <xref:System.Windows.Controls.Button> sono disposti a intervalli regolari con un'area di margine da 10 pixel in ogni direzione.  
  
 [!code-cpp[MarginPaddingAlignmentSample#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#1)]
 [!code-csharp[MarginPaddingAlignmentSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#1)]
 [!code-vb[MarginPaddingAlignmentSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#1)]
 [!code-xml[MarginPaddingAlignmentSample#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#1)]  
  
 In diverse situazioni un margine uniforme non è appropriato.  In questi casi, è possibile applicare una spaziatura non uniforme.  Nell'esempio seguente viene illustrato come applicare una spaziatura dei margini non uniforme agli elementi figlio.  I margini sono descritti in quest'ordine: sinistro, superiore, destro, inferiore.  
  
 [!code-cpp[MarginPaddingAlignmentSample#2](../../../../samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#2)]
 [!code-csharp[MarginPaddingAlignmentSample#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#2)]
 [!code-vb[MarginPaddingAlignmentSample#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#2)]
 [!code-xml[MarginPaddingAlignmentSample#2](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#2)]  
  
<a name="wcpsdk_layout_amp_padding_properties"></a>   
## Informazioni sulla proprietà Padding  
 Padding è simile a <xref:System.Windows.FrameworkElement.Margin%2A> per molti aspetti.  La proprietà Padding è esposta solo su poche classi, principalmente per praticità: <xref:System.Windows.Documents.Block>, <xref:System.Windows.Controls.Border>, <xref:System.Windows.Controls.Control>e <xref:System.Windows.Controls.TextBlock> sono esempi di classi che espongono una proprietà Padding.  La proprietà <xref:System.Windows.Controls.Border.Padding%2A> ingrandisce le dimensioni effettive di un elemento figlio in base al valore <xref:System.Windows.Thickness> specificato.  
  
 Nell'esempio seguente viene illustrato come applicare la proprietà <xref:System.Windows.Controls.Border.Padding%2A> a un elemento <xref:System.Windows.Controls.Border> padre.  
  
 [!code-cpp[MarginPaddingAlignmentSample#3](../../../../samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#3)]
 [!code-csharp[MarginPaddingAlignmentSample#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#3)]
 [!code-vb[MarginPaddingAlignmentSample#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#3)]
 [!code-xml[MarginPaddingAlignmentSample#3](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#3)]  
  
<a name="wcpsdk_layout_amp_summary"></a>   
## Utilizzo di allineamento, margini e spaziatura interna in un'applicazione  
 Le proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, <xref:System.Windows.Controls.Border.Padding%2A> e <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> forniscono il controllo sul posizionamento necessario per creare un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] complessa.  È possibile utilizzare gli effetti di ogni proprietà per modificare il posizionamento degli elementi figlio, ottenendo in questo modo flessibilità nella creazione di applicazioni ed esperienze utente dinamiche.  
  
 Nell'esempio seguente viene illustrato ognuno dei concetti descritti in questo argomento.  Sulla base dell'infrastruttura descritta nel primo esempio di questo argomento, in questo esempio viene aggiunto un oggetto <xref:System.Windows.Controls.Grid> come elemento figlio dell'oggetto <xref:System.Windows.Controls.Border>.  <xref:System.Windows.Controls.Border.Padding%2A> viene applicata all'elemento <xref:System.Windows.Controls.Border> padre.  L'oggetto <xref:System.Windows.Controls.Grid> viene utilizzato per dividere lo spazio tra tre elementi <xref:System.Windows.Controls.StackPanel>.  Vengono ancora una volta utilizzati gli elementi <xref:System.Windows.Controls.Button> per illustrare i vari effetti delle proprietà <xref:System.Windows.FrameworkElement.Margin%2A> e <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>.  <xref:System.Windows.Controls.TextBlock> vengono aggiunti a ogni oggetto <xref:System.Windows.Controls.ColumnDefinition> per definire in modo più dettagliato le varie proprietà applicate agli elementi <xref:System.Windows.Controls.Button> in ogni colonna.  
  
 [!code-cpp[MarginPaddingAlignmentSample#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#4)]
 [!code-csharp[MarginPaddingAlignmentSample#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#4)]
 [!code-vb[MarginPaddingAlignmentSample#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#4)]
 [!code-xml[MarginPaddingAlignmentSample#4](../../../../samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#4)]  
  
 Dopo la compilazione, l'applicazione precedente genera un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di aspetto simile al seguente.  Gli effetti dei vari valori delle proprietà sono evidenti nella spaziatura tra gli elementi e i valori delle proprietà significativi per gli elementi in ogni colonna sono illustrati all'interno di oggetti <xref:System.Windows.Controls.TextBlock>.  
  
 ![Alcune proprietà di posizionamento in un'applicazione](../../../../docs/framework/wpf/advanced/media/layout-margins-padding-aligment-graphic3.png "layout\_margins\_padding\_aligment\_graphic3")  
  
<a name="wcpsdk_layout_amp_alignment_whatsnext"></a>   
## Argomenti successivi  
 Le proprietà di posizionamento definite dalla classe <xref:System.Windows.FrameworkElement> consentono un controllo accurato del posizionamento degli elementi all'interno delle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Quelle descritte qui sono dunque le diverse tecniche che permettono di posizionare in modo più efficace gli elementi utilizzando [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Sono inoltre disponibili ulteriori risorse in cui il layout di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene descritto in modo più particolareggiato.  L'argomento [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md) contiene ulteriori informazioni sui vari elementi <xref:System.Windows.Controls.Panel>.  Nell'argomento [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md) vengono presentate tecniche avanzate in cui si utilizzano gli elementi del layout per posizionare i componenti e associare le relative azioni a origini dati.  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>   
 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>   
 <xref:System.Windows.FrameworkElement.Margin%2A>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Layout](../../../../docs/framework/wpf/advanced/layout.md)   
 [Esempio di raccolte di layout WPF](http://go.microsoft.com/fwlink/?LinkID=160054)