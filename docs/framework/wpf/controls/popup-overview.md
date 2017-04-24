---
title: "Cenni preliminari sul controllo Popup | Microsoft Docs"
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
  - "controlli, Popup"
  - "Popup (controllo) [WPF], informazioni sul controllo Popup"
ms.assetid: 774f53ca-bff8-470e-9ce9-3928b4cf3d4c
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# Cenni preliminari sul controllo Popup
Il controllo <xref:System.Windows.Controls.Primitives.Popup> consente di visualizzare il contenuto relativo a uno specifico elemento o coordinata dello schermo in una finestra separata, mobile rispetto alla finestra dell'applicazione corrente.  In questo argomento viene descritto il controllo <xref:System.Windows.Controls.Primitives.Popup> e vengono fornite informazioni sul relativo utilizzo.  
  
   
  
<a name="What_Is_a_Popup_"></a>   
## Definizione di un controllo Popup  
 Un controllo <xref:System.Windows.Controls.Primitives.Popup> visualizza il contenuto in una finestra separata relativa a un elemento o punto dello schermo.  Quando il controllo <xref:System.Windows.Controls.Primitives.Popup> è visibile, la proprietà <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> è impostata su `true`.  
  
> [!NOTE]
>  Un oggetto <xref:System.Windows.Controls.Primitives.Popup> non si apre automaticamente quando il puntatore del mouse si sposta sul relativo oggetto padre.  Se si desidera aprire automaticamente un <xref:System.Windows.Controls.Primitives.Popup>, utilizzare la classe <xref:System.Windows.Controls.ToolTip> o <xref:System.Windows.Controls.ToolTipService>.  Per ulteriori informazioni, vedere [Panoramica sul controllo ToolTip](../../../../docs/framework/wpf/controls/tooltip-overview.md).  
  
<a name="APopupExample"></a>   
## Creazione di un controllo Popup  
 Nell'esempio seguente viene illustrato come definire un controllo <xref:System.Windows.Controls.Primitives.Popup> che è l'elemento figlio di un controllo <xref:System.Windows.Controls.Button>.  Poiché <xref:System.Windows.Controls.Button> può avere un solo elemento figlio, in questo esempio il testo per i controlli <xref:System.Windows.Controls.Button> e <xref:System.Windows.Controls.Primitives.Popup> viene inserito in un oggetto <xref:System.Windows.Controls.StackPanel>.  Il contenuto di <xref:System.Windows.Controls.Primitives.Popup> viene inserito in un controllo <xref:System.Windows.Controls.TextBlock> che visualizza il relativo testo in una finestra separata mobile rispetto alla finestra dell'applicazione accanto al relativo controllo <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[PopupSimple#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#1)]  
  
 [!code-xml[PopupSimple#CreatePopupCodeXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupSimple/CSharp/Window1.xaml#createpopupcodexaml)]  
  
<a name="PopupUses"></a>   
## Controlli che implementano un controllo Popup  
 È possibile compilare controlli <xref:System.Windows.Controls.Primitives.Popup> in altri controlli.  I controlli riportati di seguito implementano il controllo <xref:System.Windows.Controls.Primitives.Popup> per utilizzi specifici:  
  
-   <xref:System.Windows.Controls.ToolTip>.  Se si desidera creare una descrizione per un elemento, utilizzare le classi <xref:System.Windows.Controls.ToolTip> e <xref:System.Windows.Controls.ToolTipService>.  Per ulteriori informazioni, vedere [Panoramica sul controllo ToolTip](../../../../docs/framework/wpf/controls/tooltip-overview.md).  
  
-   <xref:System.Windows.Controls.ContextMenu>.  Se si desidera creare un menu di scelta rapida per un elemento, utilizzare il controllo <xref:System.Windows.Controls.ContextMenu>.  Per ulteriori informazioni, vedere [Cenni preliminari sull'oggetto ContextMenu](../../../../docs/framework/wpf/controls/contextmenu-overview.md).  
  
-   <xref:System.Windows.Controls.ComboBox>.  Se si desidera creare un controllo di selezione con un elenco a discesa che può essere visualizzato o nascosto, utilizzare il controllo <xref:System.Windows.Controls.ComboBox>.  
  
-   <xref:System.Windows.Controls.Expander>.  Se si desidera creare un controllo che visualizza un'intestazione con un'area comprimibile che visualizza il contenuto, utilizzare il controllo <xref:System.Windows.Controls.Expander>.  Per ulteriori informazioni, vedere [Cenni preliminari sul controllo Expander](../../../../docs/framework/wpf/controls/expander-overview.md).  
  
<a name="PopupBehaviorandAppearance"></a>   
## Comportamento e aspetto del controllo Popup  
 Il controllo <xref:System.Windows.Controls.Primitives.Popup> fornisce funzionalità che consentono di personalizzarne il comportamento e l'aspetto.  Ad esempio, è possibile impostare il comportamento di apertura e di chiusura, l'animazione, gli effetti di opacità e bitmap e la dimensione e la posizione del controllo <xref:System.Windows.Controls.Primitives.Popup>.  
  
<a name="OpenandCloseBehavior"></a>   
### Comportamento di apertura e di chiusura  
 Un controllo <xref:System.Windows.Controls.Primitives.Popup> visualizza il relativo contenuto quando la proprietà <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> è impostata su `true`.  Per impostazione predefinita, <xref:System.Windows.Controls.Primitives.Popup> resta aperto finché la proprietà <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> non viene impostata su `false`.  Tuttavia, è possibile modificare il comportamento predefinito, impostando la proprietà <xref:System.Windows.Controls.Primitives.Popup.StaysOpen%2A> su `false`.  Quando questa proprietà viene impostata su `false`, la finestra del contenuto di <xref:System.Windows.Controls.Primitives.Popup> ha lo stato mouse capture.  Il controllo <xref:System.Windows.Controls.Primitives.Popup> perde lo stato mouse capture e la finestra viene chiusa quando si verifica un evento del mouse fuori della finestra <xref:System.Windows.Controls.Primitives.Popup>.  
  
 Gli eventi <xref:System.Windows.Controls.Primitives.Popup.Opened> e <xref:System.Windows.Controls.Primitives.Popup.Closed> vengono generati quando si apre o chiude la finestra del contenuto di <xref:System.Windows.Controls.Primitives.Popup>.  
  
<a name="Animation"></a>   
### Animazione  
 Il controllo <xref:System.Windows.Controls.Primitives.Popup> include il supporto incorporato per le animazioni generalmente associate a comportamenti quali dissolvenza in entrata e scorrimento in entrata.  È possibile attivare queste animazioni impostando la proprietà <xref:System.Windows.Controls.Primitives.Popup.PopupAnimation%2A> su un valore di enumerazione <xref:System.Windows.Controls.Primitives.PopupAnimation>.  Affinché le animazioni <xref:System.Windows.Controls.Primitives.Popup> siano eseguite correttamente, la proprietà <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> deve essere impostata su `true`.  
  
 È inoltre possibile applicare animazioni come <xref:System.Windows.Media.Animation.Storyboard> al controllo <xref:System.Windows.Controls.Primitives.Popup>.  
  
<a name="OpacityandBitmapEffects"></a>   
### Effetti di opacità e bitmap  
 La proprietà <xref:System.Windows.UIElement.Opacity%2A> di un controllo <xref:System.Windows.Controls.Primitives.Popup> non ha effetto sul relativo contenuto.  La finestra del contenuto di <xref:System.Windows.Controls.Primitives.Popup> è opaca per impostazione predefinita.  Per creare un <xref:System.Windows.Controls.Primitives.Popup> trasparente, impostare la proprietà <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> su `true`.  
  
 Il contenuto di un <xref:System.Windows.Controls.Primitives.Popup> non eredita effetti bitmap, come ad esempio <xref:System.Windows.Media.Effects.DropShadowBitmapEffect>, che vengono impostati direttamente sul controllo <xref:System.Windows.Controls.Primitives.Popup> o su qualsiasi altro elemento della finestra padre.  Per visualizzare gli effetti bitmap nel contenuto di un <xref:System.Windows.Controls.Primitives.Popup>, è necessario impostare l'effetto bitmap direttamente sul contenuto.  Ad esempio, se l'elemento figlio di un <xref:System.Windows.Controls.Primitives.Popup> è un oggetto <xref:System.Windows.Controls.StackPanel>, è necessario impostare l'effetto bitmap sull'oggetto <xref:System.Windows.Controls.StackPanel>.  
  
<a name="PopupSize"></a>   
### Dimensioni del controllo Popup  
 Per impostazione predefinita, le dimensioni del controllo <xref:System.Windows.Controls.Primitives.Popup> vengono definite automaticamente in base al contenuto.  Quando viene eseguito il ridimensionamento automatico, alcuni effetti bitmap possono essere nascosti poiché le dimensioni predefinite dell'area dello schermo definite per il contenuto di <xref:System.Windows.Controls.Primitives.Popup> non forniscono spazio sufficiente per la visualizzazione degli effetti bitmap.  
  
 Il contenuto di <xref:System.Windows.Controls.Primitives.Popup> può anche essere oscurato quando viene impostato <xref:System.Windows.UIElement.RenderTransform%2A> sul contenuto.  In questo caso, parte del contenuto può essere nascosto se il contenuto di <xref:System.Windows.Controls.Primitives.Popup> trasformato si estende oltre l'area del <xref:System.Windows.Controls.Primitives.Popup> originale.  Se un effetto bitmap o una trasformazione richiedono più spazio, è possibile definire un margine intorno al contenuto di <xref:System.Windows.Controls.Primitives.Popup> per fornire più area al controllo.  
  
<a name="DefiningPopupPosition"></a>   
## Definizione della posizione di un controllo Popup  
 Per posizionare un popup, impostare le proprietà <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>, <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>, <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>, <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffsetProperty>.  Per ulteriori informazioni, vedere [Comportamento del controllo Popup in relazione al posizionamento](../../../../docs/framework/wpf/controls/popup-placement-behavior.md).  Quando il <xref:System.Windows.Controls.Primitives.Popup> viene visualizzato sullo schermo, non viene riposizionato se non viene riposizionato il relativo controllo padre.  
  
<a name="CustomizingPopupPlacement"></a>   
### Personalizzazione del posizionamento di un oggetto Popup  
 Il posizionamento di un controllo <xref:System.Windows.Controls.Primitives.Popup> può essere personalizzato specificando una serie di coordinate relative al <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> in cui si desidera visualizzare il <xref:System.Windows.Controls.Primitives.Popup>.  
  
 Per personalizzare il posizionamento, impostare la proprietà <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> su <xref:System.Windows.Controls.Primitives.PlacementMode>.  Quindi, definire un delegato di <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> che restituisca una serie di possibili punti di posizionamento e assi primari \(in ordine di preferenza\) per il controllo <xref:System.Windows.Controls.Primitives.Popup>.  Viene selezionato automaticamente il punto che visualizza la maggior parte del <xref:System.Windows.Controls.Primitives.Popup>.  Per un esempio, vedere [Specificare un posizione personalizzata per un controllo Popup](../../../../docs/framework/wpf/controls/how-to-specify-a-custom-popup-position.md).  
  
<a name="PopupandtheVisualTree"></a>   
## Controllo Popup e struttura ad albero visuale  
 Un controllo <xref:System.Windows.Controls.Primitives.Popup> non ha una propria [struttura ad albero visuale](GTMT); restituisce invece una dimensione di 0 \(zero\) quando viene chiamato il metodo <xref:System.Windows.Controls.Primitives.Popup.MeasureOverride%2A> per il <xref:System.Windows.Controls.Primitives.Popup>.  Tuttavia, quando la proprietà <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A> del <xref:System.Windows.Controls.Primitives.Popup> viene impostata su `true`, viene creata una nuova finestra con una propria struttura ad albero visuale.  La nuova finestra contiene il contenuto di <xref:System.Windows.Controls.Primitives.Popup.Child%2A> del <xref:System.Windows.Controls.Primitives.Popup>.  La larghezza e l'altezza della nuova finestra non possono superare il 75 per cento della larghezza o dell'altezza dello schermo.  
  
 Il controllo <xref:System.Windows.Controls.Primitives.Popup> mantiene un riferimento al relativo contenuto di <xref:System.Windows.Controls.Primitives.Popup.Child%2A> come elemento figlio logico.  Quando si crea una nuova finestra, il contenuto di <xref:System.Windows.Controls.Primitives.Popup> diventa un elemento figlio visivo della finestra e resta il figlio logico del <xref:System.Windows.Controls.Primitives.Popup>.  Viceversa, il <xref:System.Windows.Controls.Primitives.Popup> resta l'elemento padre logico del relativo contenuto di <xref:System.Windows.Controls.Primitives.Popup.Child%2A>.  
  
## Vedere anche  
 <xref:System.Windows.Controls.Primitives.Popup>   
 <xref:System.Windows.Controls.Primitives.PopupPrimaryAxis>   
 <xref:System.Windows.Controls.Primitives.PlacementMode>   
 <xref:System.Windows.Controls.Primitives.CustomPopupPlacement>   
 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>   
 <xref:System.Windows.Controls.ToolTip>   
 <xref:System.Windows.Controls.ToolTipService>   
 [Procedure relative](../../../../docs/framework/wpf/controls/popup-how-to-topics.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)