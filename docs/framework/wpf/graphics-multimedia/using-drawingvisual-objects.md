---
title: "Utilizzo degli oggetti DrawingVisual | Microsoft Docs"
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
  - "DrawingVisual (oggetti nel livello visivo)"
  - "livello visivo, DrawingVisual (oggetti)"
ms.assetid: 0b4e711d-e640-40cb-81c3-8f5c59909b7d
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Utilizzo degli oggetti DrawingVisual
In questo argomento vengono forniti cenni preliminari sull'utilizzo di oggetti <xref:System.Windows.Media.DrawingVisual> al livello visivo di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Di seguito sono elencate le diverse sezioni di questo argomento.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
-   [Oggetto DrawingVisual](#drawing_visual_object)  
  
-   [Contenitore host di DrawingVisual](#drawingvisual_host_container)  
  
-   [Creazione di oggetti DrawingVisual](#creating_drawingvisual_objects)  
  
-   [Creazione di override per i membri FrameworkElement](#creating_overrides)  
  
-   [Supporto per l'hit testing](#providing_hit_testing_support)  
  
-   [Argomenti correlati](#seeAlsoToggle)  
  
<a name="drawingvisual_object"></a>   
## Oggetto DrawingVisual  
 <xref:System.Windows.Media.DrawingVisual> è una classe di disegno semplificata utilizzata per il rendering di forme, immagini o testo.  Questa classe è considerata semplice perché non fornisce la gestione del layout o degli eventi, migliorando in tal modo le prestazioni.  Per questo motivo, i disegni sono ideali per gli sfondi e per ClipArt.  
  
<a name="drawingvisual_host_container"></a>   
## Contenitore host di DrawingVisual  
 Per utilizzare oggetti <xref:System.Windows.Media.DrawingVisual> è necessario creare un contenitore host.  L'oggetto contenitore host deve derivare dalla classe <xref:System.Windows.FrameworkElement> che fornisce il layout e il supporto per la gestione di eventi che mancano alla classe <xref:System.Windows.Media.DrawingVisual>.  Tramite l'oggetto contenitore host non vengono visualizzate proprietà visibili, poiché lo scopo principale di questo oggetto è quello di contenere oggetti figlio.  Tuttavia, è necessario impostare la proprietà <xref:System.Windows.UIElement.Visibility%2A> del contenitore host su <xref:System.Windows.Visibility>. In caso contrario, nessuno degli elementi figlio sarà visibile.  
  
 Quando si crea un oggetto contenitore host per gli oggetti visivi, è necessario archiviare i riferimenti agli oggetti visivi in <xref:System.Windows.Media.VisualCollection>.  Utilizzare il metodo <xref:System.Windows.Media.VisualCollection.Add%2A> per aggiungere un oggetto visivo al contenitore host.  Nell'esempio riportato di seguito, viene creato un oggetto contenitore host e tre oggetti visivi vengono aggiunti a <xref:System.Windows.Media.VisualCollection>.  
  
 [!code-csharp[DrawingVisualSample#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[DrawingVisualSample#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#100)]  
  
> [!NOTE]
>  Per l'esempio di codice completo dal quale è stato estratto l'esempio di codice precedente, vedere [Esempio di hit test mediante DrawingVisual](http://go.microsoft.com/fwlink/?LinkID=159994) \(la pagina potrebbe essere in inglese\).  
  
<a name="creating_drawingvisual_objects"></a>   
## Creazione di oggetti DrawingVisual  
 Quando viene creato, un oggetto <xref:System.Windows.Media.DrawingVisual> non ha contenuto di disegno.  È possibile aggiungere contenuto di testo, grafica o immagini recuperando <xref:System.Windows.Media.DrawingContext> per l'oggetto e disegnandovi.  <xref:System.Windows.Media.DrawingContext> viene restituito chiamando il metodo <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A> di un oggetto <xref:System.Windows.Media.DrawingVisual>.  
  
 Per disegnare un rettangolo in <xref:System.Windows.Media.DrawingContext> utilizzare il metodo <xref:System.Windows.Media.DrawingContext.DrawRectangle%2A>dell'oggetto <xref:System.Windows.Media.DrawingContext>.  Sono disponibili metodi simili per disegnare altri tipi di contenuto.  Al termine delle operazioni di disegno del contenuto in <xref:System.Windows.Media.DrawingContext>, chiamare il metodo <xref:System.Windows.Media.DrawingContext.Close%2A> per chiudere <xref:System.Windows.Media.DrawingContext> e mantenere il contenuto.  
  
 Nell'esempio riportato di seguito, viene creato un oggetto <xref:System.Windows.Media.DrawingVisual> e viene disegnato un rettangolo in <xref:System.Windows.Media.DrawingContext>.  
  
 [!code-csharp[DrawingVisualSample#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[DrawingVisualSample#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
<a name="creating_overrides"></a>   
## Creazione di override per i membri FrameworkElement  
 L'oggetto contenitore host è responsabile della gestione della raccolta di oggetti visivi.  A tale scopo, è necessario che il contenitore host implementi l'override di membri per la classe <xref:System.Windows.FrameworkElement> derivata.  
  
 Nell'elenco riportato di seguito vengono descritti due membri per i quali è necessario eseguire l'override:  
  
-   <xref:System.Windows.FrameworkElement.GetVisualChild%2A>: restituisce un elemento figlio in corrispondenza dell'indice specificato dalla raccolta di elementi figlio.  
  
-   <xref:System.Windows.FrameworkElement.VisualChildrenCount%2A>: ottiene il numero di elementi figlio visivi all'interno di questo elemento.  
  
 Nell'esempio riportato di seguito, viene implementato l'override per i due membri <xref:System.Windows.FrameworkElement>.  
  
 [!code-csharp[DrawingVisualSample#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#102)]
 [!code-vb[DrawingVisualSample#102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#102)]  
  
<a name="providing_hit_testing_support"></a>   
## Supporto per l'hit testing  
 L'oggetto contenitore host può fornire la gestione degli eventi, anche se non visualizza alcuna proprietà visibile. Si noti tuttavia che la proprietà <xref:System.Windows.UIElement.Visibility%2A> del contenitore deve essere impostata su <xref:System.Windows.Visibility>.  Consente di creare una routine di gestione degli eventi per il contenitore host in grado di intercettare eventi del mouse, ad esempio il rilascio del pulsante sinistro del mouse.  Tramite la routine di gestione degli eventi è quindi possibile implementare l'hit testing richiamando il metodo <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A>.  Il parametro <xref:System.Windows.Media.HitTestResultCallback> del metodo fa riferimento a una procedura definita dall'utente che è possibile utilizzare per determinare l'azione risultante di un hit test.  
  
 Nell'esempio riportato di seguito, il supporto per l'hit testing viene implementato per l'oggetto contenitore host e i relativi elementi figlio.  
  
 [!code-csharp[DrawingVisualSample#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#103)]
 [!code-vb[DrawingVisualSample#103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#103)]  
  
## Vedere anche  
 <xref:System.Windows.Media.DrawingVisual>   
 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A>   
 [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [Hit testing a livello visivo](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)