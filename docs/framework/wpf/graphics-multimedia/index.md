---
title: "Grafica e funzionalit&#224; multimediali | Microsoft Docs"
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
  - "animazione, funzionalità"
  - "funzionalità grafiche"
  - "supporto, funzionalità"
  - "effetti sonori"
  - "effetti di transizione"
  - "effetti video"
ms.assetid: 1817d9dc-3d6c-46cb-afc8-63b0bae35e37
caps.latest.revision: 30
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# Grafica e funzionalit&#224; multimediali
<a name="introduction"></a> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] offre supporto per contenuto multimediale, grafica vettoriale, animazione e composizione di contenuto, consentendo agli sviluppatori di compilare interfacce utente e contenuto interessanti.  Tramite [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] è possibile creare grafica vettoriale o animazioni complesse e integrare supporti nelle applicazioni.  
  
 In questo argomento vengono illustrate le funzionalità relative alla grafica, all'animazione e ai supporti di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che consentono di aggiungere grafica, effetti di transizione, suoni e video alle applicazioni.  
  
> [!NOTE]
>  L'utilizzo di tipi WPF in un servizio Windows è fortemente sconsigliato.  Se si tenta di utilizzare i tipi WPF in un servizio Windows, è possibile che tale servizio non funzioni come previsto.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="whats_new_with_graphics_and_multimedia_in_wpf_4"></a>   
## Novità di WPF 4 relativamente a grafica e contenuti multimediali  
 Sono state apportate diverse modifiche correlate agli elementi grafici e alle animazioni.  
  
-   Arrotondamento del layout  
  
     Quando il bordo di un oggetto cade in corrispondenza del centro del pixel di un dispositivo, il sistema grafico indipendente dai dpi può creare elementi di rendering, ad esempio bordi sfuocati o semitrasparenti.  La gestione di questa situazione nelle versioni precedenti di WPF veniva realizzata tramite il blocco dei pixel.  In Silverlight 2 è stato introdotto l'arrotondamento del layout, ovvero un'altra modalità di spostamento degli elementi che determina il posizionamento dei bordi in corrispondenza dei limiti di pixel interi.  In WPF è ora supportato l'arrotondamento del layout con la proprietà collegata <xref:System.Windows.FrameworkElement.UseLayoutRounding%2A> su <xref:System.Windows.FrameworkElement>.  
  
-   Composizione memorizzata nella cache  
  
     Tramite le nuove classi <xref:System.Windows.Media.BitmapCache> e <xref:System.Windows.Media.BitmapCacheBrush>, è possibile memorizzare nella cache una parte complessa della struttura ad albero visuale come bitmap e migliorare notevolmente i tempi di rendering.  La bitmap risponderà all'input dell'utente, ad esempio i clic del mouse, e sarà possibile disegnarla su altri elementi esattamente come con un qualsiasi pennello.  
  
-   Supporto di Pixel Shader 3  
  
     WPF 4 si basa sul supporto di <xref:System.Windows.Media.Effects.ShaderEffect> introdotto in WPF 3.5 SP1, consentendo la scrittura di effetti per le applicazioni tramite Pixel Shader \(PS\) versione 3.0.  Il modello di shader PS 3.0 è più avanzato rispetto a PS 2.0 e rende disponibile un maggior numero di effetti nell'hardware supportato.  
  
-   Funzioni di interpolazione  
  
     È possibile migliorare la qualità delle animazioni utilizzando le funzioni di interpolazione che forniscono il controllo sul comportamento delle animazioni.  È ad esempio possibile applicare un oggetto <xref:System.Windows.Media.Animation.ElasticEase> a un'animazione per conferire all'animazione un effetto molla.  Per ulteriori informazioni, vedere i tipi di interpolazione nello spazio dei nomi <xref:System.Windows.Media.Animation>.  
  
<a name="graphics_and_rendering"></a>   
## Grafica e rendering  
 WPF include supporto per grafica 2D di elevata qualità.  La funzionalità include pennelli, geometrie, immagini, forme e trasformazioni.  Per ulteriori informazioni, vedere [Grafica](../../../../docs/framework/wpf/graphics-multimedia/graphics.md).  Il rendering degli elementi grafici si basa sulla classe <xref:System.Windows.Media.Visual>.  La struttura degli oggetti visivi sullo schermo è descritta dalla struttura ad albero visuale.  Per ulteriori informazioni, vedere [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md).  
  
### Forme 2D  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce una libreria di forme [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] basate su vettore e di utilizzo comune quali rettangoli ed ellissi, come illustrato di seguito.  
  
 ![Ellissi e rettangoli](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure4.png "WPFIntroFigure4")  
  
 Queste forme [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] intrinseche non sono solo forme, ma elementi programmabili che implementano molte funzionalità tipiche dei controlli più comuni, incluso l'input della tastiera e del mouse.  Nell'esempio seguente viene illustrato come gestire l'evento <xref:System.Windows.UIElement.MouseUp> generato facendo clic su un elemento <xref:System.Windows.Shapes.Ellipse>.  
  
```xaml  
<Window  
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
  
 Di seguito viene illustrato l'output per il code\-behind e il markup [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] precedente.  
  
 ![Finestra con il testo "you clicked the ellipse&#33;"](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure12.png "WPFIntroFigure12")  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md).  Per un esempio introduttivo, vedere [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037).  
  
### Geometrie 2D  
 Se le forme [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] fornite da [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] non sono sufficienti, è possibile utilizzare il supporto [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per geometrie e percorsi e crearne di personalizzati.  Di seguito viene illustrato come utilizzare le geometrie per creare forme, ad esempio un pennello, e per ridimensionare altri elementi [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 ![Vari usi di Path](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure5.png "WPFIntroFigure5")  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  Per un esempio introduttivo, vedere [Esempio di geometrie](http://go.microsoft.com/fwlink/?LinkID=159989).  
  
### Effetti 2D  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce una libreria di classi [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] che è possibile utilizzare per creare molteplici effetti.  La funzionalità di rendering [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente di disegnare elementi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] con sfumature, bitmap, disegni e video, nonché di modificarli tramite rotazione, ridimensionamento e [inclinazione](GTMT).  Nell'illustrazione seguente viene fornito un esempio dei molti effetti che è possibile ottenere utilizzando i pennelli [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
 ![Illustrazione di pennelli diversi](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure6.png "WPFIntroFigure6")  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sui pennelli di WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-brushes-overview.md).  Per un esempio introduttivo, vedere [Esempio Brush](http://go.microsoft.com/fwlink/?LinkID=159973).  
  
<a name="rendering"></a>   
## Rendering 3D  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce un insieme di funzionalità di rendering [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] integrabili con il supporto della grafica [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per creare layout, elementi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]e visualizzazione dei dati più accattivanti.  A una estremità dello spettro, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente di eseguire il rendering delle immagini [!INCLUDE[TLA2#tla_2d](../../../../includes/tla2sharptla-2d-md.md)] sulle superfici di forme [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)], come illustrato di seguito.  
  
 ![Schermata dell'esempio Visual3D](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure13.png "WPFIntroFigure13")  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md).  Per un esempio introduttivo, vedere [Esempio di solidi 3D](http://go.microsoft.com/fwlink/?LinkID=159964).  
  
<a name="animation"></a>   
## Animazione  
 Utilizzare l'animazione per applicare ai controlli e agli elementi gli effetti di dissolvenza, rotazione, ingrandimento e tremolio, nonché per creare accattivanti transizioni tra le pagine e molto altro.  Poiché [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente di animare la maggior parte delle proprietà, non solo è possibile animare la maggior parte degli oggetti [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], ma anche utilizzare [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] per animare gli oggetti personalizzati creati.  
  
 ![Immagini di un cubo animato](../../../../docs/framework/wpf/graphics-multimedia/media/wpfintrofigure7.png "WPFIntroFigure7")  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  Per un esempio introduttivo, vedere [Raccolta di esempi di animazioni](http://go.microsoft.com/fwlink/?LinkID=159969).  
  
<a name="media"></a>   
## Supporti multimediali  
 Immagini, video e audio sono supporti multimediali per trasmettere informazioni ed esperienze utente.  
  
### Immagini  
 Le immagini, ovvero icone, sfondi e parti di animazioni, sono fondamentali per la maggior parte delle applicazioni.  Perché è spesso necessario utilizzare le immagini, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente di utilizzarle in vari modi.  Di seguito viene illustrato uno di questi modi.  
  
 ![Schermata dell'esempio Styling](../../../../docs/framework/wpf/controls/media/stylingintro-eventtriggers.png "StylingIntro\_EventTriggers")  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md).  
  
### Video e audio  
 Una caratteristica fondamentale delle funzionalità grafiche di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è rappresentata dal supporto nativo per l'utilizzo di contenuti multimediali, inclusi video e audio.  Nell'esempio seguente viene illustrato come inserire un lettore multimediale in un'applicazione.  
  
```xaml  
<MediaElement Source="media\numbers.wmv" Width="450" Height="250" />  
```  
  
 L'oggetto <xref:System.Windows.Controls.MediaElement> consente di riprodurre video e audio e la sua estensibilità è tale consentire la creazione di [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] personalizzate.  
  
 Per ulteriori informazioni, vedere [Panoramica delle funzionalità multimediali](../../../../docs/framework/wpf/graphics-multimedia/multimedia-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Media>   
 <xref:System.Windows.Media.Animation>   
 <xref:System.Windows.Media.Media3D>   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Animation and Timing](http://msdn.microsoft.com/it-it/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [3\-D Graphics](http://msdn.microsoft.com/it-it/565c1f3c-235b-47de-b05b-3b53ed63f1b8)   
 [Multimedia](http://msdn.microsoft.com/it-it/44a8dcd0-80cb-4db0-a222-87cde68c2fac)