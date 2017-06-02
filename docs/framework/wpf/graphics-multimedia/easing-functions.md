---
title: "Funzioni di interpolazione | Microsoft Docs"
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
  - "applicazione di formule matematiche ad animazioni [WPF]"
  - "applicazione di funzioni di interpolazione ad animazioni [WPF]"
  - "applicazione ad animazioni formule matematiche [WPF]"
  - "animazioni [WPF], movimento realistico"
  - "funzioni di interpolazione [WPF]"
  - "personalizzazione delle funzioni di interpolazione [WPF]"
  - "funzioni di interpolazione [WPF], definizione"
  - "funzioni di interpolazione [WPF], personalizzazione"
  - "applicare animazioni [WPF]"
ms.assetid: 075b9c2b-82c4-43fa-b3cd-de0b6236eb38
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Funzioni di interpolazione
Funzioni di interpolazione consentono di applicare formule matematiche personalizzate alle animazioni. Ad esempio, è un oggetto realisticamente rimbalzo o si comportano come se fosse su una molla. È possibile utilizzare fotogrammi chiave o anche animazioni From/To/By per simulare gli effetti, ma richiederebbe una quantità significativa di lavoro e l'animazione potrebbe essere meno accurata rispetto all'utilizzo di una formula matematica.  
  
 Oltre a creare una funzione di interpolazione personalizzata ereditando da <xref:System.Windows.Media.Animation.EasingFunctionBase>, è possibile utilizzare una delle diverse funzioni di interpolazione fornite dal runtime per creare effetti comuni.  
  
-   <xref:System.Windows.Media.Animation.BackEase>: ritrae leggermente il movimento di un'animazione prima di iniziare a eseguire un'animazione nel percorso indicato.  
  
-   <xref:System.Windows.Media.Animation.BounceEase>: crea un effetto di rimbalzo.  
  
-   <xref:System.Windows.Media.Animation.CircleEase>: crea un'animazione che accelera e/o rallenta utilizzando una funzione circolare.  
  
-   <xref:System.Windows.Media.Animation.CubicEase>: crea un'animazione che accelera e/o rallenta utilizzando la formula *f*( *t*) = *t*<sup>3</sup>.  
  
-   <xref:System.Windows.Media.Animation.ElasticEase>: consente di creare un'animazione simile a una molla che oscilla avanti e indietro fino ad arrestarsi.  
  
-   <xref:System.Windows.Media.Animation.ExponentialEase>: crea un'animazione che accelera e/o rallenta utilizzando una formula esponenziale.  
  
-   <xref:System.Windows.Media.Animation.PowerEase>: crea un'animazione che accelera e/o rallenta utilizzando la formula *f*( *t*) = *t*<sup>p</sup> dove p è uguale al <xref:System.Windows.Media.Animation.PowerEase.Power%2A> proprietà.  
  
-   <xref:System.Windows.Media.Animation.QuadraticEase>: crea un'animazione che accelera e/o rallenta utilizzando la formula *f*( *t*) = *t*<sup>2</sup>.  
  
-   <xref:System.Windows.Media.Animation.QuarticEase>: crea un'animazione che accelera e/o rallenta utilizzando la formula *f*( *t*) = *t*<sup>4</sup>.  
  
-   <xref:System.Windows.Media.Animation.QuinticEase>: creare un'animazione che accelera e/o rallenta utilizzando la formula *f*( *t*) = *t*<sup>5</sup>.  
  
-   <xref:System.Windows.Media.Animation.SineEase>: crea un'animazione che accelera e/o rallenta utilizzando una formula sinusoidale.  
  
 È possibile esplorare il comportamento di queste funzioni di interpolazione con l'esempio seguente.  
  
 [Eseguire questo esempio](http://go.microsoft.com/fwlink/?LinkId=139798&sref=easing_functions_gallery)  
  
 Per applicare una funzione di interpolazione per un'animazione, utilizzare il `EasingFunction` proprietà dell'animazione specificare la funzione di interpolazione da applicare all'animazione. Nell'esempio seguente viene applicato un <xref:System.Windows.Media.Animation.BounceEase> funzione di interpolazione un <xref:System.Windows.Media.Animation.DoubleAnimation> per creare un effetto di rimbalzo.  
  
 [Eseguire questo esempio](http://go.microsoft.com/fwlink/?LinkId=139798&sref=BounceEase)  
  
 [!code-xml[BounceEase_snippet#BounceEase](../../../../samples/snippets/csharp/VS_Snippets_Wpf/bounceease_snippet/CS/window1.xaml#bounceease)]  
  
 Nell'esempio precedente, è stata applicata la funzione di interpolazione per From/To/By animazione. È inoltre possibile applicare queste funzioni di interpolazione ad animazioni di fotogrammi chiave. Nell'esempio seguente viene illustrato come utilizzare fotogrammi chiave sono associate funzioni di interpolazione per creare un'animazione di un rettangolo che contratti verso l'alto, basso, quindi si espande verso il basso (come se fallback) e fatto rimbalzare fino ad arrestarsi.  
  
 [Eseguire questo esempio](http://go.microsoft.com/fwlink/?LinkId=139798&sref=EasingFunctionDoubleKeyFrame)  
  
 [!code-xml[EasingFunctionDoubleKeyFrame_snippet#EasingFunctionDoubleKeyFrame](../../../../samples/snippets/csharp/VS_Snippets_Wpf/easingfunctiondoublekeyframe_snippet/CS/window1.xaml#easingfunctiondoublekeyframe)]  
  
 È possibile utilizzare il <xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A> di modifica delle proprietà per modificare la funzione di interpolazione comportamento, vale a dire la modalità di interpolazione di animazione. Esistono tre possibili valori, è possibile fornire per <xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A>:  
  
-   <xref:System.Windows.Media.Animation.EasingMode>: l'interpolazione segue la formula matematica associata alla funzione di interpolazione.  
  
-   <xref:System.Windows.Media.Animation.EasingMode>: l'interpolazione segue interpolazione al 100% meno l'output della formula associata alla funzione di interpolazione.  
  
-   <xref:System.Windows.Media.Animation.EasingMode>: interpolazione utilizza <xref:System.Windows.Media.Animation.EasingMode> per la prima metà dell'animazione e <xref:System.Windows.Media.Animation.EasingMode> nella seconda metà.  
  
 Le immagini seguenti vengono illustrati i diversi valori di <xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A> in *f*( *x*) rappresenta l'avanzamento dell'animazione e *t* rappresenta l'ora.  
  
 <xref:System.Windows.Media.Animation.BackEase>  
  
 ![Grafici di BackEase EasingMode. ] (../Image/BackEase_Graph.png "BackEase_Graph")  
  
 <xref:System.Windows.Media.Animation.BounceEase>  
  
 ![Grafici di BounceEase EasingMode. ] (../Image/BounceEase_Graph.png "BounceEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CircleEase>  
  
 ![Grafici di CircleEase EasingMode. ] (../Image/CircleEase_Graph.png "CircleEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CubicEase>  
  
 ![Grafici di CubicEase EasingMode. ] (../Image/CubicEase_Graph.png "CubicEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ElasticEase>  
  
 ![ElasticEase con grafici di EasingMode diversi. ] (../Image/ElasticEase_Graph.png "ElasticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ExponentialEase>  
  
 ![Grafici di ExponentialEase con EasingMode diversi. ] (../Image/ExponentialEase_Graph.png "ExponentialEase_Graph")  
  
 <xref:System.Windows.Media.Animation.PowerEase>  
  
 ![QuarticEase con grafici di EasingMode diversi. ] (../Image/QuarticEase_Graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuadraticEase>  
  
 ![QuadraticEase con grafici di EasingMode diversi](../../../../docs/framework/wpf/graphics-multimedia/media/quadraticease-graph.png "QuadraticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuarticEase>  
  
 ![QuarticEase con grafici di EasingMode diversi. ] (../Image/QuarticEase_Graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuinticEase>  
  
 ![QuinticEase con grafici di EasingMode diversi. ] (../Image/QuinticEase_Graph.png "QuinticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.SineEase>  
  
 ![SineEase per valori EasingMode diversi](../../../../docs/framework/wpf/graphics-multimedia/media/sineease-graph.png "SineEase_Graph")  
  
> [!NOTE]
>  È possibile utilizzare <xref:System.Windows.Media.Animation.PowerEase> per creare lo stesso comportamento di <xref:System.Windows.Media.Animation.CubicEase>, <xref:System.Windows.Media.Animation.QuadraticEase>, <xref:System.Windows.Media.Animation.QuarticEase>, e <xref:System.Windows.Media.Animation.QuinticEase> utilizzando il <xref:System.Windows.Media.Animation.PowerEase.Power%2A> proprietà. Ad esempio, se si desidera utilizzare <xref:System.Windows.Media.Animation.PowerEase> in sostituzione di <xref:System.Windows.Media.Animation.CubicEase>, specificare un <xref:System.Windows.Media.Animation.PowerEase.Power%2A> valore 3.  
  
 Oltre a utilizzare le funzioni di interpolazione incluse in fase di esecuzione, è possibile creare funzioni di interpolazione personalizzate ereditando da <xref:System.Windows.Media.Animation.EasingFunctionBase>. Nell'esempio seguente viene illustrato come creare una semplice funzione di interpolazione personalizzata. È possibile aggiungere la propria logica matematica per determinare la funzione di interpolazione comportamento eseguendo l'override di <xref:System.Windows.Media.Animation.EasingFunctionBase.EaseInCore%2A> metodo.  
  
 [Eseguire questo esempio](http://go.microsoft.com/fwlink/?LinkId=139798&sref=CustomEasingFunction)  
  
 [!code-csharp[CustomEasingFunction#CustomEasingFunction](../../../../samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/customlog10easingfunction.cs#customeasingfunction)]
 [!code-vb[CustomEasingFunction#CustomEasingFunction](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/customeasingfunction/visualbasic/customlog10easingfunction.vb#customeasingfunction)]
 [!code-xml[CustomEasingFunction#CustomEasingFunction](../../../../samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/window1.xaml#customeasingfunction)]