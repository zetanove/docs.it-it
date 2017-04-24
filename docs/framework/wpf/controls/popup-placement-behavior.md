---
title: "Comportamento del controllo Popup in relazione al posizionamento | Microsoft Docs"
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
  - "popup"
  - "Controllo popup, inserimento"
  - "inserimento di popup"
  - "posizionamento di popup"
ms.assetid: fbf642e9-f670-4efd-a7af-a67468a1c8e1
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Comportamento del controllo Popup in relazione al posizionamento
Oggetto <xref:System.Windows.Controls.Primitives.Popup> controllo Visualizza il contenuto in una finestra separata mobile rispetto a un'applicazione. È possibile specificare la posizione di un <xref:System.Windows.Controls.Primitives.Popup> relativo a un controllo, il mouse o la schermata utilizzando il <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>, <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>, <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>, <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>, e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> proprietà.  Queste proprietà funzionano insieme per garantiscono la flessibilità che specifica la posizione di <xref:System.Windows.Controls.Primitives.Popup>.  
  
> [!NOTE]
>  Il <xref:System.Windows.Controls.ToolTip> e <xref:System.Windows.Controls.ContextMenu> classi anche definiscono queste cinque proprietà e si comportano in modo analogo.  
  
   
  
<a name="Positioning"></a>   
## <a name="positioning-the-popup"></a>Posizionamento di Popup  
 La posizione di un <xref:System.Windows.Controls.Primitives.Popup> può essere relativo a un <xref:System.Windows.UIElement> o a schermo intero.  L'esempio seguente crea quattro <xref:System.Windows.Controls.Primitives.Popup> controlli relativo a un <xref:System.Windows.UIElement>, in questo caso, un'immagine. Tutti il <xref:System.Windows.Controls.Primitives.Popup> controlli dispongono di <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> impostata su `image1`, ma ogni <xref:System.Windows.Controls.Primitives.Popup> ha un valore diverso per la proprietà di posizionamento.  
  
 [!code-xml[PopupPositionSnippet#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#3)]  
  
 Nella figura seguente viene mostrata l'immagine e il <xref:System.Windows.Controls.Primitives.Popup> controlli  
  
 ![Immagine con quattro controlli popup](../../../../docs/framework/wpf/controls/media/popupplacementintro.png "PopupPlacementIntro")  
Immagine con quattro controlli popup  
  
 Questo semplice esempio viene illustrato come impostare il <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> e <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> proprietà, ma utilizzando il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>, <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>, e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> proprietà, si dispone di un maggiore controllo sul posizionamento il <xref:System.Windows.Controls.Primitives.Popup> è posizionato.  
  
<a name="Definitions"></a>   
## <a name="definitions-of-terms-the-anatomy-of-a-popup"></a>Le definizioni dei termini: Anatomia di una finestra Popup  
 I termini seguenti sono utili per informazioni su come il <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>, <xref:System.Windows.Controls.Primitives.Popup.Placement%2A>, <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>, <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A>, e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> proprietà interagiscono tra di loro e <xref:System.Windows.Controls.Primitives.Popup>:  
  
-   Oggetto destinazione  
  
-   Area di destinazione  
  
-   Origine di destinazione  
  
-   Punto di allineamento popup  
  
 Questi termini offrono un modo pratico per fare riferimento a vari aspetti di <xref:System.Windows.Controls.Primitives.Popup> e il controllo che è associato.  
  
### <a name="target-object"></a>Oggetto di destinazione  
 Il *oggetto di destinazione* è l'elemento che la <xref:System.Windows.Controls.Primitives.Popup> è associato. Se il <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> è impostata, specifica l'oggetto di destinazione.  Se <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> non è impostata e <xref:System.Windows.Controls.Primitives.Popup> ha un padre, l'elemento padre è l'oggetto di destinazione.  Se è presente alcun <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> valore e alcun elemento padre, non esiste alcun oggetto di destinazione e <xref:System.Windows.Controls.Primitives.Popup> posizionato rispetto allo schermo.  
  
 Nell'esempio seguente viene creato un <xref:System.Windows.Controls.Primitives.Popup> figlio di un <xref:System.Windows.Controls.Canvas>.  Nell'esempio viene impostata la <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> proprietà di <xref:System.Windows.Controls.Primitives.Popup>. Il valore predefinito per <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode?displayProperty=fullName>, pertanto il <xref:System.Windows.Controls.Primitives.Popup> viene visualizzato sotto il <xref:System.Windows.Controls.Canvas>.  
  
 [!code-xml[PopupPositionSnippet#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#1)]  
  
 La figura seguente mostra che il <xref:System.Windows.Controls.Primitives.Popup> è posizionato in relazione al <xref:System.Windows.Controls.Canvas>.  
  
 ![Controllo popup senza PlacementTarget](../../../../docs/framework/wpf/controls/media/popupplacementnoplacementtarget.png "PopupPlacementNoPlacementTarget")  
Popup senza PlacementTarget  
  
 Nell'esempio seguente viene creato un <xref:System.Windows.Controls.Primitives.Popup> figlio di un <xref:System.Windows.Controls.Canvas>, ma questa volta il <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> è impostato su `ellipse1`, pertanto il popup viene visualizzato sotto il <xref:System.Windows.Shapes.Ellipse>.  
  
 [!code-xml[PopupPositionSnippet#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#2)]  
  
 La figura seguente mostra che il <xref:System.Windows.Controls.Primitives.Popup> è posizionato in relazione al <xref:System.Windows.Shapes.Ellipse>.  
  
 ![Popup posizionato rispetto a un'ellisse](../../../../docs/framework/wpf/controls/media/popupplacementwithplacementtarget.png "PopupPlacementWithPlacementTarget")  
Popup PlacementTarget  
  
> [!NOTE]
>  Per <xref:System.Windows.Controls.ToolTip>, il valore predefinito di <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode>.  Per <xref:System.Windows.Controls.ContextMenu>, il valore predefinito di <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode>. Questi valori vengono illustrati più avanti, in "Modalità di interazione delle proprietà."  
  
### <a name="target-area"></a>Area di destinazione  
 Il *area di destinazione* è l'area sullo schermo che il <xref:System.Windows.Controls.Primitives.Popup> fa riferimento a. Negli esempi precedenti, il <xref:System.Windows.Controls.Primitives.Popup> è allineato con i limiti dell'oggetto di destinazione, ma in alcuni casi, il <xref:System.Windows.Controls.Primitives.Popup> allineato ad altri limiti, anche se il <xref:System.Windows.Controls.Primitives.Popup> dispone di un oggetto di destinazione.  Se il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> proprietà è impostata, l'area di destinazione è diversa rispetto ai limiti dell'oggetto di destinazione.  
  
 Nell'esempio seguente vengono create due <xref:System.Windows.Controls.Canvas> oggetti, ciascuno dei quali contiene un <xref:System.Windows.Shapes.Rectangle> e <xref:System.Windows.Controls.Primitives.Popup>.  In entrambi i casi, l'oggetto di destinazione per il <xref:System.Windows.Controls.Primitives.Popup> è il <xref:System.Windows.Controls.Canvas>. Il <xref:System.Windows.Controls.Primitives.Popup> nel primo <xref:System.Windows.Controls.Canvas> ha il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> impostato, con il relativo <xref:System.Windows.Rect.X%2A>, <xref:System.Windows.Rect.Y%2A>, <xref:System.Windows.Rect.Width%2A>, e <xref:System.Windows.Rect.Height%2A> impostate rispettivamente su 50, 50, 50 e 100,. Il <xref:System.Windows.Controls.Primitives.Popup> nella seconda <xref:System.Windows.Controls.Canvas> non dispone di <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> impostato.  Di conseguenza, il primo <xref:System.Windows.Controls.Primitives.Popup> si trova sotto il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> e il secondo <xref:System.Windows.Controls.Primitives.Popup> si trova sotto il <xref:System.Windows.Controls.Canvas>. Ogni <xref:System.Windows.Controls.Canvas> contiene inoltre un <xref:System.Windows.Shapes.Rectangle> con gli stessi limiti di <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> per la prima <xref:System.Windows.Controls.Primitives.Popup>.  Si noti che il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> non crea un elemento visibile nell'applicazione; nell'esempio viene creato un <xref:System.Windows.Shapes.Rectangle> per rappresentare il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>.  
  
 [!code-xml[PopupPositionSnippet#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#4)]  
  
 Nella figura seguente viene illustrato il risultato dell'esempio precedente.  
  
 ![Popup con e senza PlacementRectangle](../../../../docs/framework/wpf/controls/media/popupplacementplacementrectangle.png "PopupPlacementPlacementRectangle")  
Popup con e senza PlacementRectangle  
  
### <a name="target-origin-and-popup-alignment-point"></a>Origine di destinazione e il punto di allineamento Popup  
 Il *origine di destinazione* e *punto di allineamento popup* sono punti di riferimento l'area di destinazione e la finestra popup, rispettivamente, che vengono utilizzati per il posizionamento. È possibile utilizzare il <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> proprietà per eseguire l'offset del popup dall'area di destinazione.  Il <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> all'origine di destinazione e il punto di allineamento popup. Il valore di <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> proprietà determina dove il punto di allineamento popup e origine destinazione si trovano.  
  
 Nell'esempio seguente viene creato un <xref:System.Windows.Controls.Primitives.Popup> e imposta il <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> proprietà su 20.  Il <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è impostata su <xref:System.Windows.Controls.Primitives.PlacementMode> (impostazione predefinita), pertanto l'origine di destinazione è l'angolo inferiore sinistro dell'area di destinazione e il punto di allineamento popup è l'angolo superiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.  
  
 [!code-xml[PopupPositionSnippet#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS/Window1.xaml#5)]  
  
 Nella figura seguente viene illustrato il risultato dell'esempio precedente.  
  
 ![Posizionamento del popup con punto di allineamento origine di destinazione](../../../../docs/framework/wpf/controls/media/popupplacementtargetoriginalignmentpoint.PNG "PopupPlacementTargetOriginAlignmentPoint")  
Popup con HorizontalOffset e VerticalOffset  
  
<a name="How"></a>   
## <a name="how-the-properties-work-together"></a>Interagiscono delle proprietà  
 I valori di <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A>, <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A>, e <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> dovranno essere considerati insieme per individuare l'area di destinazione, l'origine di destinazione e punto di allineamento popup.  Ad esempio, se il valore di <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode>, non esiste alcun oggetto di destinazione, il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> viene ignorato e l'area di destinazione è costituita dai limiti del puntatore del mouse. D'altra parte, se <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode>, <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> oppure padre determina l'oggetto di destinazione e <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> determina l'area di destinazione.  
  
 Nella tabella seguente descrive l'oggetto di destinazione, area di destinazione, origine di destinazione e il punto di allineamento popup e indica se <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> e <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> vengono utilizzati per ogni <xref:System.Windows.Controls.Primitives.PlacementMode> valore di enumerazione.  
  
|PlacementMode|Oggetto destinazione|Area di destinazione|Origine di destinazione|Punto di allineamento popup|  
|-------------------|-------------------|-----------------|-------------------|---------------------------|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Non applicabile. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> viene ignorato.|La schermata o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è rispetto allo schermo.|L'angolo superiore sinistro dell'area di destinazione.|Nell'angolo superiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Non applicabile. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> viene ignorato.|La schermata o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è rispetto allo schermo.|L'angolo superiore sinistro dell'area di destinazione.|Nell'angolo superiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> o padre.|L'oggetto di destinazione, o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è relativo all'oggetto di destinazione.|L'angolo inferiore sinistro dell'area di destinazione.|Nell'angolo superiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> o padre.|L'oggetto di destinazione, o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è relativo all'oggetto di destinazione.|Il centro dell'area di destinazione.|Al centro del <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> o padre.|L'oggetto di destinazione, o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è relativo all'oggetto di destinazione.|Definita per il <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>.|Definita per il <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> o padre.|L'oggetto di destinazione, o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è relativo all'oggetto di destinazione.|L'angolo superiore sinistro dell'area di destinazione.|Nell'angolo superiore destro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Non applicabile. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> viene ignorato.|I limiti del puntatore del mouse. <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> viene ignorato.|L'angolo inferiore sinistro dell'area di destinazione.|Nell'angolo superiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Non applicabile. <xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> viene ignorato.|I limiti del puntatore del mouse. <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> viene ignorato.|L'angolo superiore sinistro dell'area di destinazione.|Nell'angolo superiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> o padre.|L'oggetto di destinazione, o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è relativo all'oggetto di destinazione.|L'angolo superiore sinistro dell'area di destinazione.|Nell'angolo superiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> o padre.|L'oggetto di destinazione, o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è relativo all'oggetto di destinazione.|L'angolo superiore sinistro dell'area di destinazione.|Nell'angolo superiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> o padre.|L'oggetto di destinazione, o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è relativo all'oggetto di destinazione.|L'angolo superiore destro dell'area di destinazione.|Nell'angolo superiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|<xref:System.Windows.Controls.Primitives.Popup.PlacementTarget%2A> o padre.|L'oggetto di destinazione, o <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> se è impostata.  Il <xref:System.Windows.Controls.Primitives.Popup.PlacementRectangle%2A> è relativo all'oggetto di destinazione.|L'angolo superiore sinistro dell'area di destinazione.|Nell'angolo inferiore sinistro di <xref:System.Windows.Controls.Primitives.Popup>.|  
  
 Nell'illustrazione seguente vengono mostrati il <xref:System.Windows.Controls.Primitives.Popup>, area di destinazione, origine di destinazione e dell'allineamento popup punti per ogni <xref:System.Windows.Controls.Primitives.PlacementMode> valore. In ogni figura è giallo, l'area di destinazione e il <xref:System.Windows.Controls.Primitives.Popup> è blu.  
  
 ![Popup con posizionamento Absolute o AbsolutePoint](../../../../docs/framework/wpf/controls/media/popupplacementabsolute.png "PopupPlacementAbsolute")  
È importante la sistemazione Absolute o AbsolutePoint  
  
 ![Popup con posizionamento Bottom](../../../../docs/framework/wpf/controls/media/popupplacementbottom.png "PopupPlacementBottom")  
La posizione è Bottom  
  
 ![Popup con posizionamento Center](../../../../docs/framework/wpf/controls/media/popupplacementcenter.png "PopupPlacementCenter")  
La posizione è Center  
  
 ![Popup con posizionamento Left](../../../../docs/framework/wpf/controls/media/popupplacementleft.png "PopupPlacementLeft")  
La posizione è Left  
  
 ![Popup con posizionamento Mouse](../../../../docs/framework/wpf/controls/media/popupplacementmouse.png "PopupPlacementMouse")  
La posizione è Mouse  
  
 ![Popup con posizionamento MousePoint](../../../../docs/framework/wpf/controls/media/popupplacementmousepoint.png "PopupPlacementMousePoint")  
La posizione è MousePoint  
  
 ![Popup con posizionamento relative o RelativePoint](../../../../docs/framework/wpf/controls/media/popupplacementrelative.png "PopupPlacementRelative")  
È importante la sistemazione relative o RelativePoint  
  
 ![Popup con posizionamento Right](../../../../docs/framework/wpf/controls/media/popupplacementright.png "PopupPlacementRight")  
La posizione è Right  
  
 ![Popup con posizionamento Top](../../../../docs/framework/wpf/controls/media/popupplacementtop.png "PopupPlacementTop")  
La posizione è Top  
  
<a name="When"></a>   
## <a name="when-the-popup-encounters-the-edge-of-the-screen"></a>Quando il Popup rileva il bordo dello schermo  
 Per motivi di sicurezza, un <xref:System.Windows.Controls.Primitives.Popup> non possono essere nascosti in base al bordo dello schermo. Si verifica una delle tre situazioni seguenti quando il <xref:System.Windows.Controls.Primitives.Popup> rileva un bordo dello schermo:  
  
-   La finestra popup viene riposizionato lungo il bordo dello schermo che nasconde il <xref:System.Windows.Controls.Primitives.Popup>.  
  
-   Il popup utilizza un punto di allineamento popup diversi.  
  
-   Il popup utilizza un punto di allineamento popup e origine di destinazione diversa.  
  
 Queste opzioni sono descritte dettagliatamente più avanti in questa sezione.  
  
 Il comportamento di <xref:System.Windows.Controls.Primitives.Popup> quando rileva un bordo dello schermo dipende dal valore di <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> proprietà e schermata bordo rilevato. Nella tabella seguente viene riepilogato il comportamento quando la <xref:System.Windows.Controls.Primitives.Popup> rileva un bordo dello schermo per ogni <xref:System.Windows.Controls.Primitives.PlacementMode> valore.  
  
|PlacementMode|Bordo superiore|Bordo inferiore|Bordo sinistro|Bordo destro|  
|-------------------|--------------|-----------------|---------------|----------------|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|Allinea il bordo inferiore.|Allinea il bordo sinistro.|Allinea il bordo destro.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|Il punto di allineamento popup viene modificato nell'angolo inferiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.|Allinea il bordo sinistro.|Il punto di allineamento popup viene modificato nell'angolo superiore destro del <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|L'origine di destinazione viene modificato nell'angolo superiore sinistro dell'area di destinazione e il punto di allineamento popup viene modificato nell'angolo inferiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.|Allinea il bordo sinistro.|Allinea il bordo destro.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|Allinea il bordo inferiore.|Allinea il bordo sinistro.|Allinea il bordo destro.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|Allinea il bordo inferiore.|L'origine di destinazione viene modificato nell'angolo superiore destro dell'area di destinazione e il punto di allineamento popup viene modificato nell'angolo superiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.|Allinea il bordo destro.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|L'origine di destinazione viene modificato nell'angolo superiore sinistro dell'area di destinazione (i limiti del puntatore del mouse) e il punto di allineamento popup viene modificato nell'angolo inferiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.|Allinea il bordo sinistro.|Allinea il bordo destro.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|Il punto di allineamento popup viene modificato nell'angolo inferiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.|Allinea il bordo sinistro.|L'allineamento popup punto viene modificato nell'angolo superiore destro della finestra popup.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|Allinea il bordo inferiore.|Allinea il bordo sinistro.|Allinea il bordo destro.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|Il punto di allineamento popup viene modificato nell'angolo inferiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.|Allinea il bordo sinistro.|L'allineamento popup punto viene modificato nell'angolo superiore destro della finestra popup.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|Viene allineato al bordo superiore.|Allinea il bordo inferiore.|Allinea il bordo sinistro.|L'origine di destinazione viene modificato nell'angolo superiore sinistro dell'area di destinazione e il punto di allineamento popup viene modificato nell'angolo superiore destro del <xref:System.Windows.Controls.Primitives.Popup>.|  
|<xref:System.Windows.Controls.Primitives.PlacementMode>|L'origine di destinazione viene modificato nell'angolo inferiore sinistro dell'area di destinazione e il punto di allineamento popup viene modificato nell'angolo superiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>. In effetti, è uguale a quella del <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode>.|Allinea il bordo inferiore.|Allinea il bordo sinistro.|Allinea il bordo destro.|  
  
### <a name="aligning-to-the-screen-edge"></a>Allineamento al bordo dello schermo  
 Oggetto <xref:System.Windows.Controls.Primitives.Popup> può essere allineato al bordo dello schermo riposizionando stesso così l'intero <xref:System.Windows.Controls.Primitives.Popup> è visibile sullo schermo.  In questo caso, la distanza tra il punto di allineamento popup e origine di destinazione potrebbero essere diversi dai valori di <xref:System.Windows.Controls.Primitives.Popup.HorizontalOffset%2A> e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A>. Quando <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode>, <xref:System.Windows.Controls.Primitives.PlacementMode>, o <xref:System.Windows.Controls.Primitives.PlacementMode>, <xref:System.Windows.Controls.Primitives.Popup> viene allineato a ogni bordo dello schermo.  Ad esempio, si supponga che un <xref:System.Windows.Controls.Primitives.Popup> è <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> impostato su <xref:System.Windows.Controls.Primitives.PlacementMode> e <xref:System.Windows.Controls.Primitives.Popup.VerticalOffset%2A> impostato su 100.  Se il bordo inferiore dello schermo nasconde tutto o parte del <xref:System.Windows.Controls.Primitives.Popup>, <xref:System.Windows.Controls.Primitives.Popup> riposizionato lungo il bordo inferiore dello schermo e la distanza verticale tra l'origine di destinazione e popup punto di allineamento è minore di 100. Nella figura seguente viene illustrato quanto descritto.  
  
 ![Popup allineato al bordo dello schermo](../../../../docs/framework/wpf/controls/media/popupplacementrelativescreenedge.png "PopupPlacementRelativeScreenEdge")  
Popup allineato al bordo dello schermo  
  
### <a name="changing-the-popup-alignment-point"></a>La modifica del punto di allineamento Popup  
 Se <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode>, <xref:System.Windows.Controls.Primitives.PlacementMode>, o <xref:System.Windows.Controls.Primitives.PlacementMode>, il punto di allineamento popup viene modificato quando il popup rileva il bordo inferiore o destro dello schermo.  
  
 Nella figura seguente viene dimostrato che quando il bordo inferiore dello schermo nasconde tutto o parte del <xref:System.Windows.Controls.Primitives.Popup>, il punto di allineamento popup è l'angolo inferiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![Nuovo punto di allineamento dovuto al bordo inferiore dello schermo](../../../../docs/framework/wpf/controls/media/popupplacementrelativepointscreenedge.png "PopupPlacementRelativePointScreenEdge")  
Il popup rileva il bordo inferiore dello schermo e il punto di allineamento popup  
  
 Nella figura seguente viene illustrato che quando il <xref:System.Windows.Controls.Primitives.Popup> è nascosto dal bordo destro dello schermo, il punto di allineamento popup è l'angolo superiore destro di <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![Nuovo punto di allineamento popup dovuto al bordo dello schermo](../../../../docs/framework/wpf/controls/media/popupplacementrelativepointrightscreenedge.png "PopupPlacementRelativePointRightScreenEdge")  
Popup rileva il bordo destro dello schermo e il punto di allineamento popup  
  
 Se il <xref:System.Windows.Controls.Primitives.Popup> rileva i bordi inferiore e destro dello schermo, il punto di allineamento popup è l'angolo in basso a destra del <xref:System.Windows.Controls.Primitives.Popup>.  
  
### <a name="changing-the-target-origin-and-popup-alignment-point"></a>Modifica l'origine di destinazione e il punto di allineamento Popup  
 Quando <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode>, <xref:System.Windows.Controls.Primitives.PlacementMode>, <xref:System.Windows.Controls.Primitives.PlacementMode>, <xref:System.Windows.Controls.Primitives.PlacementMode>, o <xref:System.Windows.Controls.Primitives.PlacementMode>, l'allineamento di origine e la finestra popup di destinazione se il punto viene rilevato un determinato bordo dello schermo.  Dipende dal bordo dello schermo che determina la posizione modificare il <xref:System.Windows.Controls.Primitives.PlacementMode> valore.  
  
 Nella figura seguente viene illustrato che quando <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode> e <xref:System.Windows.Controls.Primitives.Popup> rileva il bordo inferiore dello schermo, l'origine di destinazione è l'angolo superiore sinistro dell'area di destinazione e il punto di allineamento popup è l'angolo inferiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![Nuovo punto di allineamento dovuto al bordo inferiore dello schermo](../../../../docs/framework/wpf/controls/media/popupplacementbottomscreenedge.png "PopupPlacementBottomScreenEdge")  
La posizione è inferiore e il popup rileva il bordo inferiore dello schermo  
  
 Nella figura seguente viene illustrato che quando <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode> e <xref:System.Windows.Controls.Primitives.Popup> rileva il bordo sinistro dello schermo, l'origine di destinazione è l'angolo superiore destro dell'area di destinazione e il punto di allineamento popup è l'angolo superiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![Nuovo punto di allineamento dovuto al bordo sinistro dello schermo](../../../../docs/framework/wpf/controls/media/popupplacementleftscreenedge.png "PopupPlacementLeftScreenEdge")  
La posizione è a sinistra e il popup rileva il bordo sinistro della schermata  
  
 Nella figura seguente viene illustrato che quando <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode> e <xref:System.Windows.Controls.Primitives.Popup> rileva il bordo destro dello schermo, l'origine di destinazione è l'angolo superiore sinistro dell'area di destinazione e il punto di allineamento popup è l'angolo superiore destro del <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![Nuovo punto di allineamento dovuto al bordo destro dello schermo](../../../../docs/framework/wpf/controls/media/popupplacementrightscreenedge.png "PopupPlacementRightScreenEdge")  
La posizione è Right e il popup rileva il bordo destro dello schermo  
  
 Nella figura seguente viene illustrato che quando <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode> e <xref:System.Windows.Controls.Primitives.Popup> rileva il bordo superiore dello schermo, l'origine di destinazione è l'angolo inferiore sinistro dell'area di destinazione e il punto di allineamento popup è l'angolo superiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![Nuovo punto di allineamento dovuto al bordo superiore dello schermo](../../../../docs/framework/wpf/controls/media/popupplacementtopscreenedge.png "PopupPlacementTopScreenEdge")  
La posizione è Top e il popup rileva il bordo superiore dello schermo  
  
 Nella figura seguente viene illustrato che quando <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> è <xref:System.Windows.Controls.Primitives.PlacementMode> e <xref:System.Windows.Controls.Primitives.Popup> rileva il bordo inferiore dello schermo, l'origine di destinazione è l'angolo superiore sinistro dell'area di destinazione (i limiti del puntatore del mouse) e il punto di allineamento popup è l'angolo inferiore sinistro del <xref:System.Windows.Controls.Primitives.Popup>.  
  
 ![nuovo punto di allineamento dovuto al mouse vicino al bordo dello schermo](../../../../docs/framework/wpf/controls/media/popupplacementmousescreenedge.png "PopupPlacementMouseScreenEdge")  
La posizione è Mouse e il popup rileva il bordo inferiore dello schermo  
  
### <a name="customizing-popup-placement"></a>Personalizzazione di posizionamento del Popup  
 È possibile personalizzare il punto di allineamento popup e origine destinazione impostando il <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> proprietà <xref:System.Windows.Controls.Primitives.PlacementMode>. Quindi definire un <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> delegato che restituisce un set di possibili punti di posizionamento e assi primari (in ordine di preferenza) per il <xref:System.Windows.Controls.Primitives.Popup>. Il punto che visualizza la maggior parte del <xref:System.Windows.Controls.Primitives.Popup> è selezionata.  La posizione del <xref:System.Windows.Controls.Primitives.Popup> viene adattata automaticamente se il <xref:System.Windows.Controls.Primitives.Popup> nascosto dal bordo dello schermo. Per un esempio, vedere [specificare una posizione di Popup personalizzato](../../../../docs/framework/wpf/controls/how-to-specify-a-custom-popup-position.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di posizionamento](http://go.microsoft.com/fwlink/?LinkID=160032)