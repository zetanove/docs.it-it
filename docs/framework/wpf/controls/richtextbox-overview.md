---
title: "Cenni generali sul controllo RichTextBox | Microsoft Docs"
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
  - "controlli, RichTextBox"
  - "RichTextBox (controllo) [WPF], informazioni sul controllo RichTextBox"
ms.assetid: c94548b2-c1e9-4b62-b10c-dd8740eb23d8
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni generali sul controllo RichTextBox
Il controllo <xref:System.Windows.Controls.RichTextBox> consente di visualizzare o modificare il contenuto del flusso, compresi i paragrafi, le immagini, le tabelle e così via.  In questo argomento viene presentata la classe <xref:System.Windows.Controls.TextBox> e vengono forniti esempi del relativo utilizzo sia in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] che in [!INCLUDE[TLA#tla_lhcshrp](../../../../includes/tlasharptla-lhcshrp-md.md)].  
  
   
  
<a name="textbox_or_richtextbox"></a>   
## TextBox o RichTextBox?  
 <xref:System.Windows.Controls.RichTextBox> e <xref:System.Windows.Controls.TextBox> consentono agli utenti di modificare il testo; tuttavia, i due controlli vengono utilizzati in scenari differenti.  <xref:System.Windows.Controls.RichTextBox> rappresenta la scelta migliore quando l'utente deve modificare testo formattato, immagini, tabelle o altro contenuto complesso.  Ad esempio, per eseguire la modifica di un documento, di un articolo o di un blog che richiede una formattazione, delle immagini e così via è più opportuno utilizzare un controllo <xref:System.Windows.Controls.RichTextBox>.  Un controllo <xref:System.Windows.Controls.TextBox> richiede una quantità inferiore di risorse di sistema rispetto a <xref:System.Windows.Controls.RichTextBox> ed è la scelta ideale quando è necessario modificare solo del testo normale \(ad esempio  nei form\).  Per ulteriori informazioni su <xref:System.Windows.Controls.TextBox>, vedere [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md).  Nella tabella seguente sono riepilogate le funzionalità principali di <xref:System.Windows.Controls.TextBox> e di <xref:System.Windows.Controls.RichTextBox>.  
  
|Controllo|Controllo ortografico in tempo reale|Menu di scelta rapida|Comandi di formattazione quale <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> \(Ctr\+B\)|Contenuto <xref:System.Windows.Documents.FlowDocument>, ad esempio immagini, paragrafi, tabelle e così via|  
|---------------|------------------------------------------|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.TextBox>|Sì|Sì|No|No.|  
|<xref:System.Windows.Controls.RichTextBox>|Sì|Sì|Sì|Sì|  
  
 **Nota:** anche se <xref:System.Windows.Controls.TextBox> non supporta la formattazione di comandi correlati quale <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> \(Ctr\+B\), molti comandi di base sono supportati da entrambi controlli, ad esempio <xref:System.Windows.Documents.EditingCommands.MoveToLineEnd%2A>.  
  
 Le funzionalità riportate nella tabella precedente saranno illustrate in modo più dettagliato in seguito.  
  
<a name="creating_a_richtextbox"></a>   
## Creazione di un controllo RichTextBox  
 Nel codice riportato di seguito viene illustrata la procedura di creazione di un controllo <xref:System.Windows.Controls.RichTextBox> che può essere utilizzato da un utente per la modifica di contenuto complesso.  
  
 [!code-xml[RichTextBoxMiscSnippets_snip#BasicRichTextBoxExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/BasicRichTextBoxExample.xaml#basicrichtextboxexamplewholepage)]  
  
 In particolare, il contenuto modificato in un controllo <xref:System.Windows.Controls.RichTextBox> è un contenuto di flusso.  Tale contenuto può includere molti tipi di elementi, compresi testo formattato, immagini, elenchi e tabelle.  Per informazioni più approfondite sui documenti dinamici, vedere [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md).  Per includere il contenuto di flusso, un controllo <xref:System.Windows.Controls.RichTextBox> ospita un oggetto <xref:System.Windows.Documents.FlowDocument> che contiene a sua volta il contenuto modificabile.  Per offrire una dimostrazione del contenuto di flusso in un oggetto <xref:System.Windows.Controls.RichTextBox>, nel codice seguente viene illustrata la creazione di un oggetto <xref:System.Windows.Controls.RichTextBox> con un paragrafo e del testo in grassetto.  
  
 [!code-xml[RichTextBoxMiscSnippets_snip#RichTextBoxWithContentExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/RichTextBoxWithContentExample.xaml#richtextboxwithcontentexamplewholepage)]  
  
 [!code-csharp[RichTextBoxMiscSnippets_procedural_snip#BasicRichTextBoxWithContentCodeOnlyExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_procedural_snip/CSharp/BasicRichTextBoxWithContentExample.cs#basicrichtextboxwithcontentcodeonlyexample)]
 [!code-vb[RichTextBoxMiscSnippets_procedural_snip#BasicRichTextBoxWithContentCodeOnlyExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_procedural_snip/visualbasic/basicrichtextboxwithcontentexample.vb#basicrichtextboxwithcontentcodeonlyexample)]  
  
 Nell'immagine seguente viene mostrato il rendering di questo esempio.  
  
 ![RichTextBox con contenuto](../../../../docs/framework/wpf/controls/media/editing-richtextbox-with-content.png "Editing\_RichTextBox\_with\_Content")  
  
 Elementi quali <xref:System.Windows.Documents.Paragraph> e <xref:System.Windows.Documents.Bold> determinano il modo in cui viene visualizzato il contenuto in un oggetto <xref:System.Windows.Controls.RichTextBox>.  Quando un utente modifica il contenuto di <xref:System.Windows.Controls.RichTextBox>, viene cambiato questo contenuto di flusso.  Per ulteriori informazioni sulle funzionalità del contenuto di flusso e sul relativo utilizzo, vedere [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md).  
  
 **Nota:** il comportamento del contenuto del flusso all'interno di <xref:System.Windows.Controls.RichTextBox> è leggermente diverso rispetto al comportamento del contenuto del flusso incluso in altri controlli.  Ad esempio, in un oggetto <xref:System.Windows.Controls.RichTextBox> non sono presenti colonne, pertanto non è previsto un comportamento di ridimensionamento automatico.  Inoltre, funzionalità incorporate quali la ricerca, la modalità di visualizzazione, la navigazione sulle pagine e lo zoom non sono disponibili in un oggetto <xref:System.Windows.Controls.RichTextBox>.  
  
<a name="realtime_spellechecking"></a>   
## Controllo ortografico in tempo reale  
 È possibile abilitare il controllo ortografico in tempo reale in un oggetto <xref:System.Windows.Controls.TextBox> o <xref:System.Windows.Controls.RichTextBox>.  Quando il controllo ortografico è attivo, viene visualizzata una linea rossa sotto le parole che presentano errori ortografici \(vedere l'immagine riportata di seguito\).  
  
 ![TextBox con controllo ortografico](../../../../docs/framework/wpf/controls/media/editing-textbox-with-spellchecking.png "Editing\_TextBox\_with\_Spellchecking")  
  
 Per apprendere la modalità di abilitazione del controllo ortografico, vedere [Attivare il controllo ortografico in un controllo di modifica del testo](../../../../docs/framework/wpf/controls/how-to-enable-spell-checking-in-a-text-editing-control.md).  
  
<a name="context_menu"></a>   
## Menu di scelta rapida  
 Per impostazione predefinita, gli oggetti <xref:System.Windows.Controls.TextBox> e <xref:System.Windows.Controls.RichTextBox> dispongono di un menu di scelta rapida che viene visualizzato quando un utente fa clic con il pulsante destro del mouse nel controllo.  Il menu di scelta rapida consente all'utente di eseguire operazioni di Taglia, Copia o Incolla \(vedere l'immagine di seguito\).  
  
 ![TextBox con menu di scelta rapida](../../../../docs/framework/wpf/controls/media/editing-textbox-with-context-menu.png "Editing\_TextBox\_with\_Context\_Menu")  
  
 È possibile creare un menu di scelta rapida personalizzato ed eseguire l'override di quello predefinito.  Per ulteriori informazioni, vedere [Posizionare un menu di scelta rapida personalizzato in un controllo RichTextBox](../../../../docs/framework/wpf/controls/how-to-position-a-custom-context-menu-in-a-richtextbox.md).  
  
<a name="detect_when_content_changes"></a>   
## Comandi di modifica  
 I comandi di modifica consentono agli utenti di formattare il contenuto modificabile all'interno di un controllo <xref:System.Windows.Controls.RichTextBox>.  Oltre ai comandi di modifica di base, <xref:System.Windows.Controls.RichTextBox> include comandi di formattazione, non supportati da <xref:System.Windows.Controls.TextBox>.  Ad esempio, se si eseguono modifiche in <xref:System.Windows.Controls.RichTextBox>, è possibile premere Ctr\+B per attivare e disattivare la formattazione del testo in grassetto.  Per un elenco completo dei comandi disponibili, vedere <xref:System.Windows.Documents.EditingCommands>.  Oltre a utilizzare i tasti di scelta rapida, è possibile associare i comandi ad altri controlli, quali i pulsanti.  Nell'esempio seguente viene illustrata la procedura per la creazione di una barra degli strumenti semplice, che l'utente potrà utilizzare per modificare la formattazione del testo.  
  
 [!code-xml[RichTextBox_InputPanel_snip#RichTextBoxWithToolBarExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_InputPanel_snip/CS/Window1.xaml#richtextboxwithtoolbarexamplewholepage)]  
  
 Nell'immagine seguente viene mostrata la visualizzazione di questo esempio.  
  
 ![RichTextBox con ToolBar](../../../../docs/framework/wpf/controls/media/editing-richtextbox-with-toobar.png "Editing\_RichTextBox\_with\_TooBar")  
  
<a name="editing_commands"></a>   
## Rilevare le modifiche del contenuto  
 Generalmente, per rilevare tutte le modifiche apportate al testo di un oggetto <xref:System.Windows.Controls.TextBox> o di un oggetto <xref:System.Windows.Controls.RichTextBox> dovrebbe essere utilizzato l'evento <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> anziché <xref:System.Windows.UIElement.KeyDown> come si potrebbe pensare.  Per un esempio, vedere [Rilevare eventuali modifiche del testo in un oggetto TextBox](../../../../docs/framework/wpf/controls/how-to-detect-when-text-in-a-textbox-has-changed.md).  
  
<a name="save_load_and_print_richtextbox_content"></a>   
## Salvare, caricare e stampare il contenuto di un controllo RichTextBox  
 Nell'esempio riportato di seguito viene illustrata la procedura per salvare il contenuto di un oggetto <xref:System.Windows.Controls.RichTextBox> in un file, caricare nuovamente il contenuto nell'oggetto <xref:System.Windows.Controls.RichTextBox> e stamparlo.  Di seguito viene riportato il markup dell'esempio.  
  
 [!code-xml[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/SaveLoadPrintRTB.xaml#saveloadprintrtbexamplewholepage)]  
  
 Di seguito viene riportato il code\-behind dell'esempio.  
  
 [!code-csharp[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/SaveLoadPrintRTB.xaml.cs#saveloadprintrtbcodeexamplewholepage)]
 [!code-vb[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/VisualBasic/SaveLoadPrintRTB.xaml.vb#saveloadprintrtbcodeexamplewholepage)]  
  
## Vedere anche  
 [Procedure relative](../../../../docs/framework/wpf/controls/richtextbox-how-to-topics.md)   
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)