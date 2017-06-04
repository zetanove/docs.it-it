---
title: "Procedura: animare una propriet&#224; utilizzando uno storyboard | Microsoft Docs"
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
  - "animazione, Storyboard"
  - "Storyboard, animazione"
ms.assetid: f4a314e9-1da2-4367-85fc-1232487efa7a
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: animare una propriet&#224; utilizzando uno storyboard
In questo esempio viene illustrato come utilizzare un oggetto <xref:System.Windows.Media.Animation.Storyboard> per animare proprietà.  Per animare una proprietà utilizzando un oggetto <xref:System.Windows.Media.Animation.Storyboard>, creare un'animazione per ogni proprietà da animare e creare inoltre un oggetto <xref:System.Windows.Media.Animation.Storyboard> per contenere le animazioni.  
  
 Il tipo di proprietà determina il tipo di animazione da utilizzare.  Ad esempio, per animare una proprietà che accetta valori <xref:System.Double>, utilizzare <xref:System.Windows.Media.Animation.DoubleAnimation>.  Utilizzare le [proprietà connesse](GTMT) <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> per specificare l'oggetto di destinazione e la proprietà cui viene applicata l'animazione.  
  
 Per avviare uno storyboard in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], utilizzare un'azione <xref:System.Windows.Media.Animation.BeginStoryboard> e un oggetto <xref:System.Windows.EventTrigger>.  <xref:System.Windows.EventTrigger> inizia l'azione <xref:System.Windows.Media.Animation.BeginStoryboard> quando si verifica l'evento specificato dalla relativa proprietà <xref:System.Windows.EventTrigger.RoutedEvent%2A>.  L'azione <xref:System.Windows.Media.Animation.BeginStoryboard> avvia <xref:System.Windows.Media.Animation.Storyboard>.  
  
 Nell'esempio seguente vengono utilizzati gli oggetti <xref:System.Windows.Media.Animation.Storyboard> per animare due controlli <xref:System.Windows.Controls.Button>.  Per modificare le dimensioni del primo pulsante, viene animata la relativa proprietà <xref:System.Windows.FrameworkElement.Width%2A>.  Per modificare il colore del secondo pulsante, viene utilizzata la proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> di <xref:System.Windows.Media.SolidColorBrush> per impostare la proprietà <xref:System.Windows.Controls.Control.Background%2A> del pulsante animato.  
  
## Esempio  
 [!code-xml[AnimatePropertyStoryboards#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/StoryboardExample.xaml#1)]  
  
> [!NOTE]
>  Anche se le animazioni possono essere destinate a un oggetto <xref:System.Windows.FrameworkElement>, ad esempio <xref:System.Windows.Controls.Control> o <xref:System.Windows.Controls.Panel>, e a un oggetto <xref:System.Windows.Freezable>, ad esempio <xref:System.Windows.Media.Brush> o <xref:System.Windows.Media.Transform>, solo gli elementi del framework includono una proprietà <xref:System.Windows.FrameworkElement.Name%2A>.  Per assegnare un nome a un oggetto bloccabile in modo che possa diventare la destinazione di un'animazione, utilizzare [Direttiva x:Name](../../../../docs/framework/xaml-services/x-name-directive.md), come illustrato nell'esempio precedente.  
  
 Se si utilizza codice, è necessario creare un oggetto <xref:System.Windows.NameScope> per un oggetto <xref:System.Windows.FrameworkElement> e registrare i nomi degli oggetti da animare con tale oggetto <xref:System.Windows.FrameworkElement>.  Per avviare le animazioni nel codice, utilizzare un'azione <xref:System.Windows.Media.Animation.BeginStoryboard> con <xref:System.Windows.EventTrigger>.  Facoltativamente, è possibile utilizzare un gestore eventi e il metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> di <xref:System.Windows.Media.Animation.Storyboard>.  Nell'esempio seguente viene illustrato come utilizzare il metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A>.  
  
 [!code-csharp[AnimatePropertyStoryboards#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimatePropertyStoryboards/CSharp/StoryboardExample.cs#11)]
 [!code-vb[AnimatePropertyStoryboards#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AnimatePropertyStoryboards/VisualBasic/StoryboardExample.vb#11)]  
  
 Per ulteriori informazioni sull'animazione e sugli storyboard, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Se si utilizza codice, non si è limitati all'utilizzo di oggetti <xref:System.Windows.Media.Animation.Storyboard> per animare le proprietà.  Per ulteriori informazioni ed esempi, vedere [Animare una proprietà senza utilizzare uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md) e [Animare una proprietà utilizzando un oggetto AnimationClock](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-an-animationclock.md).