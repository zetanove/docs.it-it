---
title: "Procedura: disegnare un&#39;area con un pennello di sistema | Microsoft Docs"
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
  - "pennelli, disegno con pennelli di sistema"
  - "disegno, con pennelli di sistema"
  - "pennelli di sistema, disegno"
ms.assetid: 5141a763-9235-42cb-a6bb-afc75513eac7
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: disegnare un&#39;area con un pennello di sistema
La classe <xref:System.Windows.SystemColors> fornisce accesso a pennelli e colori di sistema, ad esempio <xref:System.Windows.SystemColors.ControlBrush%2A>, <xref:System.Windows.SystemColors.ControlBrushKey%2A> e <xref:System.Windows.SystemColors.DesktopBrush%2A>.  Un pennello di sistema è un oggetto <xref:System.Windows.Media.SolidColorBrush> che consente di disegnare un’area con il colore di sistema specificato.  Un pennello di sistema produce sempre un riempimento a tinta unita; non può essere utilizzato per creare una sfumatura.  
  
 È possibile utilizzare i pennelli di sistema come risorse statiche o come risorse dinamiche.  Utilizzare una risorsa dinamica se si desidera aggiornare automaticamente il pennello nel caso in cui l’utente modifichi il pennello di sistema durante l'esecuzione dell'applicazione; in caso contrario utilizzare una risorsa statica.  La classe SystemColors contiene numerose proprietà statiche che seguono una rigida convenzione di denominazione:  
  
-   *\<SystemColor\>*Brush  
  
     Ottiene un riferimento statico a un oggetto <xref:System.Windows.Media.SolidColorBrush> del colore di sistema specificato.  
  
-   *\<SystemColor\>*BrushKey  
  
     Ottiene un riferimento dinamico a un oggetto <xref:System.Windows.Media.SolidColorBrush> del colore di sistema specificato.  
  
-   *\<SystemColor\>*Color  
  
     Ottiene un riferimento statico a una struttura <xref:System.Windows.Media.Color> del colore di sistema specificato.  
  
-   *\<SystemColor\>*ColorKey  
  
     Ottiene un riferimento dinamico alla struttura <xref:System.Windows.Media.Color> del colore di sistema specificato.  
  
 Un colore di sistema è una struttura <xref:System.Windows.Media.Color> che può essere utilizzata per configurare un pennello.  Ad esempio, è possibile creare una sfumatura tramite colori di sistema impostando le proprietà <xref:System.Windows.Media.GradientStop.Color%2A> dei cursori sfumatura di un oggetto <xref:System.Windows.Media.LinearGradientBrush> con i colori di sistema.  Per un esempio, vedere [Utilizzare i colori di sistema in una sfumatura](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato un riferimento dinamico ai pennelli di sistema per impostare lo sfondo di un pulsante.  
  
 [!code-xml[brushsamples_snip#GraphicsMMDynamicSystemColorDesktopBrushKeyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemBrushExample.xaml#graphicsmmdynamicsystemcolordesktopbrushkeyexamplewholepage)]  
  
 Nell'esempio successivo viene utilizzato un riferimento statico ai pennelli di sistema per impostare lo sfondo di un pulsante.  
  
 [!code-xml[brushsamples_snip#GraphicsMMStaticSystemColorDesktopBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemBrushExample.xaml#graphicsmmstaticsystemcolordesktopbrushexamplewholepage)]  
  
 Per un esempio in cui viene illustrato come utilizzare un colore di sistema in una sfumatura, vedere [Utilizzare i colori di sistema in una sfumatura](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md).  
  
## Vedere anche  
 [Utilizzare i colori di sistema in una sfumatura](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md)   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)