---
title: "Procedura: utilizzare i trigger di evento per controllare uno storyboard dopo il relativo avvio | Microsoft Docs"
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
  - "trigger di eventi, di controllo degli storyboard"
  - "Storyboard, controllo dopo l'avvio"
  - "trigger, di controllo degli storyboard"
ms.assetid: 3b115594-6a93-4972-b24d-61aa16f1c15f
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: utilizzare i trigger di evento per controllare uno storyboard dopo il relativo avvio
In questo esempio viene illustrato come controllare un oggetto <xref:System.Windows.Media.Animation.Storyboard> dopo l'avvio.  Per avviare un oggetto <xref:System.Windows.Media.Animation.Storyboard> mediante [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], utilizzare l'oggetto <xref:System.Windows.Media.Animation.BeginStoryboard> che distribuisce le animazioni agli oggetti e alle proprietà che vengono animati, quindi avvia lo storyboard.  Se si assegna un nome all'oggetto <xref:System.Windows.Media.Animation.BeginStoryboard> specificandone la proprietà <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A>, si crea uno storyboard controllabile.  È quindi possibile controllare in modo interattivo lo storyboard dopo l'avvio.  
  
 Utilizzare le azioni di storyboard seguenti con gli oggetti <xref:System.Windows.EventTrigger> per controllare uno storyboard.  
  
-   <xref:System.Windows.Media.Animation.PauseStoryboard>: sospende lo storyboard.  
  
-   <xref:System.Windows.Media.Animation.ResumeStoryboard>: riprende uno storyboard sospeso.  
  
-   <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>: modifica la velocità dello storyboard.  
  
-   <xref:System.Windows.Media.Animation.SkipStoryboardToFill>: sposta uno storyboard alla fine del periodo di riempimento, se presente.  
  
-   <xref:System.Windows.Media.Animation.StopStoryboard>: interrompe lo storyboard.  
  
-   <xref:System.Windows.Media.Animation.RemoveStoryboard>: rimuove lo storyboard, liberando risorse.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono utilizzate azioni di storyboard controllabili per controllare in modo interattivo uno storyboard.  
  
 **Nota:** per un esempio di controllo di uno storyboard tramite codice, vedere [Controllare uno storyboard in seguito al relativo avvio utilizzando i metodi interattivi](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-storyboard-after-it-starts.md).  
  
 [!code-xml[timingbehaviors_snip#ControlStoryboardExampleUsingWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/ControlStoryboardExample.xaml#controlstoryboardexampleusingwholepage)]  
  
 Per ulteriori esempi, vedere [Raccolta di esempi di animazioni](http://go.microsoft.com/fwlink/?LinkID=159969) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.ResumeStoryboard>   
 <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>   
 <xref:System.Windows.Media.Animation.SkipStoryboardToFill>   
 <xref:System.Windows.Media.Animation.PauseStoryboard>   
 <xref:System.Windows.Media.Animation.StopStoryboard>   
 <xref:System.Windows.Media.Animation.SeekStoryboard>   
 [Controllare uno storyboard in seguito al relativo avvio utilizzando i metodi interattivi](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-storyboard-after-it-starts.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)