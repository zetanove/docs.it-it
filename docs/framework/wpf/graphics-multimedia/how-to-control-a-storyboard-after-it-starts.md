---
title: "Procedura: controllare uno storyboard in seguito al relativo avvio | Microsoft Docs"
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
  - "Storyboard, controllo dopo l'avvio"
ms.assetid: 040f13f0-69f9-4ab5-be2b-079f4f80c7c0
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: controllare uno storyboard in seguito al relativo avvio
In questo esempio viene illustrato come utilizzare codice per controllare <xref:System.Windows.Media.Animation.Storyboard> dopo l'avvio.  Per controllare uno storyboard in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], utilizzare gli oggetti <xref:System.Windows.Trigger> e <xref:System.Windows.TriggerAction>. Per un esempio, vedere [Utilizzare i trigger di eventi per controllare uno storyboard in seguito al relativo avvio](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md).  
  
 Per avviare uno storyboard, viene utilizzato il relativo metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A>, che distribuisce le animazioni dello storyboard alle proprietà animate e avvia lo storyboard.  
  
 Per rendere controllabile uno storyboard, viene utilizzato il metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> e viene specificato **true** come secondo parametro.  È quindi possibile utilizzare i metodi interattivi dello storyboard per sospendere, riprendere, cercare, interrompere, accelerare o rallentare lo storyboard oppure andare avanti fino alla fine del segmento di tempo.  Di seguito viene fornito un elenco dei metodi interattivi dello storyboard:  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>: sospende lo storyboard.  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>: riprende uno storyboard sospeso.  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SetSpeedRatio%2A>: imposta la velocità interattiva dello storyboard.  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>: cerca la posizione specificata nello storyboard.  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SeekAlignedToLastTick%2A>: cerca la posizione specificata nello storyboard.  A differenza del metodo <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>, questa operazione viene elaborata prima del tick successivo.  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>: fa avanzare lo storyboard fino alla fine del segmento di tempo, se presente.  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>: interrompe lo storyboard.  
  
 Nell'esempio riportato di seguito vengono utilizzati vari metodi di storyboard per controllare in modo interattivo uno storyboard.  
  
 **Nota:** per un esempio di controllo di uno storyboard tramite trigger con [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], vedere [Utilizzare i trigger di eventi per controllare uno storyboard in seguito al relativo avvio](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md).  
  
## Esempio  
 [!code-csharp[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ControlStoryboardExample.cs#controlstoryboardexampleusingwholepage)]
 [!code-vb[timingbehaviors_procedural_snip#ControlStoryboardExampleUsingWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/controlstoryboardexample.vb#controlstoryboardexampleusingwholepage)]  
  
## Vedere anche  
 [Utilizzare i trigger di eventi per controllare uno storyboard in seguito al relativo avvio](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)