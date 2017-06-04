---
title: "Mapping di propriet&#224; di Windows Form e WPF | Microsoft Docs"
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
  - "interoperabilità [WPF], Windows Form"
  - "mapping di proprietà [interoperabilità WPF]"
  - "Windows Form [WPF], interoperabilità con"
  - "Windows Form, interoperabilità WPF"
  - "WindowsFormsHost (mapping di proprietà dell'elemento)"
ms.assetid: 999d8298-9c04-467d-a453-86e41002057d
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Mapping di propriet&#224; di Windows Form e WPF
Le tecnologie [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] hanno due modelli di proprietà simili, ma diversi.  Il *mapping della proprietà* supporta l'interazione tra le due architetture e fornisce le seguenti funzionalità:  
  
-   Semplifica l'esecuzione del mapping di modifiche delle proprietà pertinenti nell'ambiente host al controllo o all'elemento ospitato.  
  
-   Fornisce la gestione predefinita del mapping della maggior parte delle proprietà più comuni.  
  
-   Consente rimozione, override o estensione semplici delle proprietà predefinite.  
  
-   Garantisce che le modifiche dei valori delle proprietà dell'host vengano rilevate e convertite automaticamente per il controllo o elemento ospitato.  
  
> [!NOTE]
>  Gli eventi di modifica delle proprietà non vengono propagati al controllo o alla gerarchia di elementi che funge da host.  La conversione delle proprietà non viene eseguita se il valore locale di una proprietà non cambia per l'impostazione diretta, gli stili, l'ereditarietà, l'associazione dati o altri meccanismi che modificano il valore della proprietà.  
  
 Utilizzare la proprietà <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A> per l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> e la proprietà <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> per il controllo <xref:System.Windows.Forms.Integration.ElementHost> per accedere al mapping delle proprietà.  
  
## Mapping delle proprietà con l'elemento WindowsFormsHost  
 L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> converte le proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] predefinite nei relativi equivalenti [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] utilizzando la seguente tabella di conversione.  
  
|Windows Presentation Foundation che funge da host|Windows Form|Comportamento di interazione|  
|-------------------------------------------------------|------------------|----------------------------------|  
|<xref:System.Windows.Controls.Control.Background%2A><br /><br /> \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\)|<xref:System.Windows.Forms.Control.BackColor%2A><br /><br /> \(<xref:System.Drawing.Color?displayProperty=fullName>\)|L'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> imposta la proprietà <xref:System.Windows.Forms.Control.BackColor%2A> del controllo ospitato e la proprietà <xref:System.Windows.Forms.Control.BackgroundImage%2A> del controllo ospitato.  Il mapping viene eseguito utilizzando le seguenti regole:<br /><br /> -   Se <xref:System.Windows.Controls.Control.Background%2A> è un colore a tinta unita, viene convertito e utilizzato per impostare la proprietà <xref:System.Windows.Forms.Control.BackColor%2A> del controllo ospitato.  La proprietà <xref:System.Windows.Forms.Control.BackColor%2A> non viene impostata sul controllo ospitato, perché il controllo ospitato può ereditare il valore della proprietà <xref:System.Windows.Forms.Control.BackColor%2A>. **Note:**  Il controllo ospitato non supporta la trasparenza.  Qualsiasi colore assegnato a <xref:System.Windows.Forms.Control.BackColor%2A> deve essere completamente opaco, con un valore alfa di 0xFF. <br /><br /> -   Se <xref:System.Windows.Controls.Control.Background%2A> non è un colore a tinta unita, il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> crea una bitmap dalla proprietà <xref:System.Windows.Controls.Control.Background%2A>.  Il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> assegna questa bitmap alla proprietà <xref:System.Windows.Forms.Control.BackgroundImage%2A> del controllo ospitato.  Ciò fornisce un effetto simile alla trasparenza. **Note:**  È possibile eseguire l'override di questo comportamento oppure è possibile rimuovere il mapping della proprietà <xref:System.Windows.Controls.Control.Background%2A>.|  
|<xref:System.Windows.FrameworkElement.Cursor%2A>|<xref:System.Windows.Forms.Control.Cursor%2A>|Se il mapping predefinito non è stato riassegnato, il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> attraversa la struttura gerarchica dei predecessori finché non rileva un predecessore con la proprietà <xref:System.Windows.FrameworkElement.Cursor%2A> impostata.  Questo valore viene convertito nel cursore di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] più corrispondente.<br /><br /> Se il mapping predefinito per la proprietà <xref:System.Windows.FrameworkElement.ForceCursor%2A> non è stato riassegnato, lo scorrimento si interrompe sul primo predecessore con <xref:System.Windows.FrameworkElement.ForceCursor%2A> impostato su `true`.|  
|<xref:System.Windows.FrameworkElement.FlowDirection%2A><br /><br /> \(<xref:System.Windows.FlowDirection?displayProperty=fullName>\)|<xref:System.Windows.Forms.Control.RightToLeft%2A><br /><br /> \(<xref:System.Windows.Forms.RightToLeft?displayProperty=fullName>\)|<xref:System.Windows.FlowDirection> corrisponde a <xref:System.Windows.Forms.RightToLeft>.<br /><br /> <xref:System.Windows.FlowDirection> corrisponde a <xref:System.Windows.Forms.RightToLeft>.<br /><br /> <xref:System.Windows.Forms.RightToLeft> non mappato.<br /><br /> <xref:System.Windows.FlowDirection?displayProperty=fullName> corrisponde a <xref:System.Windows.Forms.RightToLeft?displayProperty=fullName>.|  
|<xref:System.Windows.Controls.Control.FontStyle%2A>|La proprietà <xref:System.Drawing.Font.Style%2A> dell'oggetto <xref:System.Drawing.Font?displayProperty=fullName> del controllo ospitato|La serie di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene convertita in un oggetto <xref:System.Drawing.Font> corrispondente.  Quando una di queste proprietà viene modificata, viene creato un nuovo oggetto <xref:System.Drawing.Font>.  Per <xref:System.Windows.FontStyles.Normal%2A>: <xref:System.Drawing.FontStyle> è disabilitato.  Per <xref:System.Windows.FontStyles.Italic%2A> o <xref:System.Windows.FontStyles.Oblique%2A>: <xref:System.Drawing.FontStyle> è abilitato.|  
|<xref:System.Windows.Controls.Control.FontWeight%2A>|La proprietà <xref:System.Drawing.Font.Style%2A> dell'oggetto <xref:System.Drawing.Font?displayProperty=fullName> del controllo ospitato|La serie di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene convertita in un oggetto <xref:System.Drawing.Font> corrispondente.  Quando una di queste proprietà viene modificata, viene creato un nuovo oggetto <xref:System.Drawing.Font>.  Per <xref:System.Windows.FontWeights.Black%2A>, <xref:System.Windows.FontWeights.Bold%2A>, <xref:System.Windows.FontWeights.DemiBold%2A>, <xref:System.Windows.FontWeights.ExtraBold%2A>, <xref:System.Windows.FontWeights.Heavy%2A>, <xref:System.Windows.FontWeights.Medium%2A>, <xref:System.Windows.FontWeights.SemiBold%2A> o <xref:System.Windows.FontWeights.UltraBold%2A>: <xref:System.Drawing.FontStyle> è abilitato.  Per <xref:System.Windows.FontWeights.ExtraLight%2A>, <xref:System.Windows.FontWeights.Light%2A>, <xref:System.Windows.FontWeights.Normal%2A>, <xref:System.Windows.FontWeights.Regular%2A>, <xref:System.Windows.FontWeights.Thin%2A> o <xref:System.Windows.FontWeights.UltraLight%2A>: <xref:System.Drawing.FontStyle> è disabilitato.|  
|<xref:System.Windows.Controls.Control.FontFamily%2A><br /><br /> <xref:System.Windows.Controls.Control.FontSize%2A><br /><br /> <xref:System.Windows.Controls.Control.FontStretch%2A><br /><br /> <xref:System.Windows.Controls.Control.FontStyle%2A><br /><br /> <xref:System.Windows.Controls.Control.FontWeight%2A>|<xref:System.Windows.Forms.Control.Font%2A><br /><br /> \(<xref:System.Drawing.Font?displayProperty=fullName>\)|La serie di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene convertita in un oggetto <xref:System.Drawing.Font> corrispondente.  Quando una di queste proprietà viene modificata, viene creato un nuovo oggetto <xref:System.Drawing.Font>.  Il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato viene ridimensionato in base alla dimensione del carattere.<br /><br /> La dimensione del carattere in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è espressa come un novantaseiesimo di pollice e in [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] come un settantaduesimo di pollice.  La conversione corrispondente è:<br /><br /> Dimensione del carattere di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] \= dimensione del carattere di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] \* 72,0\/96,0.|  
|<xref:System.Windows.Controls.Control.Foreground%2A><br /><br /> \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\)|<xref:System.Windows.Forms.Control.ForeColor%2A><br /><br /> \(<xref:System.Drawing.Color?displayProperty=fullName>\)|Il mapping della proprietà <xref:System.Windows.Controls.Control.Foreground%2A> viene eseguito utilizzando le seguenti regole:<br /><br /> -   Se <xref:System.Windows.Controls.Control.Foreground%2A> è <xref:System.Windows.Media.SolidColorBrush>, utilizzare <xref:System.Windows.Media.SolidColorBrush.Color%2A> per <xref:System.Windows.Forms.Control.ForeColor%2A>.<br />-   Se <xref:System.Windows.Controls.Control.Foreground%2A> è <xref:System.Windows.Media.GradientBrush>, utilizzare il colore di <xref:System.Windows.Media.GradientStop> con il valore di offset più basso per <xref:System.Windows.Forms.Control.ForeColor%2A>.<br />-   Per qualsiasi altro tipo <xref:System.Windows.Media.Brush>, lasciare <xref:System.Windows.Forms.Control.ForeColor%2A> invariato.  Ciò significa che viene utilizzato il valore predefinito.|  
|<xref:System.Windows.UIElement.IsEnabled%2A>|<xref:System.Windows.Forms.Control.Enabled%2A>|Quando <xref:System.Windows.UIElement.IsEnabled%2A> è impostato, l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> imposta la proprietà <xref:System.Windows.Forms.Control.Enabled%2A> del controllo ospitato.|  
|<xref:System.Windows.Controls.Control.Padding%2A>|<xref:System.Windows.Forms.Control.Padding%2A>|Tutti i quattro valori della proprietà <xref:System.Windows.Forms.Control.Padding%2A> del controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato sono impostati sullo stesso valore di <xref:System.Windows.Thickness>.<br /><br /> -   I valori maggiori di <xref:System.Int32.MaxValue> vengono impostati su <xref:System.Int32.MaxValue>.<br />-   I valori minori di <xref:System.Int32.MinValue> vengono impostati su <xref:System.Int32.MinValue>.|  
|<xref:System.Windows.UIElement.Visibility%2A>|<xref:System.Windows.Forms.Control.Visible%2A>|-   <xref:System.Windows.Visibility> corrisponde a <xref:System.Windows.Forms.Control.Visible%2A> \= `true`.  Il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] è visibile.  L'impostazione esplicita della proprietà <xref:System.Windows.Forms.Control.Visible%2A> del controllo ospitato su `false` non è un'operazione consigliata.<br />-   <xref:System.Windows.Visibility> corrisponde a <xref:System.Windows.Forms.Control.Visible%2A> \= `true` o a `false`.  Il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato non viene tracciato e l'area relativa viene compressa.<br />-   <xref:System.Windows.Visibility>: il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato occupa spazio del layout, ma non è visibile.  In questo caso la proprietà <xref:System.Windows.Forms.Control.Visible%2A> è impostata su `true`.  L'impostazione esplicita della proprietà <xref:System.Windows.Forms.Control.Visible%2A> del controllo ospitato su `false` non è un'operazione consigliata.|  
  
 Le proprietà associate degli elementi contenitore sono completamente supportate dall'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
 Per ulteriori informazioni, vedere [Procedura dettagliata: mapping di proprietà tramite l'elemento WindowsFormsHost](../../../../docs/framework/wpf/advanced/walkthrough-mapping-properties-using-the-windowsformshost-element.md).  
  
## Aggiornamenti relativi alle proprietà padre  
 Le modifiche alla maggior parte delle proprietà padre causano notifiche al controllo figlio ospitato.  L'elenco riportato di seguito descrive le proprietà che non causano notifiche quando i valori cambiano.  
  
-   <xref:System.Windows.Controls.Control.Background%2A>  
  
-   <xref:System.Windows.FrameworkElement.Cursor%2A>  
  
-   <xref:System.Windows.FrameworkElement.ForceCursor%2A>  
  
-   <xref:System.Windows.UIElement.Visibility%2A>  
  
 Se ad esempio si modifica il valore della proprietà <xref:System.Windows.Controls.Control.Background%2A> dell'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost>, la proprietà <xref:System.Windows.Forms.Control.BackColor%2A> del controllo ospitato non cambia.  
  
## Mapping delle proprietà con il controllo ElementHost  
 Le proprietà riportate di seguito forniscono notifiche di modifica incorporate.  Non chiamare il metodo <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> durante il mapping di queste proprietà:  
  
-   AutoSize  
  
-   BackColor  
  
-   BackgroundImage  
  
-   BackgroundImageLayout  
  
-   BindingContext  
  
-   CausesValidation  
  
-   ContextMenu  
  
-   ContextMenuStrip  
  
-   Cursore  
  
-   Dock  
  
-   Enabled  
  
-   Tipo di carattere  
  
-   ForeColor  
  
-   Location  
  
-   Margin  
  
-   Riempimento  
  
-   Padre  
  
-   Region  
  
-   RightToLeft  
  
-   Dimensione  
  
-   TabIndex  
  
-   TabStop  
  
-   Text  
  
-   Visible  
  
 Il controllo <xref:System.Windows.Forms.Integration.ElementHost> converte le proprietà di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] predefinite nei relativi equivalenti di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] mediante la tabella di conversione riportata di seguito.  
  
 Per ulteriori informazioni, vedere [Procedura dettagliata: mapping delle proprietà tramite il controllo ElementHost](../../../../docs/framework/wpf/advanced/walkthrough-mapping-properties-using-the-elementhost-control.md).  
  
|Windows Form che funge da host|Windows Presentation Foundation|Comportamento di interazione|  
|------------------------------------|-------------------------------------|----------------------------------|  
|<xref:System.Windows.Forms.Control.BackColor%2A><br /><br /> \(<xref:System.Drawing.Color?displayProperty=fullName>\)|<xref:System.Windows.Controls.Control.Background%2A><br /><br /> \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\) sull'elemento ospitato|L'impostazione di questa proprietà impone un aggiornamento con <xref:System.Windows.Media.ImageBrush>.  Se la proprietà <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> è impostata su `false` \(il valore predefinito\), <xref:System.Windows.Media.ImageBrush> si basa sull'aspetto del controllo <xref:System.Windows.Forms.Integration.ElementHost>, comprese le proprietà <xref:System.Windows.Forms.Control.BackColor%2A>, <xref:System.Windows.Forms.Control.BackgroundImage%2A>, <xref:System.Windows.Forms.Control.BackgroundImageLayout%2A> relative e qualsiasi gestore dell'evento Paint associato.<br /><br /> Se la proprietà <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> è impostata su `true`, <xref:System.Windows.Media.ImageBrush> si basa sull'aspetto dell'elemento padre del controllo <xref:System.Windows.Forms.Integration.ElementHost>, comprese le proprietà <xref:System.Windows.Forms.Control.BackColor%2A>, <xref:System.Windows.Forms.Control.BackgroundImage%2A>, <xref:System.Windows.Forms.Control.BackgroundImageLayout%2A> dell'elemento padre e qualsiasi gestore dell'evento Paint associato.|  
|<xref:System.Windows.Forms.Control.BackgroundImage%2A><br /><br /> \(<xref:System.Drawing.Image?displayProperty=fullName>\)|<xref:System.Windows.Controls.Control.Background%2A><br /><br /> \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\) sull'elemento ospitato|L'impostazione di questa proprietà causa lo stesso comportamento descritto per il mapping di <xref:System.Windows.Forms.Control.BackColor%2A>.|  
|<xref:System.Windows.Forms.Control.BackgroundImageLayout%2A>|<xref:System.Windows.Controls.Control.Background%2A><br /><br /> \(<xref:System.Windows.Media.Brush?displayProperty=fullName>\) sull'elemento ospitato|L'impostazione di questa proprietà causa lo stesso comportamento descritto per il mapping di <xref:System.Windows.Forms.Control.BackColor%2A>.|  
|<xref:System.Windows.Forms.Control.Cursor%2A><br /><br /> \(<xref:System.Windows.Forms.Cursor?displayProperty=fullName>\)|<xref:System.Windows.FrameworkElement.Cursor%2A><br /><br /> \(<xref:System.Windows.Input.Cursor?displayProperty=fullName>\)|Il cursore standard [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] viene convertito nel cursore standard [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] corrispondente.  Se [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non è un cursore standard, viene assegnato quello predefinito.|  
|<xref:System.Windows.Forms.Control.Enabled%2A>|<xref:System.Windows.UIElement.IsEnabled%2A>|Quando <xref:System.Windows.Forms.Control.Enabled%2A> è impostato, il controllo <xref:System.Windows.Forms.Integration.ElementHost> imposta la proprietà <xref:System.Windows.UIElement.IsEnabled%2A> dell'elemento ospitato.|  
|<xref:System.Windows.Forms.Control.Font%2A><br /><br /> \(<xref:System.Drawing.Font?displayProperty=fullName>\)|<xref:System.Windows.Controls.Control.FontFamily%2A><br /><br /> <xref:System.Windows.Controls.Control.FontSize%2A><br /><br /> <xref:System.Windows.Controls.Control.FontStretch%2A><br /><br /> <xref:System.Windows.Controls.Control.FontStyle%2A><br /><br /> <xref:System.Windows.Controls.Control.FontWeight%2A>|Il valore <xref:System.Windows.Forms.Control.Font%2A> viene convertito in una serie corrispondente di proprietà del carattere di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|  
|<xref:System.Drawing.Font.Bold%2A>|<xref:System.Windows.Controls.Control.FontWeight%2A> sull'elemento ospitato|Se <xref:System.Drawing.Font.Bold%2A> è `true`, <xref:System.Windows.Controls.Control.FontWeight%2A> viene impostato su <xref:System.Windows.FontWeights.Bold%2A>.<br /><br /> Se <xref:System.Drawing.Font.Bold%2A> è `false`, <xref:System.Windows.Controls.Control.FontWeight%2A> viene impostato su <xref:System.Windows.FontWeights.Normal%2A>.|  
|<xref:System.Drawing.Font.Italic%2A>|<xref:System.Windows.Controls.Control.FontStyle%2A> sull'elemento ospitato|Se <xref:System.Drawing.Font.Italic%2A> è `true`, <xref:System.Windows.Controls.Control.FontStyle%2A> viene impostato su <xref:System.Windows.FontStyles.Italic%2A>.<br /><br /> Se <xref:System.Drawing.Font.Italic%2A> è `false`, <xref:System.Windows.Controls.Control.FontStyle%2A> viene impostato su <xref:System.Windows.FontStyles.Normal%2A>.|  
|<xref:System.Drawing.Font.Strikeout%2A>|<xref:System.Windows.TextDecorations> sull'elemento ospitato|Valido solo per l'hosting di un controllo <xref:System.Windows.Controls.TextBlock>.|  
|<xref:System.Drawing.Font.Underline%2A>|<xref:System.Windows.TextDecorations> sull'elemento ospitato|Valido solo per l'hosting di un controllo <xref:System.Windows.Controls.TextBlock>.|  
|<xref:System.Windows.Forms.Control.RightToLeft%2A><br /><br /> \(<xref:System.Windows.Forms.RightToLeft?displayProperty=fullName>\)|<xref:System.Windows.FrameworkElement.FlowDirection%2A><br /><br /> \(<xref:System.Windows.FlowDirection>\)|<xref:System.Windows.Forms.RightToLeft> corrisponde a <xref:System.Windows.FlowDirection>.<br /><br /> <xref:System.Windows.Forms.RightToLeft> corrisponde a <xref:System.Windows.FlowDirection>.|  
|<xref:System.Windows.Forms.Control.Visible%2A>|<xref:System.Windows.UIElement.Visibility%2A>|Il controllo <xref:System.Windows.Forms.Integration.ElementHost> imposta la proprietà <xref:System.Windows.UIElement.Visibility%2A> dell'elemento ospitato utilizzando le seguenti regole:<br /><br /> -   <xref:System.Windows.Forms.Control.Visible%2A> \= `true` corrisponde a <xref:System.Windows.Visibility>.<br />-   <xref:System.Windows.Forms.Control.Visible%2A> \= `false` corrisponde a <xref:System.Windows.Visibility>.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)   
 [Interoperatività di WPF e Windows Form](../../../../docs/framework/wpf/advanced/wpf-and-windows-forms-interoperation.md)   
 [Procedura dettagliata: mapping di proprietà tramite l'elemento WindowsFormsHost](../../../../docs/framework/wpf/advanced/walkthrough-mapping-properties-using-the-windowsformshost-element.md)   
 [Procedura dettagliata: mapping delle proprietà tramite il controllo ElementHost](../../../../docs/framework/wpf/advanced/walkthrough-mapping-properties-using-the-elementhost-control.md)