---
title: "Procedura: animare l&#39;opacit&#224; di un elemento o un pennello | Microsoft Docs"
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
  - "animazione, Opacity (proprietà)"
  - "opacità, animazione"
ms.assetid: 572af23b-39dd-48d1-9db5-4bca56a4b3d3
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: animare l&#39;opacit&#224; di un elemento o un pennello
Per applicare una dissolvenza in entrata e in uscita a un elemento del framework, è possibile animare la relativa proprietà <xref:System.Windows.UIElement.Opacity%2A> o la proprietà <xref:System.Windows.Media.Brush.Opacity%2A> di <xref:System.Windows.Media.Brush> \(o pennelli\) utilizzato per disegnarlo.  L‘animazione dell'opacità dell'elemento consente di applicare ad esso e ai relativi elementi figlio una dissolvenza in entrata e in uscita, ma l’animazione del pennello utilizzato per disegnare l'elemento consente di selezionare con maggior precisione la parte dell’elemento a cui applicare la dissolvenza.  Ad esempio, è possibile animare l’opacità di un pennello utilizzato per disegnare lo sfondo di un pulsante.  In questo modo verrebbe applicata una dissolvenza in entrata e in uscita allo sfondo del pulsante, lasciando il testo completamente opaco.  
  
> [!NOTE]
>  L’animazione di <xref:System.Windows.Media.Brush.Opacity%2A> di <xref:System.Windows.Media.Brush> offre vantaggi a livello di prestazioni rispetto all’animazione della proprietà <xref:System.Windows.UIElement.Opacity%2A> di un elemento.  
  
 Nell'esempio riportato di seguito, vengono animati due pulsanti in modo da poter applicare loro una dissolvenza in entrata e in uscita.  L'opacità del primo oggetto <xref:System.Windows.Controls.Button> viene animata da `1.0` a `0.0` su una <xref:System.Windows.Media.Animation.Timeline.Duration%2A> di cinque secondi.  Anche il secondo pulsante viene animato, ma viene animata l'opacità dell’oggetto SolidColorBrush utilizzato per disegnare <xref:System.Windows.Controls.Control.Background%2A> anziché l’opacità dell’intero pulsante.  Quando l'esempio viene eseguito, al primo pulsante viene applicata una dissolvenza in entrata e in uscita completa, mentre per il secondo pulsante la dissolvenza in entrata e in uscita viene applicata solo allo sfondo.  Il testo e il bordo rimangono completamente opachi.  
  
## Esempio  
 [!code-xml[timingbehaviors_snip#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/OpacityAnimationExample.xaml#10)]  
  
 Er questo esempio, il codice è stato omesso.  Nell’esempio completo viene anche illustrato come animare l'opacità di <xref:System.Windows.Media.Color> all'interno di <xref:System.Windows.Media.LinearGradientBrush>.  Per l'esempio completo, vedere [Esempio di animazione dell'opacità di un elemento](http://go.microsoft.com/fwlink/?LinkID=159968) \(la pagina potrebbe essere in inglese\).