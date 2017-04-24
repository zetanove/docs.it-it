---
title: "Grafica e funzionalità multimediali | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework-4.6
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- media, features
- video effects
- sound effects
- animation, features
- graphics features
- transition effects
ms.assetid: 1817d9dc-3d6c-46cb-afc8-63b0bae35e37
caps.latest.revision: 30
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: ea78944133412f43075d8d094cd5fa93685299f9
ms.lasthandoff: 04/08/2017

---
# <a name="graphics-and-multimedia"></a>Grafica e funzionalità multimediali
<a name="introduction"></a> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornisce il supporto per funzionalità multimediali, grafica vettoriale, animazione e composizione del contenuto, consentendo agli sviluppatori di creare interfacce utente e contenuto interessanti. Tramite [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)], è possibile creare grafica vettoriale o animazioni complesse e integrare file multimediali nelle applicazioni.  
  
 Questo argomento presenta le funzionalità di grafica, di animazione e di file multimediali di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], che consentono di aggiungere elementi grafici, effetti di transizione, audio e video alle applicazioni.  
  
> [!NOTE]
<<<<<<< HEAD
>  L'uso di tipi WPF in un servizio Windows è fortemente sconsigliato. Se si tenta di usare tipi WPF in un servizio Windows, è possibile che tale servizio non funzioni come previsto.   
=======
>  L'utilizzo di tipi WPF in un servizio Windows è fortemente sconsigliato.  Se si tenta di utilizzare i tipi WPF in un servizio Windows, è possibile che tale servizio non funzioni come previsto.  
  
   
>>>>>>> 91db859... fix build error
  
<a name="whats_new_with_graphics_and_multimedia_in_wpf_4"></a>   
## <a name="whats-new-with-graphics-and-multimedia-in-wpf-4"></a>Novità di grafica e funzionalità multimediali in WPF 4  
 Sono state apportate diverse modifiche correlate agli elementi grafici e alle animazioni.  
  
-   Arrotondamento del layout  
  
     Quando il bordo di un oggetto cade al centro del pixel di un dispositivo, il sistema grafico indipendente da DPI può creare elementi di rendering, ad esempio bordi sfocati o semitrasparenti. Le versioni precedenti di WPF includevano lo snapping dei pixel per gestire questa situazione. In Silverlight 2 è stato introdotto l'arrotondamento del layout, che è un altro modo per spostare gli elementi in modo che i bordi rientrino nei limiti dei pixel intero. WPF ora supporta ora l'arrotondamento del layout con la proprietà associata <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> su <xref:System.Windows.FrameworkElement>.  
  
-   Composizione memorizzata nella cache  
  
     Usando le nuove classi <xref:System.Windows.Media.BitmapCache> e <xref:System.Windows.Media.BitmapCacheBrush>, è possibile memorizzare nella cache un aspetto complesso della struttura ad albero visuale come bitmap e migliorare notevolmente il tempo di rendering. La bitmap risponderà all'input dell'utente, ad esempio i clic del mouse, e sarà possibile disegnarla su altri elementi esattamente come con un pennello.  
  
-   Supporto Pixel Shader 3  
  
     WPF 4 si basa sul supporto <xref:System.Windows.Media.Effects.ShaderEffect> introdotto in WPF 3.5 SP1, consentendo alle applicazioni di scrivere effetti usando Pixel Shader (PS) versione 3.0. Il modello di shader PS 3.0 è più avanzato rispetto a PS 2.0 e rende disponibile un maggior numero di effetti nell'hardware supportato.  
  
-   Funzioni di interpolazione  
  
     È possibile migliorare le animazioni con funzioni di interpolazione che forniscono il controllo del comportamento delle animazioni. È possibile ad esempio applicare un oggetto <xref:System.Windows.Media.Animation.ElasticEase> a un'animazione per fornire un effetto molla. Per altre informazioni, vedere i tipi di interpolazione nello spazio dei nomi <xref:System.Windows.Media.Animation>.  
  
<a name="graphics_and_rendering"></a>   
## <a name="graphics-and-rendering"></a>Grafica e rendering  
 WPF include il supporto per gli elementi grafici 2D di qualità elevata. La funzionalità include pennelli, geometrie, immagini, forme e trasformazioni. Per altre informazioni, vedere [Grafica](../../../../docs/framework/wpf/graphics-multimedia/graphics.md). Il rendering degli elementi grafici è basato sulla classe <xref:System.Windows.Media.Visual>. La struttura degli oggetti visivi sullo schermo è descritta dalla struttura ad albero visuale. Per altre informazioni, vedere [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md).  
  
### <a name="2-d-shapes"></a>Forme 2D  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce una libreria di forme [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] di uso comune basate su vettori, ad esempio i rettangoli e le ellissi mostrati nella figura seguente.  
  
 ![Ellissi e rettangoli](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure4.PNG "WPFIntroFigure4")  
  
 Queste forme [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] intrinseche non sono solo forme: sono elementi programmabili che implementano molte delle funzionalità tipiche dei controlli più comuni, che includono l'input della tastiera e del mouse. L'esempio seguente illustra come gestire l'evento <xref:System.Windows.UIElement.MouseUp> generato facendo clic su un elemento <xref:System.Windows.Shapes.Ellipse>.  
  
```xaml  
\<Window  
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
  x:Class="Window1" >  
  <Ellipse Fill="LightBlue" MouseUp="ellipseButton_MouseUp" />  
</Window>  
```  
  
```csharp  
public partial class Window1  : Window  
{  
    void ellipseButton_MouseUp(object sender, MouseButtonEventArgs e)  
    {  
        MessageBox.Show("You clicked the ellipse!");  
    }  
}  
```  
  
```vb  
Partial Public Class Window1  
    Inherits Window  
    Private Sub ellipseButton_MouseUp(ByVal sender As Object, ByVal e As MouseButtonEventArgs)  
        MessageBox.Show("You clicked the ellipse!")  
    End Sub  
End Class  
  
```  
  
 Nella figura seguente viene illustrato l'output del markup e code-behind [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] precedente.  
  
 ![Finestra con il testo "you clicked the ellipse&#33;"](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure12.png "WPFIntroFigure12")  
  
 Per altre informazioni, vedere [Panoramica degli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md). Per un esempio introduttivo, vedere [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037).  
  
### <a name="2-d-geometries"></a>Geometrie 2D  
 Quando le forme [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] fornite da [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] non sono sufficienti, è possibile usare il supporto [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per creare geometrie e tracciati personalizzati. La figura seguente mostra come usare le geometrie per creare forme, ad esempio un pennello da disegno e per ritagliare altri elementi [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 ![Vari usi di Path](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure5.PNG "WPFIntroFigure5")  
  
 Per altre informazioni, vedere [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md). Per un esempio introduttivo, vedere [Esempio di geometrie](http://go.microsoft.com/fwlink/?LinkID=159989).  
  
### <a name="2-d-effects"></a>Effetti 2D  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce una libreria di classi [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] che è possibile usare per creare una vasta gamma di effetti. La funzionalità di rendering [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] offre la possibilità di disegnare elementi [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] che hanno gradienti, bitmap, disegni e video e di modificarli mediante rotazione, ridimensionamento e inclinazione. La figura seguente fornisce un esempio dei molti effetti che è possibile ottenere usando i pennelli [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 ![Illustrazione di pennelli diversi](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure6.PNG "WPFIntroFigure6")  
  
 Per altre informazioni, vedere [Panoramica dei pennelli di WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-brushes-overview.md). Per un esempio introduttivo, vedere [Esempio di pennelli](http://go.microsoft.com/fwlink/?LinkID=159973).  
  
<a name="rendering"></a>   
## <a name="3-d-rendering"></a>Rendering 3D  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce un set di funzionalità di rendering [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] che si integrano con il supporto della grafica [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per la creazione di layout, [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] e visualizzazione dei dati più interessanti. A un'estremità dello spettro, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente di eseguire il rendering di immagini [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] su superfici di forme [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)], come illustrato di seguito.  
  
 ![Screenshot dell'esempio Visual3D](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure13.png "WPFIntroFigure13")  
  
 Per altre informazioni, vedere [Panoramica della grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md). Per un esempio introduttivo, vedere [Esempio di solidi 3D](http://go.microsoft.com/fwlink/?LinkID=159964).  
  
<a name="animation"></a>   
## <a name="animation"></a>Animazione  
 Usare l'animazione per applicare ai controlli e agli elementi gli effetti di ingrandimento, tremolio, rotazione e dissolvenza, nonché per creare interessanti transizioni tra le pagine e altro ancora. Poiché [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente di animare la maggior parte delle proprietà, non solo è possibile animare la maggior parte degli oggetti [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], ma è anche possibile usare [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per animare oggetti personalizzati creati.  
  
 ![Immagini di un cubo animato](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure7.png "WPFIntroFigure7")  
  
 Per altre informazioni, vedere [Panoramica dell'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md). Per un esempio introduttivo, vedere [Raccolta di esempi di animazioni](http://go.microsoft.com/fwlink/?LinkID=159969).  
  
<a name="media"></a>   
## <a name="media"></a>Supporti  
 Immagini, video e audio sono supporti multimediali per trasmettere informazioni ed esperienze utente.  
  
### <a name="images"></a>Immagini  
 Le immagini, tra cui le icone, gli sfondi e le parti di animazioni, sono un componente fondamentale della maggior parte delle applicazioni. Poiché spesso è necessario usare le immagini, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente di usarle in vari modi. La figura seguente mostra uno dei vari modi.  
  
 ![Screenshot di esempio di applicazione di uno stile](../../../../docs/framework/wpf/controls/media/stylingintro-eventtriggers.png "StylingIntro_EventTriggers")  
  
 Per altre informazioni, vedere [Panoramica della creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md).  
  
### <a name="video-and-audio"></a>Video e audio  
 Una caratteristica fondamentale delle funzionalità grafiche di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consiste nel fornire il supporto nativo per l'uso di contenuti multimediali, inclusi video e audio. L'esempio seguente illustra come inserire un lettore multimediale in un'applicazione.  
  
```xaml  
<MediaElement Source="media\numbers.wmv" Width="450" Height="250" />  
```  
  
 <xref:System.Windows.Controls.MediaElement> è in grado di riprodurre video e audio ed è sufficientemente estensibile per consentire la creazione di [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] personalizzate.  
  
 Per altre informazioni, vedere [Panoramica delle funzionalità multimediali](../../../../docs/framework/wpf/graphics-multimedia/multimedia-overview.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Media>   
 <xref:System.Windows.Media.Animation>   
 <xref:System.Windows.Media.Media3D>   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Animazione e sistema di temporizzazione](http://msdn.microsoft.com/en-us/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [Grafica tridimensionale](http://msdn.microsoft.com/en-us/565c1f3c-235b-47de-b05b-3b53ed63f1b8)   
 [Elementi multimediali](http://msdn.microsoft.com/en-us/44a8dcd0-80cb-4db0-a222-87cde68c2fac)
