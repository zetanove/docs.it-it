---
title: "Procedura: impostare una propriet&#224; dopo averla animata con uno storyboard | Microsoft Docs"
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
  - "animazione, modifica dei valori delle proprietà dopo"
ms.assetid: 79466556-4dbf-40bd-9c1e-a77613b07077
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: impostare una propriet&#224; dopo averla animata con uno storyboard
In alcuni casi, potrebbe sembrare che non sia possibile modificare il valore di una proprietà dopo che è stata animata.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.Animation.Storyboard> per aggiungere un'animazione al colore di un oggetto <xref:System.Windows.Media.SolidColorBrush>.  Lo storyboard viene attivato quando si fa clic sul pulsante.  L'evento <xref:System.Windows.Media.Animation.Timeline.Completed> viene gestito in modo che il programma riceva una notifica quando l'oggetto <xref:System.Windows.Media.Animation.ColorAnimation> viene completato.  
  
 [!code-xml[timingbehaviors_snip#GraphicsMMButton1Declaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton1declaration)]  
  
## Esempio  
 Una volta completato l'oggetto <xref:System.Windows.Media.Animation.ColorAnimation>, il programma tenta di cambiare il colore del pennello nel colore blu.  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton1Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton1handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton1Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton1handler)]  
  
 Il codice precedente non sembra eseguire alcuna azione: il pennello rimane giallo, vale a dire il valore fornito dall'oggetto <xref:System.Windows.Media.Animation.ColorAnimation> che ha animato il pennello.  Il valore della proprietà sottostante \(valore di base\) è realmente passato a blu.  Tuttavia, il valore effettivo o corrente rimane giallo in quanto l'oggetto <xref:System.Windows.Media.Animation.ColorAnimation> sta ancora eseguendo l'override del valore di base.  Se si desidera che il valore di base divenga nuovamente il valore effettivo, è necessario interrompere l'effetto dell'animazione sulla proprietà.  Esistono tre modi per eseguire questa operazione con le animazioni storyboard:  
  
-   Impostare la proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> dell'animazione su <xref:System.Windows.Media.Animation.FillBehavior>  
  
-   Rimuovere l'intero storyboard.  
  
-   Rimuovere l'animazione dalla singola proprietà.  
  
## Impostare la proprietà FillBehavior dell'animazione su Stop  
 Impostando la proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> su <xref:System.Windows.Media.Animation.FillBehavior>, si indica all'animazione di interrompere l'effetto sulla proprietà di destinazione una volta raggiunta la fine del periodo attivo.  
  
 [!code-xml[timingbehaviors_snip#GraphicsMMButton2Declaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton2declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton2Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton2handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton2Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton2handler)]  
  
## Rimuovere l'intero storyboard  
 Se si utilizza un trigger <xref:System.Windows.Media.Animation.RemoveStoryboard> o il metodo <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=fullName>, si indica alle animazioni dello storyboard di interrompere l'effetto sulle proprietà di destinazione.  La differenza tra questo approccio e l'impostazione della proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> consiste nel fatto che lo storyboard può essere rimosso in qualsiasi momento, mentre la proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> ha effetto solo quando l'animazione raggiunge la fine del periodo attivo.  
  
 [!code-xml[timingbehaviors_snip#GraphicsMMButton3Declaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton3declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton3Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton3handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton3Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton3handler)]  
  
## Rimuovere un'animazione da una singola proprietà  
 Un'altra tecnica per interrompere l'effetto di un'animazione su una proprietà consiste nell'utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> dell'oggetto animato.  Specificare la proprietà a cui si sta aggiungendo un'animazione come primo parametro e `null` come secondo.  
  
 [!code-xml[timingbehaviors_snip#GraphicsMMButton4Declaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton4declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton4Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton4handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton4Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton4handler)]  
  
 Questa tecnica funziona anche per le animazioni non storyboard.  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>   
 <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=fullName>   
 <xref:System.Windows.Media.Animation.RemoveStoryboard>   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)