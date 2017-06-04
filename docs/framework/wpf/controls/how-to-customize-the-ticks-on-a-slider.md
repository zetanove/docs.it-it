---
title: "Procedura: personalizzare i segni di graduazione di un controllo Slider | Microsoft Docs"
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
  - "TickBar"
  - "Controllo dispositivo di scorrimento, creazione con TickBar"
ms.assetid: 4fa694f2-a620-4b15-be78-5f4286f89361
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: personalizzare i segni di graduazione di un controllo Slider
In questo esempio viene illustrato come creare un <xref:System.Windows.Controls.Slider> controllo che presenta segni di graduazione.  
  
## <a name="example"></a>Esempio  
 Il <xref:System.Windows.Controls.Primitives.TickBar> viene visualizzato quando imposta la <xref:System.Windows.Controls.Slider.TickPlacement%2A> proprietà su un valore diverso da <xref:System.Windows.Controls.Primitives.TickPlacement>, ovvero il valore predefinito.  
  
 Nell'esempio seguente viene illustrato come creare un <xref:System.Windows.Controls.Slider> con un <xref:System.Windows.Controls.Primitives.TickBar> che consente di visualizzare i segni di graduazione. Il <xref:System.Windows.Controls.Slider.TickPlacement%2A> e <xref:System.Windows.Controls.Slider.TickFrequency%2A> definiscono la posizione dei segni di graduazione e l'intervallo tra di essi. Quando si sposta il <xref:System.Windows.Controls.Primitives.Thumb>, le descrizioni comandi forniscono il valore di <xref:System.Windows.Controls.Slider>. Il <xref:System.Windows.Controls.Slider.AutoToolTipPlacement%2A> definisce proprietà in cui si verificano le descrizioni comandi. Il <xref:System.Windows.Controls.Primitives.Thumb> movimenti corrispondono alla posizione dei segni di graduazione poiché <xref:System.Windows.Controls.Slider.IsSnapToTickEnabled%2A> è impostato su `true`.  
  
 Nell'esempio seguente viene illustrato come utilizzare il <xref:System.Windows.Controls.Slider.Ticks%2A> proprietà per creare segni di graduazione lungo la <xref:System.Windows.Controls.Slider> in modo intermittente.  
  
 [!code-xml[Slider#4](../../../../samples/snippets/xaml/VS_Snippets_Wpf/Slider/xaml/window1.xaml#4)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.Slider>   
 <xref:System.Windows.Controls.Primitives.TickBar>   
 <xref:System.Windows.Controls.Slider.TickPlacement%2A>   
 [Procedure per il dispositivo di scorrimento](http://msdn.microsoft.com/it-it/534be86c-afb2-425d-8186-631278a9925e)